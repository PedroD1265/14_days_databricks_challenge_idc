# Day 08 — Unity Catalog Governance

## Focus
- Catalog → Schema → Table hierarchy
- Managed tables vs existing Delta data
- Access control with GRANT
- Controlled data access using views

---

## What I Used (My Setup)
- **Catalog:** `ecommerce`
- **Schemas:** `bronze`, `silver`, `gold`
- **Existing Delta data (from Day 6):**
  - `/Volumes/workspace/ecommerce/ecommerce_data/medallion/bronze/events`
  - `/Volumes/workspace/ecommerce/ecommerce_data/medallion/silver/events`
  - `/Volumes/workspace/ecommerce/ecommerce_data/medallion/gold/products`
- **Compute:** Databricks SQL + Notebook environment
- **Notes:** Unity Catalog managed tables created using CTAS (`CREATE TABLE AS SELECT`) from existing Delta data.

---

## Tasks Completed (Checklist)
- [x] Created and validated Catalog & Schemas (`ecommerce.bronze`, `ecommerce.silver`, `ecommerce.gold`)
- [x] Registered existing Delta data as **Unity Catalog managed tables**
- [x] Applied table-level permissions using `GRANT`
- [x] Created a controlled analytics view in the Gold layer

---

## Key Learnings
- Unity Catalog introduces a **governance layer on top of Delta Lake**, independent of storage paths.
- UC does **not allow `dbfs:/` or `/Volumes/...` paths** in `LOCATION` clauses.
- Existing Delta data must be registered using **CTAS** to become UC-managed tables.
- Permissions (`GRANT`) work only with **valid principals** (users or groups).
- Views are the recommended way to expose **curated, controlled data** to consumers.

---

## Evidence
- Tables registered in Unity Catalog:
  - `ecommerce.bronze.events`
  - `ecommerce.silver.events`
  - `ecommerce.gold.products`
- View created:
  - `ecommerce.gold.top_products`
- Validation queries:
  - `SHOW TABLES IN ecommerce.bronze;`
  - `SHOW TABLES IN ecommerce.silver;`
  - `SHOW TABLES IN ecommerce.gold;`
  - `SELECT COUNT(*) FROM ecommerce.gold.products;`
  - `SELECT * FROM ecommerce.gold.top_products LIMIT 10;`

