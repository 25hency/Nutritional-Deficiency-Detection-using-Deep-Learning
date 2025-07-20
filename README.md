# Deep Learning for Detection of Nutritional Deficiencies from Skin Images

![Project Status](https://img.shields.io/badge/status-active-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg)](CONTRIBUTING.md)

This project uses deep learning techniques to detect nutritional deficiencies through multimodal analysis of dermatological images combined with health metrics data from NHANES (National Health and Nutrition Examination Survey).

## 🎯 Project Overview

This multimodal approach combines:

1. **Dermatological images** showing various skin conditions
2. **Health metrics data** from NHANES datasets, including dietary intake, laboratory tests, examination results, and demographics

By leveraging both visual and tabular data, our models can detect correlations between skin conditions and nutritional status, potentially enabling early detection of nutritional deficiencies through skin analysis.

## 🧠 Key Features

- **Data Integration Framework**: Maps NHANES patient data to dermatological images
- **Custom Data Generator**: Efficient multimodal data generator for training deep learning models
- **EfficientNet-based Architecture**: Advanced CNN architecture for image processing
- **Multimodal Fusion**: Novel approach to combine tabular health data with image features
- **Evaluation Framework**: Comprehensive tools to assess model performance

## 📋 Requirements

- Python 3.8+
- TensorFlow 2.x
- pandas
- numpy
- scikit-learn
- matplotlib
- jupyter

## 🔧 Setup & Installation

1. Clone this repository
   ```bash
   git clone https://github.com/25hency/Deep-Learning-for-detection-of-nutritional-deficiencies-from-skin-image.git
   cd Deep-Learning-for-detection-of-nutritional-deficiencies-from-skin-image
   ```

2. Create a virtual environment:
   ```bash
   python -m venv env
   ```

3. Activate the virtual environment:
   - Windows: `env\Scripts\activate`
   - Mac/Linux: `source env/bin/activate`

4. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## 📁 Data Structure

The project expects the following directory structure:

```
project/
├── dataset/
│   ├── NHANES/
│   │   ├── diet.csv
│   │   ├── examination.csv
│   │   ├── labs.csv
│   │   ├── demographic.csv
│   │   └── ...
│   ├── Image data/
│   │   ├── train/
│   │   │   └── [image categories]/
│   │   └── test/
│   │       └── [image categories]/
│   └── Time-Series Data/
│       └── weight_change_dataset.csv
├── results/
│   └── [model outputs]/
├── data_mapper.py
├── custom_data_generator.py
└── notebooks/
    ├── eda.ipynb
    ├── train_multimodal.ipynb
    └── evaluate_multimodal_model.ipynb
```

## 💻 Usage

### Data Preparation

```python
from data_mapper import NHANESImageMapper

# Initialize the mapper
mapper = NHANESImageMapper(
    nhanes_dir="dataset/NHANES",
    image_dir="dataset/Image data"
)

# Load and process data
nhanes_data = mapper.load_nhanes_data()

# Create synthetic mapping between patients and images
mapping = mapper.create_synthetic_mapping(save_path="patient_image_mapping.json")

# Create paired datasets for training
paired_dataset = mapper.create_paired_dataset()
```

### Model Training

```python
from custom_data_generator import MultiModalDataGenerator
import tensorflow as tf

# Create data generators
train_generator = MultiModalDataGenerator(
    dataset=paired_dataset['train'],
    batch_size=32,
    image_size=(224, 224),
    shuffle=True,
    augment=True
)

# Build and train model
# See train_multimodal.ipynb for the complete implementation
```

## 📊 Notebooks

- `eda.ipynb`: Exploratory data analysis of NHANES data and skin images
- `train_multimodal.ipynb`: End-to-end model training pipeline
- `evaluate_multimodal_model.ipynb`: Comprehensive model evaluation

## 📂 Key Files

- `data_mapper.py`: Creates mappings between NHANES data and dermatological images
- `custom_data_generator.py`: Efficient data generator for multimodal learning
- `patient_image_mapping.json`: Generated mapping between patients and images
- `requirements.txt`: List of dependencies

## 🤝 Contributing

Contributions are welcome! Please read our [Contributing Guidelines](CONTRIBUTING.md) for details on how to submit pull requests, report issues, or suggest enhancements.

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## �‍💻 Contribution Opportunities

We welcome contributions to improve this project! Here are some current areas we're looking for help with:

### 🐛 Current Issues
- **Data Augmentation**: Implement additional augmentation techniques for skin images
- **Model Optimization**: Improve inference speed without sacrificing accuracy
- **Data Preprocessing**: Enhance preprocessing pipeline for NHANES data
- **UI/Visualization**: Create better visualization tools for model interpretability

### 🚀 Feature Requests
- **Mobile Integration**: Develop a mobile interface for on-device inference
- **Additional Data Sources**: Integrate additional health databases beyond NHANES
- **Transfer Learning**: Experiment with different pretrained models beyond EfficientNet
- **Time Series Analysis**: Improve handling of temporal health data

See our [CONTRIBUTING.md](CONTRIBUTING.md) file for guidelines on how to contribute.

## �📧 Contact

For any questions or collaborations, please open an issue on our GitHub repository.

## 🙏 Acknowledgements

- NHANES for providing comprehensive health data
- The open-source dermatological image collections used for training
