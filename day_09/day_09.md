
# Day 09 — SQL Analytics & Dashboards

## Focus
- Analytical SQL queries
- Window functions (moving averages)
- Funnel analysis
- Customer segmentation
- Databricks SQL Dashboards

---

## What I Used (My Setup)
- **Catalog:** `ecommerce`
- **Schemas:** `silver`, `gold`
- **Core Tables:**
  - `ecommerce.silver.events`
  - `ecommerce.gold.category_funnel`
- **Compute:** Databricks SQL (Serverless – Community Edition)
- **Visualization:** Databricks SQL Dashboards
- **Notes:** All analytics queries were written in SQL and reused directly as dashboard datasets.

---

## Tasks Completed (Checklist)
- [x] Created analytical SQL queries for business metrics
- [x] Implemented a 7-day moving average using window functions
- [x] Built a conversion funnel aggregated by category
- [x] Created customer tiers based on purchase frequency and lifetime value
- [x] Added all queries as datasets in a Databricks SQL dashboard
- [x] Built visualizations for trends, funnels, and customer segments
- [x] Applied dashboard layout and visual customization

---

## Key Learnings
- **Window functions (`OVER`)** allow calculations across related rows without collapsing data.
- Moving averages are ideal for smoothing volatile time-series revenue.
- Funnel analysis should be built from **event-level data (Silver)** and then materialized into **Gold tables** for analytics.
- Gold tables represent **business-ready aggregates**, not raw events.
- Customer segmentation can be derived directly from transactional behavior using SQL.
- Databricks SQL Dashboards can reuse saved queries as datasets without duplication.
- **Scheduling and automatic refresh are not available in Community Edition** and require a paid Databricks plan.
