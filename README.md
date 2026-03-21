# 📉 Telco Customer Churn Prediction

![Python](https://img.shields.io/badge/Python-3.12-blue)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-17.9-blue)
![Power BI](https://img.shields.io/badge/PowerBI-Dashboard-yellow)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-orange)
![XGBoost](https://img.shields.io/badge/XGBoost-Boosting-red)
![Status](https://img.shields.io/badge/Status-In%20Progress-orange)

---

## 📌 Project Overview

This is an end-to-end machine learning project that predicts customer churn for a fictional California-based telecommunications company using the Maven Analytics Telecom Customer Churn dataset. The project covers the complete data analytics and ML workflow — from raw data ingestion and SQL analysis, through to predictive modelling with explainability and an interactive Power BI dashboard.

The goal is to identify customers who are likely to churn, understand the key drivers behind their decision to leave, and present actionable retention insights in a business-ready format.

This project was built as part of a personal portfolio to demonstrate practical skills in Python, SQL, machine learning, model explainability, and business intelligence reporting — targeting graduate analyst roles at Big 4 consulting firms.

---

## 🎯 Project Objectives

- Load and validate a multi-table telecom dataset and design a relational PostgreSQL schema
- Perform exploratory data analysis to uncover churn patterns across customer demographics, services, and billing
- Engineer features and handle class imbalance for machine learning
- Train and compare three ML models: Logistic Regression, Random Forest, and XGBoost
- Explain model predictions using SHAP values for business stakeholder communication
- Build a three-page interactive Power BI dashboard linking ML output to business insight

---

## 📂 Dataset

- **Source:** [Maven Analytics — Telecom Customer Churn](https://mavenanalytics.io/data-playground/telecom-customer-churn)
- **Period:** Q2 2022, California, USA
- **Type:** Multi-table (relational structure)

| File | Description | Rows | Columns |
|---|---|---|---|
| `telecom_customer_churn.csv` | Main customer table — demographics, services, billing, churn outcome | 7,043 | 38 |
| `telecom_zipcode_population.csv` | California zip code population data for geographic enrichment | 1,671 | 2 |
| `telecom_data_dictionary.csv` | Column definitions and descriptions | 40 | 3 |

**Join Key:** `Zip Code` — 100% coverage confirmed (all 1,626 unique customer zip codes match the population table)

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Python (pandas, numpy) | Data loading, cleaning, and manipulation |
| psycopg2 / SQLAlchemy | Python-to-PostgreSQL ETL pipeline |
| PostgreSQL 17.9 | Relational schema design and SQL analysis |
| scikit-learn | Logistic Regression, Random Forest, model evaluation |
| XGBoost | Gradient boosting model |
| SHAP | Model explainability and feature importance |
| Power BI | Interactive three-page dashboard |
| GitHub | Version control and project hosting |
| VS Code | Development environment |

---

## 📁 Project Structure

```
telco-customer-churn/
│
├── data/
│   ├── raw/                          # Original Maven Analytics CSV files
│   │   ├── telecom_customer_churn.csv
│   │   ├── telecom_zipcode_population.csv
│   │   └── telecom_data_dictionary.csv
│   └── processed/                    # Cleaned datasets ready for modelling
│
├── notebooks/
│   ├── 01_data_loading.ipynb         # Data loading, inspection & validation ✅
│   ├── 02_sql_analysis.ipynb         # PostgreSQL schema + 10 analytical queries ✅
│   ├── 03_eda.ipynb                  # Exploratory data analysis 🔄
│   ├── 04_feature_engineering.ipynb  # Encoding, scaling, SMOTE 🔄
│   └── 05_modelling.ipynb            # LR, RF, XGBoost + SHAP 🔄
│
├── sql/                              # SQL scripts for PostgreSQL
├── powerbi/                          # Power BI dashboard (.pbix)
├── reports/figures/                  # Saved charts and plots from notebooks
├── screenshots/                      # Power BI dashboard screenshots
├── .gitignore
├── LICENSE
└── README.md
```

---

## 🔍 Project Workflow

### Notebook 1 — Data Loading & Inspection ✅

Loaded all three CSV files into pandas DataFrames and performed a thorough inspection of the dataset before any cleaning or modelling.

**Key steps:**
- Loaded 7,043 rows × 38 columns using `encoding='latin-1'`
- Defined reusable file paths using `os.path.join()` for cross-platform compatibility
- Inspected all 38 column names and confirmed data types assigned by pandas
- Identified 15 columns with missing values — all confirmed as structural nulls, not errors
- Created a binary `Churn` column: `1` = Churned, `0` = Stayed or Joined
- Validated zip code join: 100% of 1,626 customer zip codes matched the population table

**Key findings:**

| Check | Result |
|---|---|
| Rows loaded | 7,043 customers × 38 columns |
| Missing values | 15 columns — all structural, not errors |
| Target variable | 26.5% churn rate — mild class imbalance |
| Top churn reason | Competitor (45% of churned customers) |
| Highest risk group | Month-to-Month contract customers (51.3%) |
| Zip code join | 100% coverage — JOIN is safe |
| Anomaly flagged | Negative Monthly Charge (-$10) — likely billing credit |

---

### Notebook 2 — SQL Analysis ✅

Designed a relational PostgreSQL schema, loaded both tables via Python using SQLAlchemy, and wrote 10 analytical queries to uncover churn patterns across key business dimensions.

**Key steps:**
- Connected Python to PostgreSQL using SQLAlchemy connection string
- Cleaned all column names to snake_case for SQL compatibility
- Loaded `customer_churn` (7,043 rows) and `zipcode_population` (1,671 rows) into PostgreSQL
- Wrote 10 business-focused SQL queries using CTEs, window functions, CASE WHEN, COALESCE, HAVING, and JOIN

**SQL concepts used:**
`COUNT`, `SUM`, `ROUND`, `GROUP BY`, `ORDER BY`, `WHERE`, `HAVING`, `CASE WHEN`, `COALESCE`, `OVER()` window functions, `JOIN`, `LIMIT`, `::numeric` casting, `IS NOT NULL`

**Key findings from 10 queries:**

| Query | Business Question | Key Finding |
|---|---|---|
| 1 | Overall churn rate | 26.5% baseline — 1 in 4 customers churned |
| 2 | Churn by contract type | Month-to-Month 45.8% vs Two Year 2.5% — 18x difference |
| 3 | Churn by internet type | Fiber Optic highest at 40.7% despite being premium service |
| 4 | Churn by tenure | First 12 months critical — 47.4% churn rate |
| 5 | Churn by payment method | Credit Card lowest at 14.5% vs Mailed Check at 36.9% |
| 6 | Top churn reasons | Competitor advantages drive 44%+ of specific churn reasons |
| 7 | Churn by offer type | Offer A best (6.7%), Offer E worst (52.9%) |
| 8 | Revenue lost by city | San Diego $385k revenue lost — highest of any city |
| 9 | Churn by population size | Larger areas churn slightly more (30.7% vs 24.5%) |
| 10 | High value customers | Every top 10 high-value churned customer was on Fiber Optic |

---

## 📊 Key Business Insights So Far

1. **26.5% overall churn rate** — roughly 1 in 4 customers left in Q2 2022
2. **Contract type is the strongest churn signal** — Month-to-Month customers churn at 18x the rate of Two Year customers
3. **First 12 months is the critical retention window** — 47.4% of new customers churn within the first year
4. **Fiber Optic is a premium service with a retention problem** — 40.7% churn rate and all top high-value churned customers were on Fiber Optic
5. **Competitor advantages drive 44%+ of churn** — better devices, better offers, faster speeds
6. **Offer A is the most effective retention tool** — 6.7% churn vs 52.9% for Offer E
7. **San Diego is the highest revenue loss city** — $385,446 in lost revenue from 185 churned customers
8. **Credit Card payment correlates with loyalty** — 14.5% churn vs 36.9% for Mailed Check customers

---

## ▶️ How to Run This Project

**1. Clone the repository:**
```bash
git clone https://github.com/jadliudit/telco-customer-churn.git
cd telco-customer-churn
```

**2. Install required libraries:**
```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost shap sqlalchemy psycopg2-binary jupyter ipykernel
```

**3. Download the dataset:**

Go to [Maven Analytics Data Playground](https://mavenanalytics.io/data-playground/telecom-customer-churn) and download the three CSV files. Place them in `data/raw/`.

**4. Set up PostgreSQL:**
- Install PostgreSQL 17.9 from [postgresql.org](https://www.postgresql.org/download/)
- Create a database called `telecom_churn`
- Update the connection string in `02_sql_analysis.ipynb` with your credentials

**5. Run the notebooks in order:**
```bash
jupyter notebook notebooks/01_data_loading.ipynb
```

---

## 📈 Project Status

| Phase | Notebook | Status |
|---|---|---|
| Data Loading & Inspection | `01_data_loading.ipynb` | ✅ Complete |
| SQL Analysis | `02_sql_analysis.ipynb` | ✅ Complete |
| Exploratory Data Analysis | `03_eda.ipynb` | 🔄 In Progress |
| Feature Engineering | `04_feature_engineering.ipynb` | ⏳ Upcoming |
| ML Modelling & SHAP | `05_modelling.ipynb` | ⏳ Upcoming |
| Power BI Dashboard | `telco_churn_dashboard.pbix` | ⏳ Upcoming |

---

## 👤 Author

**Udit Jadli**

- 📧 jadliudit@gmail.com
- 💼 [LinkedIn](https://www.linkedin.com/in/jadliudit97/)
- 🐙 [GitHub](https://github.com/jadliudit)
- 🌐 [Portfolio](https://portfolio-preview-62.emergent.host)