# PRCP-1000 – Portuguese Bank Marketing Prediction

## 📌 Project Overview

The project follows a complete **end-to-end data science workflow**, including Exploratory Data Analysis (EDA), feature engineering, model building, evaluation, threshold tuning, and business recommendations.

---

## 🎯 Problem Statement

Banks invest significant resources in telemarketing campaigns. However, only a small fraction of contacted customers subscribe to term deposits. Efficiently identifying customers who are most likely to subscribe can:

* Reduce marketing costs
* Improve conversion rates
* Optimize campaign strategies

---

## 🎯 Objective

To build a **predictive classification model** that accurately identifies customers who are likely to subscribe to a term deposit (`y = yes`).

---


## 🔍 Exploratory Data Analysis (EDA)

### Key Insights

* Customers aged **30–40** have the highest subscription rates
* Higher education levels correlate with higher subscription probability
* **Cellular contact** is significantly more effective than telephone
* Early contact attempts (1–3 calls) have the highest success rate
* **Call duration strongly correlates with subscription** (data leakage risk)
* Previous campaign success is a strong predictor of future subscriptions
* Macroeconomic indicators (employment rate, Euribor rate, consumer confidence) strongly influence customer decisions

> ⚠️ **Data Leakage Note:** The `duration` feature was excluded from modeling because it is only known after the call ends.

---

## ⚙️ Data Preprocessing & Feature Engineering

* Removed duplicate records
* Retained `unknown` values as valid categorical levels
* Encoded categorical variables using **OneHotEncoder**
* Scaled numerical variables using **StandardScaler** and **RobustScaler**
* Feature engineering steps:

  * Converted `pdays` into a binary feature: `previously_contacted`
  * Capped campaign calls into:

    * `0`: Low contact (1–3 calls)
    * `1`: High contact (>3 calls)
* Dropped leakage feature `duration`

---

## 🤖 Models Trained

The following models were trained using pipelines and evaluated using **Stratified K-Fold Cross Validation**:

* Logistic Regression (baseline)
* Random Forest Classifier
* Gradient Boosting Classifier (tuned)
* XGBoost Classifier (tuned)

### Evaluation Metrics

Given the imbalanced dataset, the following metrics were used:

* Precision
* Recall
* F1-score
* ROC-AUC

Threshold tuning was applied to optimize business outcomes.

---

## 📊 Model Comparison

| Model                     | Threshold | F1-score | Precision | Recall   | ROC-AUC  |
| ------------------------- | --------- | -------- | --------- | -------- | -------- |
| Logistic Regression       | 0.6       | 0.49     | 0.41      | 0.62     | 0.80     |
| Random Forest             | 0.3       | 0.42     | 0.38      | 0.47     | 0.76     |
| Gradient Boosting (Tuned) | 0.6       | 0.51     | 0.43      | 0.62     | 0.80     |
| **XGBoost (Tuned)**       | **0.7**   | **0.52** | **0.49**  | **0.57** | **0.80** |

---

## 🏆 Final Model Selection

**XGBoost (Tuned)** was selected as the final model because it:

* Achieved the **highest F1-score**
* Provided a strong balance between precision and recall
* Handled class imbalance effectively using `scale_pos_weight`
* Captured complex non-linear relationships in the data

The probability threshold was optimized to **0.7** to balance customer acquisition and marketing cost.

---

## 📌 Business Recommendations

* Focus campaigns on customers aged **30–40** with higher education
* Prioritize **cellular-based marketing** over telephone calls
* Limit contact attempts to **1–3 calls** per customer
* Re-target customers who subscribed in previous campaigns
* Align marketing efforts with favorable economic conditions (low interest rates, higher consumer confidence)

---

## 🚀 Deployment Considerations

* The final trained pipeline is **deployment-ready**
* Data leakage features are removed
* Threshold tuning allows flexible business alignment
* The model can be serialized using `pickle` for real-time inference

---

## 🛠️ Technologies Used

* Python
* Pandas, NumPy
* Matplotlib, Seaborn
* Scikit-learn
* XGBoost
* Imbalanced-learn

---

## 📁 Project Structure

```
PRCP-1000-PortugeseBank/
│
├── data/
├── notebooks/
│   └── EDA_and_Modeling.ipynb
├── outputs/
│   └── model_comparison_table.csv
├── visualizations/
│   └── *.png
├── models/
│   └── xgb_final_model.pkl
└── README.md
```

---


## 👤 Author

**Madari Vijay Kumar**

---

⭐ *If you find this project useful, feel free to star the repository!*
