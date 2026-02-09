# Wafer Fault Prediction

A machine learning project to predict faulty wafers in semiconductor manufacturing using sensor data analysis.

## 📋 Project Overview

In electronics, a **wafer** is a thin slice of semiconductor (crystalline silicon) used for fabricating integrated circuits and manufacturing solar cells. This project aims to automate the detection of faulty wafers using machine learning, eliminating the need for manual inspection and reducing operational costs.

### Problem Statement

Wafers are located at remote locations in bulk and contain hundreds of sensors. Currently, manual inspection is required to identify faulty wafers, which involves:
- Stopping all nearby wafers during inspection
- Opening wafers from scratch to investigate
- High cost and time wastage if suspicions are false negatives
- Disruption of the entire production process

### Solution

This project implements a machine learning pipeline that analyzes data from wafer sensors to determine whether a wafer is faulty, thereby:
- Eliminating manual labor costs
- Reducing production downtime
- Improving accuracy of fault detection
- Enabling real-time monitoring

## 🔧 Technologies Used

- **Python 3.x**
- **Data Analysis:** Pandas, NumPy
- **Visualization:** Matplotlib, Seaborn
- **Machine Learning:** Scikit-learn, XGBoost
- **Preprocessing:** KNNImputer, RobustScaler
- **Resampling:** imbalanced-learn (SMOTETomek)
- **Clustering:** KMeans, KneeLocator

## 📊 Dataset

- **Source:** Wafer sensor data (`wafer_23012020_041211.csv`)
- **Initial Dataset Size:** 100 samples × 592 features
- **Target Variable:** Good/Bad (binary classification)
- **Class Distribution:** 
  - Good wafers (-1): 74 samples (92.5%)
  - Bad wafers (1): 6 samples (7.5%)
  - Highly imbalanced dataset
- **Characteristics:** 
  - Missing values: 3.85% of total cells
  - 4 features with >70% missing values (Sensor-158, 159, 293, 294)
  - Multiple features with zero standard deviation

## 🚀 Methodology

### 1. Data Preprocessing
- **Missing Data Handling:** 3.85% missing values imputed using KNN Imputer (n_neighbors=3)
- **Feature Engineering:**
  - Removed 4 features with >70% missing values
  - Dropped features with zero standard deviation
  - Reduced from 592 to **465 contributing features**
- **Scaling:** RobustScaler for handling outliers
- **Train-Test Split:** 80-20 split (80 training samples, 20 test samples initially)

### 2. Data Transformation Pipeline
```python
Pipeline([
    ('Imputer', KNNImputer(n_neighbors=3)),
    ('Scaler', RobustScaler())
])
```

### 3. Clustering Analysis
- Applied KMeans clustering using Elbow method (k-means++, range 1-10)
- Found optimal **3 clusters** based on WCSS analysis
- Cluster distribution highly unbalanced:
  - Cluster 1: 62 samples (77.5%)
  - Cluster 0: 17 samples (21.25%)
  - Cluster 2: 1 sample (1.25%)
- **Decision:** Proceed without clustering due to severe imbalance

### 4. Class Imbalancing
- **Method:** SMOTETomek (combination of SMOTE oversampling and Tomek links undersampling)
- **Before Resampling:** 80 samples (74 good, 6 bad)
- **After Resampling:** 296 samples total
  - Good wafers (-1): 148 samples (50%)
  - Bad wafers (1): 148 samples (50%)
- **Result:** Perfectly balanced dataset achieved

### 5. Model Selection & Training

**Training Set:** 98 samples × 464 features  
**Test Set:** 50 samples × 464 features

Evaluated multiple machine learning models using 10-fold cross-validation:

| Model | Kernel/Type | Train ROC-AUC (Mean ± Std) | Test ROC-AUC |
|-------|-------------|----------------------------|---------------|
| **Random Forest Classifier** | - | **1.000 ± 0.000** | **1.000** |
| **SVC** | **Linear** | **1.000 ± 0.000** | **0.940** |
| SVC | RBF | 0.996 ± 0.012 | 0.680 |
| XGBoost Classifier | Binary Logistic | Not shown | Not shown |

### 6. Model Evaluation
- **Metric:** ROC-AUC Score
- **Validation Strategy:** Cross-validation (10-fold for training, 5-fold for testing)

## 📁 Project Structure

```
Credit-Card-Default-Prediction-main/
│
├── in1__exploratory analysis.ipynb    # Main analysis notebook
├── wafer_23012020_041211.csv          # Dataset (not included in repo)
├── test.csv                            # Sample test data
└── README.md                           # Project documentation
```

## 🔍 Key Insights

1. **Feature Distribution:** Many features exhibit significant outliers and skewness, requiring robust scaling
2. **Missing Data:** 3.85% missing values across features, handled through KNN imputation
3. **Class Imbalance:** Severely imbalanced (92.5% vs 7.5%), successfully addressed using SMOTETomek to achieve 50-50 balance
4. **Feature Selection:** Eliminated 127 non-contributing features (zero std dev and high missing values), reducing from 592 to 465 features
5. **Clustering:** Dataset not suitable for clustering-based approach - 3 clusters identified but with extreme imbalance (62-17-1 distribution)
6. **Model Performance:** Random Forest and SVC (Linear) achieved perfect training scores (ROC-AUC = 1.0)

## 📈 Results

### Best Performing Models

1. **Random Forest Classifier** (Recommended)
   - Training ROC-AUC: 1.000 (perfect classification)
   - Test ROC-AUC: 1.000 (perfect generalization)
   - Most robust model with excellent performance

2. **SVC with Linear Kernel**
   - Training ROC-AUC: 1.000
   - Test ROC-AUC: 0.940
   - Strong performance with good generalization

3. **SVC with RBF Kernel**
   - Training ROC-AUC: 0.996 ± 0.012
   - Test ROC-AUC: 0.680
   - Shows signs of overfitting

### Key Achievements
- ✅ Successfully handled 3.85% missing data using KNN imputation
- ✅ Reduced feature space from 592 to 465 features (21.5% reduction)
- ✅ Achieved perfect class balance (148-148) using SMOTETomek
- ✅ Random Forest achieved **100% accuracy** on test set
- ✅ Scalable preprocessing pipeline ready for production

**Note:** This project demonstrates end-to-end machine learning workflow including data preprocessing, feature engineering, model selection, and evaluation for industrial IoT applications.
