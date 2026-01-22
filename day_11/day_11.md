# Day 11 — Statistical Analysis & ML Prep

## Focus
- Descriptive statistics on e-commerce event data
- Hypothesis testing idea: **weekday vs weekend conversion**
- Simple correlation checks (exploratory, not causal)
- Feature engineering with Spark (time + behavioral features)

---

## What I Used (My Setup)
- **Catalog / Tables:**
  - Source: `ecommerce.silver.events`
  - Output (features): `ecommerce.silver.events_features`
- **Key columns used:** `event_time`, `event_date`, `event_type`, `price`, `user_id`, `product_id`, `category_code`
- **Compute:** Databricks Notebook (Serverless)
- **Notes:** Worked in Spark using DataFrames + Window functions. Used a lightweight permutation-test style check (no external stats libs required).

---

## Tasks Completed (Checklist)
- [x] Calculated descriptive statistics for `price` (distribution + sanity checks)
- [x] Built a weekday vs weekend comparison using `is_weekend`
- [x] Estimated conversion rates (purchases/views) by weekend/weekday
- [x] Explored correlations (event-level and aggregated checks)
- [x] Engineered ML-ready features and saved them as a table

---

## Key Learnings
- `summary()`/`describe()` gives fast distribution signals (min/max/avg/std, plus quantiles if using `summary()`).
- Weekend logic in Spark: `dayofweek()` returns **1=Sunday** and **7=Saturday**, so weekend is `IN (1,7)`.
- `silver.events` is event-level data, so “conversion rate” must be **derived via aggregation** (e.g., purchases/views).
- Correlation is a **screening tool**, not proof: strong correlations can come from confounding or data imbalance.
- Window functions let you create user-level time features (e.g., time since first event) without leaving Spark.
- Feature engineering must avoid **leakage** (don’t use “future” behavior to predict the past).

---

## Evidence
- Validation steps:
  - `ecommerce.silver.events` schema + sample preview
  - Weekend vs weekday funnel counts + conversion
- Correlation checks:
  - `corr(price, is_purchase)` (event level)
  - `corr(avg_price, product_conv)` (aggregated by product)
- Output table created:
  - `ecommerce.silver.events_features` with:
    - `hour`, `day_of_week`, `is_weekend`, `price_log`, `time_since_first_event_sec`

