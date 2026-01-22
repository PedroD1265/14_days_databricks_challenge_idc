# Day 13 — Model Comparison & Feature Engineering

## Focus
- Train and compare multiple regression models (baseline → tree-based)
- Track experiments in **MLflow** (params, metrics, artifacts)
- Choose a “best” model based on metrics + practicality

---

## What I Used (My Setup)
- **Source table:** `ecommerce.gold.products`
- **Features used (X):** `views`, `revenue`
- **Target (y):** `purchases`
- **Split:** 80/20 (`test_size=0.2`, `random_state=42`)
- **Experiment (MLflow):** `/Users/pedelvicl@gmail.com/mlflow_day13`
- **Compute:** Databricks (Serverless notebook)

---

## Tasks Completed (Checklist)
- [x] Trained **3 models** (Linear Regression, Decision Tree, Random Forest)
- [x] Logged **parameters** (model type, features, split, hyperparameters)
- [x] Logged **metrics** (R², RMSE, MAE)
- [x] Logged **model artifacts** in MLflow (one per run)
- [x] Compared runs and selected a best candidate for this dataset

---

## Results (What I Got)
From the notebook output (3 MLflow runs):

- **Linear Regression**
  - R² ≈ **0.7672**
  - RMSE ≈ **73.8645**
  - MAE ≈ **4.9868**

- **Decision Tree (max_depth=5)**
  - R² ≈ **0.7786**  *(best)*
  - RMSE ≈ **72.0230** *(best / lowest)*
  - MAE ≈ **2.4405**

- **Random Forest**
  - R² ≈ **0.7043**
  - RMSE ≈ **83.2356**
  - MAE ≈ **1.9592** *(best / lowest)*

**Interpretation**
- If your priority is overall fit (R²) + typical error (RMSE), **Decision Tree** looks best here.
- Random Forest showed **lower MAE** but worse **R²/RMSE**, which can happen when a model predicts many cases “closer” on average but fails badly on some larger values (outliers), hurting RMSE and R².

---

## Key Learnings
- **MLflow** makes comparisons easy: each model run stores params + metrics + artifacts in one place.
- **Use multiple metrics** (R² + RMSE + MAE). One metric alone can mislead.
- Tree models can outperform linear models when relationships are **non-linear**.
- The MLflow warning about **integer columns / missing values** is common:
  - It warns that if missing values appear later, integer columns could be promoted to float, causing schema mismatch.
  - Best practice: ensure a realistic `input_example` (including nulls if they can exist) or cast numeric inputs to float before logging.

---

## Evidence
- Notebook: `day_13_Model Comparison & Feature Engineering`
- MLflow experiment: `/Users/pedelvicl@gmail.com/mlflow_day13`
- Runs created (3):
  - `linear_model`
  - `decision_tree_model`
  - `random_forest_model`
- Metrics logged: `r2`, `rmse`, `mae`
- Model artifacts logged under: `model/`
