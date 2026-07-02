# Tanager Hyperspectral Land Cover Classification Framework

A reproducible Python workflow for hyperspectral land cover classification using **Tanager-1 hyperspectral imagery**, integrating **Principal Component Analysis (PCA)**, **Random Forest (RF)** classification, and **spatial post-processing**. The framework evaluates the influence of **10 m** and **50 m** reference datasets on classification accuracy, with particular emphasis on detecting **solar photovoltaic (PV) installations** and **greenhouses**.

---

## Overview

Hyperspectral imagery provides hundreds of contiguous spectral bands that enable detailed discrimination of land cover types beyond the capability of conventional multispectral sensors. However, the high dimensionality of hyperspectral data introduces challenges such as spectral redundancy, computational cost, and increased model complexity.

This repository presents a complete end-to-end workflow that addresses these challenges through:

- Spectral standardization
- Principal Component Analysis (PCA)
- Random Forest classification
- Majority filtering
- Morphological refinement
- GeoTIFF export
- Accuracy assessment
- Publication-quality visualization

The workflow is fully implemented in **Python** using open-source geospatial and machine learning libraries.

---

## Study Area

- **Satellite:** Tanager-1 (Planet Labs)
- **Location:** Hekinan, Aichi Prefecture, Japan
- **Acquisition Date:** May 3, 2025
- **Data Format:** HDFEOS (HDF5)
- **Product:** Surface Reflectance
- **Spatial Resolution:** ~35.75 m
- **Coordinate Reference System:** EPSG:32653 (UTM Zone 53N)

---

## Workflow

The complete processing pipeline consists of the following stages:

```
Tanager HDF5 Image
        │
        ▼
Read Hyperspectral Cube
        │
        ▼
Generate Training Labels
(JAXA HRLULC 10 m / 50 m)
        │
        ▼
Spectral Standardization
        │
        ▼
Principal Component Analysis
(30 Components)
        │
        ▼
Random Forest Training
(400 Trees)
        │
        ▼
Accuracy Assessment
        │
        ▼
Full-Scene Classification
        │
        ▼
Majority Filtering
        │
        ▼
Morphological Refinement
        │
        ▼
GeoTIFF Export
        │
        ▼
Publication Figures
```

---

## Land Cover Classes

The framework supports the following land cover classes.

| ID | Class |
|----|----------------|
| 1 | Cropland |
| 2 | Built-up Area |
| 3 | Grassland |
| 4 | Greenhouse |
| 5 | Paddy Field |
| 6 | Solar Panel |
| 7 | Water |
| 8 | Bare Land |

The study specifically evaluates the detection performance of:

- Solar photovoltaic (PV) installations
- Agricultural greenhouses

---

## Feature Engineering

The preprocessing pipeline consists of two main steps:

### Spectral Standardization

Each spectral band is standardized to zero mean and unit variance to ensure equal contribution during model training.

### Principal Component Analysis (PCA)

PCA reduces the original hyperspectral feature space into **30 principal components**, preserving the dominant spectral variance while reducing redundancy and computational cost.

---

## Machine Learning Model

The classification model uses a **Random Forest** classifier with:

- 400 decision trees
- Stratified 70:30 train-test split
- Majority voting prediction
- Pixel-wise classification

Random Forest was selected because it:

- Handles high-dimensional hyperspectral data efficiently
- Is robust to noisy training samples
- Requires minimal parameter tuning
- Provides feature importance
- Produces stable classification performance

---

## Spatial Post-Processing

To improve spatial consistency, the classified maps undergo three refinement steps:

1. **5 × 5 Majority Filtering**
2. **Binary Opening (3 × 3)**
3. **Binary Closing (5 × 5)**
4. **Final Majority Filtering**

These operations reduce salt-and-pepper noise while preserving meaningful land cover boundaries.

---

## Accuracy Assessment

Model performance is evaluated using multiple complementary metrics:

- Overall Accuracy (OA)
- Confusion Matrix
- Precision
- Recall
- F1-score
- ROC-AUC (One-vs-Rest)

This comprehensive evaluation assesses both overall predictive performance and class-specific reliability.

---

## Outputs

The workflow generates:

- Land cover classification maps
- GeoTIFF raster products
- Classification visualizations
- Confusion matrices
- Accuracy reports
- PCA feature importance plots
- Surface reflectance signature plots
- Publication-ready figures

---

## Software Requirements

- Python 3.10 or later

Main dependencies:

- numpy
- scipy
- pandas
- matplotlib
- h5py
- rasterio
- geopandas
- scikit-learn
- scikit-image
- affine
- tqdm

Install all packages using:

```bash
pip install -r requirements.txt
```

or

```bash
conda install --file requirements.txt
```

---

## Data Sources

### Hyperspectral Imagery

- Planet Labs Tanager-1 Surface Reflectance Product
- HDFEOS (HDF5) format
- CC BY 4.0 License

### Reference Labels

- JAXA High-Resolution Land-Use and Land-Cover (HRLULC)
- 10 m resolution product
- 50 m resolution product

---

## Applications

This framework can be adapted for:

- Hyperspectral land cover mapping
- Solar farm detection
- Greenhouse monitoring
- Agricultural mapping
- Environmental monitoring
- Remote sensing research
- Machine learning benchmarking

---

## Citation

If you use this repository in your research, please cite:

> Ramdani, F., et al. (2026). *Hyperspectral land cover classification using Tanager-1 imagery with multi-resolution training datasets*. (Manuscript in preparation)

---

## License

This repository is intended for academic and research purposes. Please acknowledge the original authors if the code or workflow is used in publications.

---

## Author

**Fatwa Ramdani**

Faculty of Humanities and Social Sciences
Graduate School of Humanities and Social Sciences
University of Tsukuba, Japan
