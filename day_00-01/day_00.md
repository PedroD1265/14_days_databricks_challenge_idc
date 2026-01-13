# Day 0 — Setup & Data Loading (Prerequisites)

Goal: Set up Databricks and load the **E-Commerce Behavior Data** dataset from Kaggle (`mkechinov/ecommerce-behavior-data-from-multi-category-store`) so you're ready for Day 1.

---

## ✅ Day 0 Checklist

### Account & Workspace
- [x] Created a Databricks Community Edition account
- [x] Verified email and logged in
- [x] Created and started a cluster (default settings are fine)
- [x] Enabled auto-termination (recommended)

### Kaggle Access
- [x] Logged into Kaggle and generated an API Token (`kaggle.json`)
- [x] Saved my Kaggle `username` and `key`

### Data Download & Storage
- [x] Installed Kaggle CLI inside Databricks
- [x] Configured Kaggle credentials
- [x] Downloaded the dataset zip
- [x] Extracted `2019-Oct.csv` and `2019-Nov.csv`
- [x] Deleted the zip to save space

### Data Validation
- [x] Loaded `2019-Oct.csv` into a Spark DataFrame
- [x] Loaded `2019-Nov.csv` into a Spark DataFrame
- [x] Verified row counts
- [x] Verified schema has **9 columns**
- [x] Displayed a sample of 5 rows
