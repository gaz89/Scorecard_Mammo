# Mammography Feature Extraction Pipeline

An automated workflow for extracting both handcrafted and deep convolutional features from mammography images across real (patient) and synthetic datasets.

---

## Table of Contents

- [Overview](#overview)  
- [Directory Structure](#directory-structure)  
- [Dependencies](#dependencies)  
- [Configuration](#configuration)  
- [Usage](#usage)  
- [Features Extracted](#features-extracted)  
  - [Handcrafted Features](#handcrafted-features)  
  - [VGG16 Deep Features](#vgg16-deep-features)  
  - [ResNet50 Deep Features](#resnet50-deep-features)  
- [Output](#output)  
- [License](#license)  

---

## Overview

This repository provides a Python script to process mammography images and extract:

1. **Handcrafted statistical and topological descriptors** (mean, std, skew, kurtosis, median, edge features, frequency energy, Betti numbers).  
2. **Deep convolutional features** using pre-trained **VGG16** (no top layer) and **ResNet50** models.  

The extracted features are saved for downstream analysis, such as dataset comparison, clustering, or machine learning tasks.

---

## Directory Structure

```
.
├── README.md
├── feature_extraction.py          # Main feature extraction script
├── requirements.txt               # Required Python packages
└── data/
    ├── patient/                   # Patient image folders
    └── synthetic/                 # Synthetic image folders

# Generated outputs
└── features_output/
    ├── handcrafted/               # CSV files of handcrafted features
    ├── vgg16/                     # NPZ files of VGG16 features
    └── resnet/                    # NPZ files of ResNet50 features
```

---

## Dependencies

Install required packages with:

```bash
pip install -r requirements.txt
```

**requirements.txt** should include:
```text
numpy>=1.21
pandas>=1.3
matplotlib>=3.4
scipy>=1.7
scikit-learn>=1.0
torch>=1.10
torchvision>=0.11
Pillow>=8.0
scikit-image>=0.18
gudhi>=3.4.0
tqdm>=4.60
```

---

## Configuration

At the top of `feature_extraction.py`, define:

- **DATASETS**: mapping dataset names → local image folder paths.  
- **IMAGE_EXTS**: allowed file extensions (`.jpg`, `.png`, `.tif`, `.dicom`, etc.).  
- **SAVE_DIR**: base directory for output features (subfolders: `handcrafted`, `vgg16`, `resnet`).  
- **IMG_SIZE_VGG**: target size for VGG16 input (default 512×512).  
- **IMG_SIZE_RES**: target size for ResNet50 input (default 224×224).  

Adjust paths and sizes as needed.

---

## Usage

Run the script:

```bash
python feature_extraction.py
```

By default, the script loops over each dataset in `DATASETS` and each feature type (`handcrafted`, `vgg16`, `resnet`):

- **Handcrafted**: computes features for each grayscale image, saves a CSV per dataset.  
- **VGG16**: loads images, extracts flattened feature maps, saves as compressed NPZ.  
- **ResNet50**: batches images, extracts final convolutional layer activations, saves NPZ.

Existing feature files are loaded if present (`--load-existing` flag can be toggled in the code).

Progress bars (via `tqdm`) show extraction progress.

---

## Features Extracted

### Handcrafted Features
- **Statistical**: mean, standard deviation, skewness, kurtosis, median  
- **Edge**: edge density, average edge pixel intensity (Canny)  
- **Frequency**: low/high-frequency energy from FFT magnitude  
- **Topological**: Betti-0 and Betti-1 from cubical complex persistence (GUDHI)

### VGG16 Deep Features
- **Model**: ImageNet‐pretrained VGG16 (no dense layers)  
- **Output**: flattened feature maps per image  

### ResNet50 Deep Features
- **Model**: ImageNet‐pretrained ResNet50 (all layers except final classifier)  
- **Output**: pooled convolutional feature vector per image  

---

## Output

All feature files are saved under `features_output/`:

- **handcrafted/\<dataset>_handcrafted.csv**  
- **vgg16/\<dataset>_vgg16.npz** (key: `features`)  
- **resnet/\<dataset>_resnet.npz**  

Load with `pandas.read_csv` for CSV or `np.load(..., allow_pickle=True)['features']` for NPZ.

---

## License

[Specify your license here]
