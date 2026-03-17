# 📊 Customer Churn Prediction System

## 📌 Overview

Customer churn is one of the biggest challenges faced by subscription-based businesses such as telecom, banking, and online services. Losing customers directly impacts revenue and growth.

This project presents a **Machine Learning-based Customer Churn Prediction System** that helps businesses identify whether a customer is likely to leave or stay based on their behavior.

The system is designed to be **simple, fast, and deployable**, with a user-friendly interface for real-time predictions.

---

## 🎯 Objective

* Predict whether a customer will **churn (leave)** or **stay**
* Help businesses take **proactive retention actions**
* Enable **data-driven decision making**

---

## 🧠 Key Features

* 🤖 Machine Learning Model (Random Forest)
* 📊 Predicts customer churn in real-time
* 🖥️ Interactive UI using Streamlit
* 📈 Clean and efficient feature selection
* 💡 Customer insights and suggestions
* ⚡ Lightweight and fast system

---

## 🏗️ Project Architecture

```text
Dataset → Data Preprocessing → Feature Selection → Model Training → Prediction → Streamlit UI
```

---

## 📊 Dataset

* **Telco Customer Churn Dataset**
* Contains customer details such as:

  * Tenure (how long customer stayed)
  * Monthly Charges
  * Total Charges
  * Customer behavior patterns

---

## ⚙️ Technologies Used

* 🐍 Python
* 📊 Pandas, NumPy
* 🤖 Scikit-learn (Random Forest)
* 🌐 Streamlit
* 💾 Joblib

---

## 🧪 How It Works

1. Load customer dataset
2. Clean and preprocess data
3. Select important features:

   * Tenure
   * Monthly Charges
   * Total Charges
4. Train Random Forest model
5. Deploy model using Streamlit
6. User inputs data → system predicts churn

---

## 🚀 Installation & Setup

### 1. Clone Repository

```bash
git clone https://github.com/your-username/customer-churn-prediction.git
cd customer-churn-prediction
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Run Application

```bash
streamlit run app.py
```

---

## 📸 Demo

* Input customer details
* Click "Predict"
* Get result: **Churn / No Churn**
* View insights in sidebar

---

## 👥 Team Collaboration (3 Members)

### 🔹 Member 1 – Problem & Data

* Defined problem statement
* Data collection and preprocessing
* Feature selection

### 🔹 Member 2 – Model Development

* Model selection (Random Forest)
* Training and evaluation
* Performance optimization

### 🔹 Member 3 – Application & UI

* Streamlit app development
* User interface design
* Integration of model with UI

---

## 🎤 Hackathon Pitch

> “We built a machine learning system that predicts customer churn using behavioral data.
> It helps businesses identify high-risk customers early and take proactive retention actions.”

---

## 🔮 Future Enhancements

* 📊 Add more features for higher accuracy
* 🌍 Real-time data integration
* 📱 Mobile app version
* ☁️ Cloud deployment
* 📈 Advanced models (XGBoost, Deep Learning)

---

## 📜 License

This project is developed for educational and hackathon purposes.

---

⭐ If you like this project, give it a star!
