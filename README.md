# 🔄 Customer Churn Prediction
### CADES Hackathon | SRM Institute of Science & Technology

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![ML](https://img.shields.io/badge/ML-Scikit--Learn%20%7C%20XGBoost-orange)
![Platform](https://img.shields.io/badge/Platform-Google%20Colab-yellow)

## 📌 Problem Statement
Customer churn is a major challenge for telecom companies. This project builds
a machine learning system that predicts whether a customer is likely to churn
based on usage patterns, subscription history, and account information.

## 🎯 Objectives
- Predict customers likely to discontinue services
- Identify key factors influencing churn
- Categorize customers into Low / Medium / High risk groups

## 📁 Project Structure
```
customer-churn-prediction/
├── notebooks/
│   ├── 01_EDA.ipynb
│   ├── 02_preprocessing.ipynb
│   ├── 03_model_training.ipynb
│   ├── 04_evaluation.ipynb
│   └── 05_final_pipeline.ipynb  ← Demo notebook
├── models/
│   └── best_model.pkl
├── reports/
│   ├── confusion_matrix.png
│   ├── roc_curve.png
│   ├── feature_importance.png
│   └── risk_categorization.png
└── requirements.txt
```

## 📊 Dataset
**Telco Customer Churn Dataset** — [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- 7,043 customers | 21 features

## 🤖 ML Pipeline
| Step | Description |
|------|-------------|
| EDA | Explored churn patterns across all features |
| Preprocessing | Handled nulls, encoding, scaling |
| Feature Engineering | Tenure groups, average monthly spend |
| Class Balancing | SMOTE to handle 26% churn imbalance |
| Models Trained | Logistic Regression, Random Forest, XGBoost |
| Evaluation | ROC-AUC, Confusion Matrix, SHAP analysis |

## 📈 Results
| Metric | Score |
|--------|-------|
| ROC-AUC | ~0.85+ |
| Risk Groups | Low / Medium / High |

## 🚀 How to Run
1. Open `notebooks/05_final_pipeline.ipynb` in Google Colab
2. Mount Google Drive
3. Run all cells in order

## 👤 Author
**Shashank Kodali** — [@shashank-kodali](https://github.com/shashank-kodali)
