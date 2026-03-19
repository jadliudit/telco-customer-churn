# 📉 Telco Customer Churn Prediction

![Python](https://img.shields.io/badge/Python-3.12-blue)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-blue)
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
| scikit-learn | Logistic Regression, Random Forest, model evaluation |
| XGBoost | Gradient boosting model |
| SHAP | Model explainability and feature importance |
| PostgreSQL | Relational schema design and SQL analysis |
| SQLAlchemy / psycopg2 | Python-to-PostgreSQL ETL pipeline |
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
│   ├── 02_sql_analysis.ipynb         # PostgreSQL schema + analytical queries 🔄
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
- Loaded 7,043 rows × 38 columns from the main churn table using `encoding='latin-1'`
- Defined reusable file paths using `os.path.join()` for cross-platform compatibility
- Inspected all 38 column names and confirmed data types assigned by pandas
- Previewed the first 3 rows transposed for readability across 38 columns
- Identified 15 columns with missing values — all confirmed as **structural nulls**, not data errors:
  - `Churn Category` & `Churn Reason` (73.5%) — only populated for churned customers
  - Internet-related columns (21.7%) — customers with no internet service
  - `Offer` (55.0%) — no marketing offer accepted
  - Long distance columns (9.7%) — customers with no phone service
- Created a binary `Churn` column: `1` = Churned, `0` = Stayed or Joined
- Validated zip code join: **100% of 1,626 customer zip codes matched** the population table

**Key findings from Notebook 1:**

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

## 📊 Key Findings So Far

1. **26.5% churn rate** — roughly 1 in 4 customers left the company in Q2 2022
2. **Competitor is the #1 churn driver** — 45% of churned customers left for a better offer elsewhere
3. **Month-to-Month contracts are the highest risk group** — 51.3% of all customers are on this contract type with no lock-in
4. **Fiber Optic is the most popular internet type** — 43.1% of customers, typically higher monthly charges
5. **All missing values are structurally expected** — no data quality issues found in the raw dataset

---

## ▶️ How to Run This Project

**1. Clone the repository:**
```bash
git clone https://github.com/jadliudit/telco-customer-churn.git
cd telco-customer-churn
```

**2. Install required libraries:**
```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost shap sqlalchemy psycopg2 jupyter ipykernel
```

**3. Download the dataset:**

Go to [Maven Analytics Data Playground](https://mavenanalytics.io/data-playground/telecom-customer-churn) and download the three CSV files. Place them in `data/raw/`.

**4. Open and run the notebooks in order:**
```bash
jupyter notebook notebooks/01_data_loading.ipynb
```

---

## 📈 Project Status

| Phase | Notebook | Status |
|---|---|---|
| Data Loading & Inspection | `01_data_loading.ipynb` | ✅ Complete |
| SQL Analysis | `02_sql_analysis.ipynb` | 🔄 In Progress |
| Exploratory Data Analysis | `03_eda.ipynb` | ⏳ Upcoming |
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