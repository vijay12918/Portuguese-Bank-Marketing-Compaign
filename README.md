# PRCP-1000: Portuguese Bank Marketing Campaign Prediction

## 📌 Project Overview

The dataset contains customer demographics, financial information, previous campaign interactions, and macroeconomic indicators. The goal is to build a **robust, business-oriented machine learning model** that helps the bank identify high-potential customers and optimize marketing efforts.

---

## 🎯 Business Objective

To help the bank marketing team:

* Identify customers who are **most likely to subscribe** to a term deposit
* Reduce campaign cost by **avoiding low-probability leads**
* Improve conversion rates using **data-driven targeting**

This is a **binary classification problem** with a highly imbalanced target variable.

---

## 🗂️ Dataset Information

* **Source**: Portuguese Bank Marketing Dataset (UCI ML Repository)
* **Records**: 41,188 customers
* **Features**: 21 (demographic, campaign-related, macroeconomic)
* **Target Variable**: `y`

  * `yes` → Subscribed to term deposit
  * `no` → Did not subscribe

### Target Distribution

* `No`: ~89%
* `Yes`: ~11%

> ⚠️ Due to class imbalance, accuracy alone is misleading. Metrics such as **F1-score, Recall, Precision, and ROC-AUC** are used.

---

## 🔍 Exploratory Data Analysis (EDA)

Key insights discovered during analysis:

### Customer Profile

* Customers aged **30–40** show the highest subscription rates
* **Higher education levels** (university degree, professional courses) lead to higher conversions
* **Single customers** are more responsive than married/divorced customers
* Customers **without personal loans or credit defaults** are more likely to subscribe

### Campaign Strategy

* **Cellular contact** is far more effective than telephone calls
* Best conversion months: **March, April, September, October**
* **Early contact attempts (1–3 calls)** perform best
* Repeated calls reduce success and increase customer irritation

### Previous Campaign Impact

* Customers who **subscribed previously** have a very high chance of subscribing again
* Warm leads outperform first-time contacts

### Economic Factors

* Customers are more likely to subscribe during:

  * Low interest rate periods
  * Higher consumer confidence
  * Economic uncertainty (preference for safe investments)

---

## 🧹 Data Preprocessing & Feature Engineering

### Key Steps

* Removed duplicate records
* Retained `unknown` values as a valid category
* **Removed data leakage** feature: `duration`
* Feature engineering:

  * `pdays` → converted to binary `previously_contacted`
  * `campaign` → capped into low (1–3) vs high (>3) contact groups

### Encoding & Scaling

* OneHotEncoding for categorical variables
* RobustScaler for `age` (outliers)
* StandardScaler for macroeconomic indicators

---

## 🤖 Model Building

Multiple models were trained using **Pipeline + ColumnTransformer**:

* Logistic Regression (baseline)
* Random Forest Classifier
* Gradient Boosting Classifier (tuned)
* XGBoost Classifier (tuned)

### Techniques Used

* Stratified Train-Test Split
* Stratified K-Fold Cross Validation
* Class imbalance handling (`class_weight`, `scale_pos_weight`)
* Threshold tuning to optimize F1-score

---

## 📊 Model Performance Comparison

| Model                     | Threshold | F1-score | Precision | Recall   | ROC-AUC  |
| ------------------------- | --------- | -------- | --------- | -------- | -------- |
| Logistic Regression       | 0.6       | 0.49     | 0.41      | 0.62     | 0.80     |
| Random Forest             | 0.3       | 0.42     | 0.38      | 0.46     | 0.76     |
| Gradient Boosting (Tuned) | 0.6       | 0.51     | 0.43      | 0.62     | 0.80     |
| **XGBoost (Tuned)**       | **0.7**   | **0.52** | **0.49**  | **0.57** | **0.80** |

✅ **Final Model Selected: XGBoost (Tuned)**

---

## 🏆 Final Model Justification

* Best balance between **precision and recall**
* Highest **F1-score** among all models
* Strong **ROC-AUC (~0.80)** indicating excellent class separation
* Minimizes false negatives → critical for marketing use cases

From a business standpoint, **recall is more important** than precision, as missing potential subscribers results in lost revenue.

---

## 🔑 Feature Importance (XGBoost)

Top contributing features:

* `euribor3m`
* `emp.var.rate`
* `nr.employed`
* `poutcome_success`
* `contact_cellular`
* Campaign intensity

### Insight

Campaign success is driven more by **economic conditions and prior engagement** than by demographics alone.

---

## 📁 Project Structure

```
PRCP-1000-PortugeseBank/
│
├── Data/
│   └── bank-additional-full.csv
│
├── notebooks/
│   └── Portugese_Bank_Analysis.ipynb
│
├── visualization/
│   ├── target_variable_analysis.png
│   ├── ROC-Curve_comparison.png
│   ├── xgb_feature_importance.png
│   └── ...
│
├── results/
│   ├── bank.csv
│   └── Model Comparison Table.csv
│
├── artifacts/
│   ├── xgb_final_model.pkl
│   └── preprocessor.pkl
│
├── README.md
└── requirements.txt
```

---

## 🛠️ Tech Stack

* **Python**
* **Pandas, NumPy**
* **Matplotlib, Seaborn**
* **Scikit-learn**
* **XGBoost**
* **Imbalanced-learn**

---

## 🚀 How to Run the Project

```bash
pip install -r requirements.txt
```

```bash
jupyter notebook
```

---

## 📈 Future Improvements

* Deploy model using Flask / FastAPI
* Integrate Power BI dashboard for business users
* Apply SHAP for advanced model explainability
* Automate monthly retraining with fresh campaign data

---

## 👤 Author

**Vijay Kumar Madari**
Data Analytics & Machine Learning Enthusiast

---

## ⭐ If you found this project useful

Give it a ⭐ on GitHub and feel free to fork or contribute!
