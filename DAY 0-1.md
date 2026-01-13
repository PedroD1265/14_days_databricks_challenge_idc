# Day 0 — Setup & Data Loading (Prerequisites)

Goal: Set up Databricks and load the **E-Commerce Behavior Data** dataset from Kaggle (`mkechinov/ecommerce-behavior-data-from-multi-category-store`) so you're ready for Day 1.

---

## ✅ Day 0 Checklist

### Account & Workspace
- [/] Created a Databricks Community Edition account
- [ ] Verified email and logged in
- [ ] Created and started a cluster (default settings are fine)
- [ ] Enabled auto-termination (recommended)

### Kaggle Access
- [ ] Logged into Kaggle and generated an API Token (`kaggle.json`)
- [ ] Saved my Kaggle `username` and `key`

### Data Download & Storage
- [ ] Installed Kaggle CLI inside Databricks
- [ ] Configured Kaggle credentials
- [ ] Downloaded the dataset zip
- [ ] Extracted `2019-Oct.csv` and `2019-Nov.csv`
- [ ] Deleted the zip to save space

### Data Validation
- [ ] Loaded `2019-Oct.csv` into a Spark DataFrame
- [ ] Loaded `2019-Nov.csv` into a Spark DataFrame
- [ ] Verified row counts
- [ ] Verified schema has **9 columns**
- [ ] Displayed a sample of 5 rows
