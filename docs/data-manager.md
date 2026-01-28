The NHANESImageMapper class handles the pairing of tabular NHANES data with corresponding images. It prepares data for use with a multi-input deep learning pipeline.

## Purpose
* Load and clean NHANES tabular data
* Match records with corresponding image files using SEQN IDs
* Create training and testing datasets
* Ensure compatibility with MultiModalDataGenerator

## Constructor
`NHANESImageMapper(tabular_path, image_dir)`

## Parameters

|Name | Type | Description |
|-----|------|-------------|
|`tabular_path`| `str` | Path to tabular data CSV files.|
|`img_dir` |`str`| Path to image directory (e.g., `Image data/`)

## Key Methods
`create_paired_dataset(test_size=0.2, random_state=42)`
Pairs image paths with tabular rows and splits into train/test sets.

* Returns:
```python
{
    "train": list[dict],
    "test": list[dict]
}
```
Each `dict` contains:

```python
{
    "image_path": "dataset/Image data/0012.jpg",
    "features": { "age": 23, "bmi": 18.5, ... },
    "label": "mild"
}
```

`_preprocess_tabular_data(df)`
* Internal method
* Cleans, selects, and standardizes the tabular features
* Drops rows with missing or unmatchable values

`_pair_data(tabular_df)`
* Internal method
* Links each row of tabular data with its image (if the image exists)
* Returns a list of paired samples

## Expected File Structure
```kotlin
dataset/
├── NHANES/
│   └── merged_data.csv         ← Tabular data
└── Image data/
    ├── train
    ├── test
    └── ...
```
* `merged_data.csv` must include a column `SEQN` for matching
* Filenames like `0012.jpg` must match values in `SEQN` column

## Example Usage
```python
from data_manager import NHANESImageMapper

mapper = NHANESImageMapper(
    tabular_path="dataset/NHANES/merged_data.csv",
    image_dir="dataset/Image data/"
)

paired_data = mapper.create_paired_dataset()

print(paired_data["train"][0])
# {
#   "image_path": "dataset/Image data/0012.jpg",
#   "features": {"age": 23, "bmi": 18.5, ...},
#   "label": "moderate"
# }
```

## Notes
* Handles internal cleaning of tabular data
* Ensures only valid samples with both tabular and image data are included
* Meant to be used upstream of the Keras MultiModalDataGenerator

