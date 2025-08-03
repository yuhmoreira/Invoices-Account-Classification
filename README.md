# 🧾 Accounting Classification - ML Pipeline for Supplier Invoices

This project implements a machine learning pipeline for **automated classification of supplier purchases into accounting accounts**. It leverages text and numerical features extracted from simulated invoices to build, evaluate, and improve a logistic regression classifier.

> 🔍 **Goal:** Predict the correct `Account_Number` from invoice data (e.g. item description, supplier name, item value).

---

## 📊 Dataset

The dataset used is available on [Kaggle](https://www.kaggle.com/datasets/moreirarogerson/accounting-classification-suppliers-purchases/):

- `invoices_classification.xlsx`: Includes supplier codes, item descriptions, tax values, amounts, and accounting labels.
- **Target:** `Account_Number` (multiclass classification)
- **Split:** Already divided into `"Training"` and `"Test"` via the `Dataset` column.

---

## 🧠 Model Pipeline

We use **Logistic Regression** as a baseline model with careful feature engineering and text preprocessing:

### Features Used:

| Feature                 | Type        | Description |
|------------------------|-------------|-------------|
| `Input_Text`           | Text        | Combination of item description and supplier name |
| `Item_Value`           | Numeric     | Raw monetary value |
| `Log_Item_Value`       | Numeric     | Log-transformed value |
| `Item_Quantity`        | Numeric     | Quantity of items |
| `Taxes_Credit_%`       | Numeric     | Percentual of taxes with credit |
| `Log_Taxes_Credit_Amount` | Numeric | Log of tax credit amount |
| `Value_Category`       | Categorical | Binned value ranges (Very Low to Very High) |

### Model Improvements:

| Pipeline               | Accuracy | Macro F1 | Notes |
|------------------------|----------|----------|-------|
| Text only              | 92%      | 0.83     | CountVectorizer on `Input_Text` |
| Text + Value features  | 94%      | 0.91     | Added `Item_Value` & `Log_Item_Value` |
| All engineered features | **98%** | **0.97** | With `GridSearchCV` tuning (C, max_features) |

---

## 📈 Visualizations

- Class distribution plots
- Heatmaps showing contingency between suppliers and accounts
- Accuracy per account
- Average item value by account
- Confusion matrix

---

## 🧰 Technologies

- Python 3.10+
- Pandas / NumPy / Seaborn / Matplotlib
- Scikit-learn
- NLTK
- Jupyter Notebook

---

## 📁 Project Structure

📦 Accounting Classification/
  ├── notebooks/
  
  │ └── Accounts_Classication.ipynb ← Full pipeline notebook
  
  ├── data/
  │ └── Accounting Classification Suppliers Purchases ← Dataset (Kaggle)
  
  ├── flowchart/
  
  │ └── invoices_classification.md ← Visual diagram (Mermaid)
  
  ├── README.md ← This file

---

## 🔁 Reproducibility

To run this project:

1. Clone the repo:
   ```bash
   git clone https://github.com/your-username/accounting-classification.git
   cd accounting-classification

---

   📌 Highlights
  ✅ Achieves 98% accuracy
  
  ✅ Feature engineering aligned with real-world accounting logic
  
  ✅ Clean pipeline using scikit-learn best practices
  
  ✅ Visual analysis and class-level error tracking
  
  ✅ Diagram in Mermaid for documentation



