# 📉 E-commerce Customer Churn Analysis

An end-to-end data cleaning and preparation project on a 50,000-customer e-commerce churn dataset. Raw data is cleaned and feature-engineered in **Python (pandas)**, then loaded into **MySQL** for SQL-based analysis.

---

## 📌 Project Overview

Customer churn directly hurts revenue. This project prepares a large churn dataset so it can be analysed to answer questions like:

- Which customer segments and countries churn the most?
- What are the top reasons customers leave?
- How much revenue is lost to churn vs. recovered?
- Do satisfaction, support tickets, or engagement relate to churn?

## 📂 Dataset

- **Source:** [E-commerce Customer Churn 2026 (Kaggle)](https://www.kaggle.com/datasets/datascikhan/e-commerce-customer-churn-2026)
- **Size:** 50,000 rows × 48 columns (raw)
- **Churn rate:** ~41.3% of customers churned (20,653 churned / 29,347 active)
- **Segments:** Consumer, Premium, Small Business, Enterprise

**Key column groups**

| Group | Example columns |
|---|---|
| Customer profile | `customer_segment`, `customer_country`, `customer_city`, `customer_age_months` |
| Churn details | `is_churned`, `churn_date`, `churn_reason`, `churn_category`, `churn_probability` |
| Behaviour | `total_spend_usd`, `num_purchases`, `days_since_last_purchase`, `engagement_level` |
| Support & satisfaction | `satisfaction_score`, `support_tickets`, `feedback_score`, `returns_count` |
| Marketing | `marketing_emails_sent/opened/clicked`, `marketing_conversions`, `referral_count` |
| Financial | `customer_lifetime_value_usd`, `customer_retention_cost_usd`, `recovery_revenue_usd`, `churn_revenue_impact_usd` |

## 🛠️ Tech Stack

- **Python 3.13** – pandas, NumPy
- **Jupyter Notebook** – analysis workflow
- **MySQL** – storage and querying
- **SQLAlchemy + PyMySQL** – Python → MySQL connection

## 🔄 Workflow

1. **Load** the raw CSV into pandas
2. **Inspect** – shape, dtypes, missing values, duplicates
3. **Clean**
   - Converted `churn_date` to datetime
   - Coerced financial/score columns to numeric
   - Standardised text columns (lowercase, trimmed whitespace)
   - Filled structural gaps: `subscription_type` → `Unknown`, `prevention_method` → `None`, `social_media_engagement` → `0`
   - Confirmed **0 duplicate rows**
4. **Feature engineering**
   - `is_churned_numeric` – binary churn indicator
   - `churn_month` – for seasonality/trend analysis
   - `net_churn_loss` – `churn_revenue_impact_usd − recovery_revenue_usd`
5. **Data readiness audit** – custom function checking duplicates, missing values, infinite values, and zero-variance columns
6. **Drop zero-variance columns** (`dataset_year`, `churn_year`)
7. **Export** cleaned data to CSV / Excel and **load into MySQL** (`customer_churn` table, 50,000 rows × 50 columns)

## 📁 Repository Structure

```
├── churn_analysis.ipynb          # Cleaning, feature engineering, MySQL load
├── cleaned_customer_churn.xlsx   # Cleaned dataset
├── README.md
└── requirements.txt              # (optional) dependencies
```

## 🔎 Key Observations So Far

- Dataset is clean of duplicates; the only missing values are structural (e.g., `churn_date` is empty for active customers).
- Class balance is reasonable (≈41% churn / 59% retained), so no heavy resampling is needed for modelling.
- `Consumer` is the largest segment (22,320 customers), followed by `Premium` (12,565).
- Most customers fall in the `excellent` health category (36,874).
- Note: the dataset is synthetic/simulated, so findings illustrate method rather than real business results.

## 🗺️ Next Steps

- [ ] SQL analysis: churn rate by segment, country, and reason
- [ ] Revenue impact and recovery analysis
- [ ] Exploratory data analysis with visualisations
- [ ] Dashboard (Power BI / Tableau)
- [ ] Churn prediction model

## 👤 Author

Jatin – MCA (AI & Data Science) student, aspiring Data / Business Analyst
