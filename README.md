# 🔄 Customer Churn Prediction
### CADES Hackathon — Problem Statement 4 | SRM Institute of Science & Technology

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square)
![ML](https://img.shields.io/badge/ML-Scikit--Learn%20%7C%20XGBoost-orange?style=flat-square)
![Platform](https://img.shields.io/badge/Platform-Google%20Colab-yellow?style=flat-square)
![Status](https://img.shields.io/badge/Status-Complete-green?style=flat-square)

---

## 📌 Problem Statement

Customer churn is a major challenge for businesses such as telecom companies and subscription platforms. Predicting which customers are likely to leave allows companies to intervene with retention strategies.

This project builds a machine learning system that predicts whether a customer is likely to churn based on **usage patterns**, **subscription history**, and **account information**.

---

## 🎯 Objectives

- Predict customers likely to discontinue services
- Identify key factors influencing churn
- Support customer retention strategies by categorizing customers into risk groups

---

## 📊 Dataset

**Telco Customer Churn Dataset** — [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)

| Property | Value |
|---|---|
| Source | IBM Sample Dataset via Kaggle |
| Total Customers | 7,043 |
| Total Features | 21 |
| Target Column | `Churn` (Yes / No) |
| Churn Rate | ~26.5% |
| Missing Values | 11 rows in `TotalCharges` |

### Feature Overview

| Category | Features |
|---|---|
| Demographics | gender, SeniorCitizen, Partner, Dependents |
| Account | tenure, Contract, PaperlessBilling, PaymentMethod |
| Charges | MonthlyCharges, TotalCharges |
| Services | PhoneService, MultipleLines, InternetService, OnlineSecurity, OnlineBackup, DeviceProtection, TechSupport, StreamingTV, StreamingMovies |

---

## 🗂️ Project Structure
```
customer-churn-prediction/
│
├── 📁 notebooks/
│   ├── 01_EDA.ipynb                  ← Exploratory Data Analysis
│   ├── 02_preprocessing.ipynb        ← Data Cleaning & Feature Engineering
│   ├── 03_model_training.ipynb       ← Model Training & Selection
│   ├── 04_evaluation.ipynb           ← Model Evaluation & Metrics
│   └── 05_final_pipeline.ipynb       ← End-to-End Demo Notebook
│
├── 📁 models/
│   └── best_model.pkl                ← Saved best performing model
│
├── 📁 reports/
│   ├── confusion_matrix.png
│   ├── roc_curve.png
│   ├── feature_importance.png
│   ├── risk_categorization.png
│   └── model_comparison.png
│
└── requirements.txt
```

---

## ⚙️ ML Pipeline

### Step 1 — Exploratory Data Analysis (`01_EDA.ipynb`)

Performed comprehensive analysis of the dataset to understand patterns and relationships:

- Analyzed churn rate distribution — dataset is imbalanced at ~26.5% churn
- Identified key patterns:
  - Month-to-month contract customers churn the most (~43%)
  - Customers with Fiber optic internet churn more than DSL customers
  - New customers (low tenure) have significantly higher churn risk
  - Higher monthly charges correlate strongly with churn
- Visualized numerical feature distributions split by churn status
- Generated correlation heatmap for numerical features

---

### Step 2 — Data Preprocessing (`02_preprocessing.ipynb`)

Cleaned and transformed raw data into model-ready format:

**Cleaning:**
- Dropped `customerID` — not useful for prediction
- Converted `TotalCharges` from string to numeric (contained whitespace)
- Filled 11 missing `TotalCharges` values with column median
- Encoded target variable: `Yes → 1`, `No → 0`

**Encoding:**
- Binary columns (Yes/No) → Label Encoding (0/1)
- Multi-class columns (Contract, InternetService, PaymentMethod, etc.) → One-Hot Encoding via `pd.get_dummies(drop_first=True)`

**Feature Engineering:**

| New Feature | Formula | Reason |
|---|---|---|
| `AvgMonthlySpend` | `TotalCharges / (tenure + 1)` | More informative than raw total |
| `TenureGroup` | Binned into 4 groups (0-1yr, 1-2yr, 2-4yr, 4+yr) | Captures tenure stage effect |

**Train/Test Split:**
- 80% training / 20% testing
- `stratify=y` used to maintain churn ratio in both splits

**Scaling:**
- `StandardScaler` applied to numerical columns
- Scaler **fit only on training data** to prevent data leakage
- Saved as `scaler.pkl` for use during inference

**Saved outputs:**
```
data/processed/
├── X_train.csv
├── X_test.csv
├── y_train.csv
├── y_test.csv
├── scaler.pkl
└── feature_columns.json    ← exact column order used during training
```

---

### Step 3 — Model Training (`03_model_training.ipynb`)

**Class Imbalance Handling:**

The dataset has only ~26.5% churn cases. Training directly on this would result in a biased model that always predicts "No Churn". SMOTE (Synthetic Minority Oversampling Technique) was used to balance the training set:
```
Before SMOTE → Stayed: 4,107  |  Churned: 1,484
After SMOTE  → Stayed: 4,107  |  Churned: 4,107
```

**Models Trained:**

| Model | Description |
|---|---|
| Logistic Regression | Linear model, draws a decision boundary |
| Random Forest | Ensemble of 100 decision trees, majority vote |
| XGBoost | Gradient boosted trees, each correcting previous errors |

All models trained on SMOTE-balanced training data and evaluated on the original (unbalanced) test set.

**Model Selection:**
Best model automatically selected based on highest **ROC-AUC score**.

---

### Step 4 — Evaluation (`04_evaluation.ipynb`)

**Metrics Used:**

| Metric | Description |
|---|---|
| ROC-AUC Score | Primary metric — measures ability to separate churners from non-churners |
| Confusion Matrix | Shows TP, TN, FP, FN breakdown |
| Precision | Of predicted churners, how many actually churned |
| Recall | Of actual churners, how many were correctly identified |
| F1-Score | Harmonic mean of Precision and Recall |

**SHAP Analysis:**
SHAP (SHapley Additive exPlanations) used to explain model predictions and identify the most influential features. Automatically selects `TreeExplainer` for tree-based models or `LinearExplainer` for Logistic Regression.

**Risk Categorization Logic:**

| Churn Probability | Risk Category | Recommended Action |
|---|---|---|
| ≥ 60% | 🔴 High Risk | Immediate retention offer |
| 30% – 59% | 🟡 Medium Risk | Proactive check-in |
| < 30% | 🟢 Low Risk | No action needed |

---

### Step 5 — Final Pipeline (`05_final_pipeline.ipynb`)

Clean, end-to-end demonstration notebook for presentation purposes. Covers:

1. Dataset overview and key statistics
2. Key insight charts (contract type, tenure, monthly charges)
3. Model performance (confusion matrix + ROC curve)
4. Risk group distribution across all test customers
5. Live single customer prediction with probability gauge

---

## 📈 Expected Output

For every customer the system produces:

| Output | Type | Example |
|---|---|---|
| Churn Prediction | Binary | Yes / No |
| Churn Probability Score | Float (0–100%) | 73.4% |
| Risk Category | Categorical | High Risk |

---

## 🚀 How to Run

### Prerequisites
- Google Account (for Colab + Drive)
- Dataset downloaded from [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)

### Setup

**1. Create folder structure in Google Drive:**
```
My Drive/
└── Churn_Hackathon/
    └── data/
        └── raw/
            └── WA_Fn-UseC_-Telco-Customer-Churn.csv
```

**2. Run notebooks in order:**

| Order | Notebook | What it produces |
|---|---|---|
| 1st | `01_EDA.ipynb` | Charts and insights |
| 2nd | `02_preprocessing.ipynb` | Cleaned data splits + scaler |
| 3rd | `03_model_training.ipynb` | `best_model.pkl` |
| 4th | `04_evaluation.ipynb` | Performance metrics + SHAP |
| 5th | `05_final_pipeline.ipynb` | Full demo |

> ⚠️ Each notebook depends on outputs from the previous one. Always run in order.

**3. Open any notebook in Google Colab:**
- Go to [colab.research.google.com](https://colab.research.google.com)
- File → Open → GitHub → paste repo URL

---

## 📦 Dependencies
```
pandas==2.0.3
numpy==1.24.3
matplotlib==3.7.2
seaborn==0.12.2
scikit-learn==1.3.0
xgboost==1.7.6
imbalanced-learn==0.11.0
shap==0.42.1
```

Install all:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost imbalanced-learn shap
```
---

## 🏫 About

Built for **CADES Hackathon — Problem Statement 4**
School of Computing | SRM Institute of Science & Technology
