# Day 06 — Medallion Architecture

## Focus
- Bronze (raw) → Silver (cleaned) → Gold (aggregated)
- Best practices per layer
- Simple incremental-ready patterns (without orchestration yet)

---

## What I Used (My Setup)
- **Dataset / Main path:** `/Volumes/workspace/ecommerce/ecommerce_data/2019-Oct.csv` (e-commerce events)
- **Delta storage paths:**
  - Bronze: `/delta/bronze/events`
  - Silver: `/delta/silver/events`
  - Gold: `/delta/gold/products`
- **Compute:** Databricks (Serverless / notebook compute)
- **Notes:** Built medallion layers using PySpark + Delta writes (no Jobs/Workflows yet).

---

## Tasks Completed (Checklist)
- [x] Designed a 3-layer architecture (Bronze / Silver / Gold)
- [x] Built **Bronze** layer (raw ingestion + ingestion timestamp)
- [x] Built **Silver** layer (cleaning, validation, dedup, derived columns)
- [x] Built **Gold** layer (business aggregates)

---

## Key Learnings
- Medallion architecture is a practical way to structure pipelines: **raw → cleaned → curated aggregates**.
- Bronze is about *immutability* (raw copy + metadata like ingestion timestamp).
- Silver is where data quality happens: filters, deduplication, derived features (e.g., `event_date`, `price_tier`).
- Gold is optimized for analytics: product performance metrics (views, purchases, revenue, conversion rate).

---

## Evidence
- Notebook: `DB_Day6.ipynb`
- Outputs created:
  - Delta Bronze: `/delta/bronze/events`
  - Delta Silver: `/delta/silver/events`
  - Delta Gold: `/delta/gold/products`
