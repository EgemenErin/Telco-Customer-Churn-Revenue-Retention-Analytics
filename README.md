# 📉 Customer Churn & Revenue Analytics

> Identifying **$139K in at-risk monthly revenue** using Python & Power BI.

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-ETL-150458?logo=pandas&logoColor=white)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

---

## 📌 Project Overview

A full end-to-end analytics project on a **7,000+ row telecom customer dataset**. The goal was to go beyond a surface-level churn rate and quantify exactly how much recurring revenue is walking out the door, and *why*.

The pipeline covers data ingestion, cleaning, transformation, and a two-page interactive Power BI dashboard surfacing actionable retention insights.

**Key result:** A baseline **26.54% churn rate** translates to **$139,131 in at-risk monthly revenue**, with Month-to-Month contracts and Electronic Check payments as the primary drivers.

---

## 🗂️ Repository Structure

```
├── data/
│   ├── Telco_Churn_RAW.csv          # Original dataset (7,043 rows, 21 columns)
│   └── Telco_Churn_CLEANED.csv      # Processed dataset with engineered features
├── data_cleaning.ipynb              # Python ETL pipeline (Pandas)
├── Customer_Churn_Revenue_Analytics.pdf  # Project presentation / report
└── README.md
```

---

## ⚙️ ETL Pipeline — `data_cleaning.ipynb`

The notebook handles the full transformation from raw to analysis-ready data.

### Steps

| Step | Description |
|---|---|
| **Type Casting** | `TotalCharges` coerced to numeric (was stored as string due to blank entries) |
| **Null Unmasking** | Whitespace-only strings replaced with `NaN` via regex before null check |
| **Null Imputation** | Remaining `TotalCharges` nulls filled with `0` (new customers with no charges) |
| **Target Binarization** | `Churn` column mapped `Yes → 1`, `No → 0` for DAX and ML compatibility |
| **Feature Engineering** | `Tenure_Cohort` created by binning `tenure` into 6-month lifecycle buckets |

### Tenure Cohort Bins

```python
bins   = [0, 12, 24, 36, 48, 60, 72]
labels = ['0-12 Months', '13-24 Months', '25-36 Months',
          '37-48 Months', '49-60 Months', '61-72 Months']
df['Tenure_Cohort'] = pd.cut(df['tenure'], bins=bins, labels=labels, include_lowest=True)
```

---

## 📊 Dataset Schema

**21 original columns → 22 after feature engineering**

| Column | Type | Description |
|---|---|---|
| `customerID` | string | Unique customer identifier |
| `gender` | categorical | Male / Female |
| `SeniorCitizen` | binary | 1 = Senior, 0 = Not |
| `Partner` / `Dependents` | binary | Household status |
| `tenure` | integer | Months as a customer |
| `PhoneService` / `MultipleLines` | categorical | Phone plan details |
| `InternetService` | categorical | DSL / Fiber optic / No |
| `OnlineSecurity`, `TechSupport`, etc. | categorical | Add-on services |
| `Contract` | categorical | Month-to-month / One year / Two year |
| `PaperlessBilling` | binary | Yes / No |
| `PaymentMethod` | categorical | Electronic check, Credit card, etc. |
| `MonthlyCharges` | float | Monthly billing amount |
| `TotalCharges` | float | Lifetime charges |
| `Churn` | binary (engineered) | 1 = Churned, 0 = Retained |
| `Tenure_Cohort` | categorical (engineered) | Lifecycle segment |

---

## 📈 Key Findings

### Executive Summary (Power BI — Page 1)

| KPI | Value |
|---|---|
| Total Customers | 7,043 |
| Churn Rate | **26.54%** |
| At-Risk Monthly Revenue | **$139,131** |

- **Churn is front-loaded.** The 0-12 month cohort churns at nearly 50% — far exceeding any other tenure group. Customers who survive past 24 months stabilize dramatically.
- **Month-to-Month contracts account for 86.86%** (~$120.85K) of all at-risk revenue. One-year and two-year contracts combined represent less than 14%.

### Risk Factors (Power BI — Page 2)

- **Electronic Check** is the single highest-churn payment method, spiking well above Mailed check, Bank transfer, and Credit card. A targeted nudge toward automatic payments could have an outsized impact.
- **Customers without Tech Support** churn at nearly double the rate of those with it — making bundled Tech Support a strong retention lever.
- **Fiber Optic users churn more than DSL users**, suggesting a pricing or reliability perception problem with the premium internet tier.

### Recommended Actions

| Segment | Action |
|---|---|
| Month-to-Month customers | Offer a 10% discount to upgrade to Annual, include free Tech Support for 12 months |
| Electronic Check payers | Incentivize switch to automatic credit card payment |
| 0-12 Month cohort | Proactive onboarding check-in at month 3 and month 6 |
| Fiber Optic customers | Investigate pricing perception; consider loyalty credits |

---

## 🛠️ Tech Stack

- **Python 3** — Pandas, NumPy, Matplotlib
- **Jupyter Notebook** — ETL and exploratory analysis
- **Power BI** — Dashboard, DAX measures, at-risk revenue quantification
- **Excel** — Intermediate data review

---

## 🚀 Getting Started

```bash
git clone https://github.com/EgemenErin/telco-churn-analytics.git
cd telco-churn-analytics
pip install pandas matplotlib numpy
jupyter notebook data_cleaning.ipynb
```

---

## 🔗 Links

- 🌐 [Portfolio — egemenerin.com](https://www.egemenerin.com)
- 📊 [Interactive Power BI Dashboard](https://app.powerbi.com/groups/me/reports/18a3646f-871e-48c8-98bf-324ee5a3a75b/3398295873e992db23e3?experience=power-bi) 
- 📧 egemeneriin@protonmail.com

---

## 👤 Author

**Egemen Erin** — Data Analyst  
*December 2024*
