# 🚨 Fraudulent Transactions Detection using Machine Learning

This project focuses on detecting **fraudulent financial transactions** using machine learning techniques. It leverages a realistic, time-based transactional dataset simulating industrial-scale money movement. The aim is to predict the **probability of fraud** for any given transaction while addressing class imbalance, model performance, and interpretability.

---

## 📊 Dataset Description

The dataset simulates 30 days of financial activity with transaction types such as transfers, payments, and cash-outs. Below is a summary of the dataset fields:

| Column Name        | Description                                                                                         |
|--------------------|-----------------------------------------------------------------------------------------------------|
| `step`             | Time step (1 step = 1 hour) — total of 744 steps (30 days)                                           |
| `type`             | Type of transaction: `CASH-IN`, `CASH-OUT`, `DEBIT`, `PAYMENT`, `TRANSFER`                         |
| `amount`           | Transaction amount in local currency                                                                |
| `nameOrig`         | Originator of the transaction                                                                        |
| `oldbalanceOrg`    | Initial balance of originator before transaction                                                    |
| `newbalanceOrig`   | New balance of originator after transaction                                                         |
| `nameDest`         | Recipient of the transaction                                                                         |
| `oldbalanceDest`   | Initial balance of recipient before transaction                                                     |
| `newbalanceDest`   | New balance of recipient after transaction                                                          |
| `isFraud`          | `1` if transaction is fraudulent, else `0`                                                           |
| `isFlaggedFraud`   | `1` if flagged due to suspicious activity (e.g. > 200,000 in a single transfer), else `0`            |

---

## 🧠 Model Objective

To accurately classify **fraudulent transactions** in a highly **imbalanced dataset**, where only ~0.1% of transactions are fraudulent.

---

## 📐 Evaluation Metric: Precision-Recall AUC (AUPRC)

Due to the extreme class imbalance, we chose the **Area Under the Precision-Recall Curve (AUPRC)** over traditional ROC-AUC:

| Metric    | Reason                                                                 |
|-----------|------------------------------------------------------------------------|
| `AUPRC`   | Focuses on performance of the minority (fraudulent) class              |
| `ROC-AUC` | Misleading with imbalanced classes — can report high scores unjustly   |

**Why AUPRC?**  
A high AUPRC score indicates strong ability to detect fraud without being biased by the overwhelming number of normal transactions.

---

## 🧪 Approach & Techniques

### 🔍 Data Imbalance Handling

- Tried both **undersampling** and **SMOTE-based oversampling**
- Final model trained on **original skewed data** with **class-weighting**

### ⚙️ Model Selection

| Method                | Result                                                              |
|------------------------|----------------------------------------------------------------------|
| Logistic Regression    | Poor performance on skewed data                                      |
| SMOTE + Random Forest  | Improved recall, but overfit in some cases                           |
| **XGBoost (Best)**     | Excellent performance; handles skew, missing values, and large data  |

> ✅ **XGBoost** with class weighting and tree ensembles gave the most consistent performance.

---

## 📈 Results

| Metric        | Value      | Interpretation                                                                 |
|---------------|------------|---------------------------------------------------------------------------------|
| AUPRC         | **0.98**   | Indicates excellent performance on the minority (fraudulent) class              |
| Precision     | High       | Very few false positives (incorrect fraud alerts)                              |
| Recall        | High       | Successfully detects most actual fraudulent transactions                      |

---

## 🛡️ Conclusion & Infrastructure Recommendations

### ✅ **Conclusion**
- The model performs exceptionally well in detecting fraud, achieving an **AUPRC score of 0.9785**.
- This confirms its strong ability to correctly identify fraudulent activity while minimizing false alarms.

### 🔐 **Fraud Prevention Recommendations**
- Pay special attention to **`TRANSFER`** and **`CASH_OUT`** transaction types — these are highly associated with fraud.
- Continuously monitor transaction patterns to detect unusual behavior.
- Use automated model retraining and performance monitoring to a
