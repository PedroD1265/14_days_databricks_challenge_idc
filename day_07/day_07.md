# Day 07 — Workflows & Job Orchestration

## Focus
- Databricks Jobs vs notebooks
- Multi-task workflows (Bronze → Silver → Gold)
- Parameters (widgets) & scheduling
- Dependencies + basic error handling mindset

---

## What I Used (My Setup)
- **Pipeline goal:** Orchestrate the Medallion pipeline (Bronze → Silver → Gold)
- **Compute:** Serverless
- **Job name:** `medallion_bronze_silver_gold_pipeline`
- **Notebook tasks (workspace paths):**
  - `day_07_bronze_layer`
  - `day_07_silver_layer`
  - `day_07_gold_layer`
- **Delta paths used:**
  - Bronze: `/delta/bronze/events`
  - Silver: `/delta/silver/events`
  - Gold: `/delta/gold/products`

---

## Tasks Completed (Checklist)
- [x] Added parameter widgets to notebooks (source path + layer outputs)
- [x] Created a multi-task Job workflow: **Bronze → Silver → Gold**
- [x] Configured task dependencies (Silver depends on Bronze, Gold depends on Silver)
- [x] Validated Job execution using Serverless compute (and prepared for scheduling)

---

## Key Learnings
- A **Notebook** is the unit of execution, while a **Job/Workflow** is how you run notebooks reliably (repeatable + schedulable).
- Parameters let one workflow run the same code with different inputs (paths, dates, layers).
- Dependencies enforce pipeline order and reduce manual steps.
- Orchestration is what turns notebooks into a production-like pipeline.

---

## Evidence
- Job / Workflow: `medallion_bronze_silver_gold_pipeline`
- Notebook tasks:
  - `day_07_bronze_layer`
  - `day_07_silver_layer`
  - `day_07_gold_layer`
- Outputs:
  - Bronze Delta: `/delta/bronze/events`
  - Silver Delta: `/delta/silver/events`
  - Gold Delta: `/delta/gold/products`

