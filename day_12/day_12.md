# Day 12 — MLflow Basics

## Focus
- MLflow fundamentals: **Tracking**, **Artifacts/Models**, and how runs are organized in **Experiments**
- Logging **parameters**, **metrics**, and a **model artifact** from a simple regression baseline
- Using the **MLflow UI** to inspect and compare runs

---

## What I Used (My Setup)
- **Source table:** `ecommerce.gold.products`
- **Target variable:** `purchases`
- **Features used:** `views`, `revenue`
- **Train/test split:** `test_size = 0.2`, `random_state = 42`
- **Model:** `sklearn.linear_model.LinearRegression`
- **Compute:** Databricks (Serverless) + Python notebook
- **Notes:** Data was converted to Pandas (`toPandas()`) to train a scikit-learn model, then logged to MLflow.

---

## Tasks Completed (Checklist)
- [x] Trained a simple regression model (Linear Regression) to predict `purchases`
- [x] Logged run metadata to MLflow:
  - [x] **Params:** model type, features, test split, random state
  - [x] **Metrics:** `r2`, `rmse`, `mae`
- [x] Logged the trained model as an MLflow **artifact**
- [x] Added `input_example` (and improved model logging vs the first version)
- [x] Validated results in the MLflow UI (experiment + run details)

---

## Key Learnings
- **MLflow Tracking** stores each training attempt as a **run** inside an **experiment** (great for reproducibility and comparisons).
- Logging **params** (what you tried) + **metrics** (how it performed) makes it easy to compare models over time.
- Logging the model as an **artifact** lets you:
  - Download the serialized model
  - Reuse it in inference later
  - (In paid tiers) register it in a **Model Registry**
- Warning observed:
  - **“Inferred schema contains integer columns… may cause schema enforcement issues with missing values.”**
  - Meaning: if later you score data where a column that was inferred as integer contains missing values, it may be coerced to float and mismatch the stored schema. A safe habit is to keep dtypes consistent (or infer/log a signature from realistic data if missing values are expected).

---

## Results (This Run)
- **R²:** `0.7672`
- **RMSE:** `73.8645`
- **MAE:** `4.9868`

---

## Evidence
- **MLflow experiment:** `/Users/pedelvicl@gmail.com/mlflow_day12`
- **Run name:** `linreg_purchases_v1`
- **What to check in the MLflow UI (Artifacts tab):**
  - `model/` (the logged model artifact)
- **What to check in the MLflow UI (Overview tab):**
  - Params: `features`, `test_size`, `random_state`, `model_type`
  - Metrics: `r2`, `rmse`, `mae`
