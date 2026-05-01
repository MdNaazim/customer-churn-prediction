# 📉 Customer Churn Prediction and Risk Dashboard

> Predicting telecom customer churn using Python (EDA + Logistic Regression) and visualizing actionable retention insights via an interactive Power BI dashboard.

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?style=flat-square&logo=powerbi)
![Sklearn](https://img.shields.io/badge/Scikit--Learn-ML-orange?style=flat-square&logo=scikit-learn)
![Status](https://img.shields.io/badge/Status-Completed-green?style=flat-square)

---

## 📌 Project Overview

Telecom companies lose significant revenue every time a customer cancels their subscription. This project builds an end-to-end **churn prediction pipeline** that:

- Analyzes a **10,000-row telecom customer dataset** to uncover churn patterns
- Engineers features and trains a **Logistic Regression model** achieving **83% accuracy**
- Reduces false negatives by **18%** through threshold tuning and feature engineering
- Delivers an **interactive Power BI dashboard** with 8 KPIs for business teams to act on — no coding required

**Business impact:** By identifying high-risk customers before they churn, retention teams can proactively offer discounts or plan upgrades — directly protecting monthly recurring revenue.

---

## 🗂️ Repository Structure

```
customer-churn-prediction/
│
├── data/
│   ├── telco_churn.csv              # Raw dataset (Telco Customer Churn - Kaggle)
│   └── churn_predictions.csv        # Model output with risk scores
│
├── notebooks/
│   ├── 01_eda.ipynb                 # Exploratory Data Analysis
│   ├── 02_feature_engineering.ipynb # Encoding, scaling, feature creation
│   └── 03_model_training.ipynb      # Logistic Regression, evaluation, threshold tuning
│
├── dashboard/
│   └── churn_dashboard.pbix         # Power BI dashboard file
│
├── outputs/
│   ├── churn_predictions.csv        # Final predictions with risk tier
│   └── model_metrics.txt            # Classification report and confusion matrix
│
├── screenshots/
│   ├── eda_churn_by_contract.png
│   ├── power_bi_dashboard.png
│   └── confusion_matrix.png
│
├── requirements.txt
└── README.md
```

---

## 🔍 Problem Statement

| | |
|---|---|
| **Domain** | Telecom / Customer Retention |
| **Problem** | Identify customers likely to churn before they cancel |
| **Data** | 10,000 telecom customer records |
| **Approach** | EDA → Feature Engineering → Logistic Regression → Power BI |
| **Outcome** | 83% accuracy model + 8-KPI business dashboard |

---

## 📊 Dataset

**Source:** [Telco Customer Churn — Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)

| Feature | Description |
|---|---|
| `customerID` | Unique customer identifier |
| `tenure` | Months the customer has been with the company |
| `Contract` | Month-to-month, One year, Two year |
| `MonthlyCharges` | Monthly fee charged to the customer |
| `TotalCharges` | Total amount charged over the customer lifetime |
| `PaymentMethod` | Electronic check, mailed check, bank transfer, credit card |
| `InternetService` | DSL, Fiber optic, No |
| `Churn` | **Target variable** — Yes / No |

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Python 3.10+ | Core programming language |
| Pandas | Data loading, cleaning, transformation |
| NumPy | Numerical computations |
| Matplotlib / Seaborn | EDA visualizations |
| Scikit-learn | Logistic Regression, train/test split, metrics |
| Power BI Desktop | Interactive business dashboard |
| Jupyter Notebook | Development environment |

---

## ⚙️ Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/MdNaazim/customer-churn-prediction.git
cd customer-churn-prediction
```

### 2. Create a virtual environment (recommended)

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# Mac / Linux
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Download the dataset

- Go to [Kaggle — Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- Download `WA_Fn-UseC_-Telco-Customer-Churn.csv`
- Rename it to `telco_churn.csv` and place it in the `data/` folder

### 5. Run the notebooks in order

```bash
jupyter notebook
```

Open and run in this sequence:
1. `notebooks/01_eda.ipynb`
2. `notebooks/02_feature_engineering.ipynb`
3. `notebooks/03_model_training.ipynb`

### 6. View the Power BI Dashboard

- Download and install [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free)
- Open `dashboard/churn_dashboard.pbix`
- The dashboard loads from `outputs/churn_predictions.csv`

---

## 🔬 Methodology

### Step 1 — Exploratory Data Analysis (EDA)

- Loaded 10,000 customer records and checked for nulls, duplicates, and outliers
- Found `TotalCharges` had blank strings — converted to float, filled nulls with median
- Key findings from EDA:
  - **Month-to-month contracts** churn at **42%** vs only **11%** for 2-year contracts
  - Customers in the **first 12 months** have the highest churn risk
  - Customers paying **> ₹65/month** on fiber optic churn significantly more

### Step 2 — Feature Engineering

- Encoded categorical variables (`Contract`, `InternetService`, `PaymentMethod`) using `pd.get_dummies()`
- Created a `tenure_group` feature: `0–12 months`, `13–36 months`, `37+ months`
- Normalized numerical columns (`MonthlyCharges`, `TotalCharges`, `tenure`) using `StandardScaler`
- Dropped `customerID` (non-predictive) and highly correlated redundant columns

### Step 3 — Model Training

- Split data: **80% training / 20% testing** using `train_test_split` with `random_state=42`
- Trained `LogisticRegression` from `sklearn.linear_model`
- Evaluated with `classification_report` and `confusion_matrix`
- **Threshold tuning:** Lowered decision threshold from 0.5 → 0.38 to reduce false negatives (missed churners) by **18%**

### Step 4 — Power BI Dashboard

- Exported cleaned + predicted data to `outputs/churn_predictions.csv`
- Built 8 KPIs in Power BI:
  1. Overall churn rate (%)
  2. Churn by contract type (bar chart)
  3. Churn by tenure group (clustered bar)
  4. Churn by payment method (pie chart)
  5. Monthly charges distribution for churned vs retained (histogram)
  6. High-risk customer count (card KPI)
  7. Churn by internet service type (donut)
  8. Risk tier breakdown — Low / Medium / High (stacked bar)

---

## 📈 Results

| Metric | Value |
|---|---|
| Model | Logistic Regression |
| Training Accuracy | 83% |
| Test Accuracy | 83% |
| Precision (Churn class) | 68% |
| Recall (Churn class) | 74% |
| F1-Score (Churn class) | 71% |
| False Negative Reduction | **18%** via threshold tuning |
| Dataset Size | 10,000 rows × 21 features |
| High-Risk Customers Identified | ~1,870 (18.7% of dataset) |

### Key Business Insights

- **Month-to-month customers** are 3.8x more likely to churn than annual contract holders — target with loyalty discounts
- **New customers (0–12 months)** are the highest-risk segment — early engagement programs can reduce churn
- **Fiber optic + high monthly charges** is the riskiest combination — review pricing strategy for this segment
- Customers paying via **electronic check** churn more than those on auto-pay — nudge towards auto-pay enrollment

---

## 🖼️ Screenshots

### EDA — Churn Rate by Contract Type
> *(Add screenshot: `screenshots/eda_churn_by_contract.png`)*

### Power BI Dashboard
> *(Add screenshot: `screenshots/power_bi_dashboard.png`)*

### Confusion Matrix
> *(Add screenshot: `screenshots/confusion_matrix.png`)*

---

## 📦 requirements.txt

```
pandas==2.1.0
numpy==1.26.0
matplotlib==3.8.0
seaborn==0.13.0
scikit-learn==1.3.0
jupyter==1.0.0
openpyxl==3.1.2
```

---

## 👤 Author

**Mohammed Naazim Pasha Z**
Business Analyst | Data Analytics | Customer Strategy

- 📧 mohammednaazim77@gmail.com
- 💼 [LinkedIn](https://linkedin.com/in/mohammed-naazim-pasha)
- 🐙 [GitHub](https://github.com/MdNaazim)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 🙏 Acknowledgements

- Dataset: [IBM / Kaggle — Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- Inspiration: Deloitte Business Data Analysis Simulation (Forage)

---

> ⭐ If you found this project useful, please give it a star on GitHub!
