# Day 10 — Performance Optimization

## Focus
- Query execution plans (understanding what Spark/Delta will actually do)
- Partitioning strategy (reduce data scanned via partition pruning)
- OPTIMIZE + ZORDER (file compaction + data skipping)
- Quick benchmarking (before vs after)

---

## What I Used (My Setup)
- **Catalog / Schemas:** `ecommerce` (`bronze`, `silver`, `gold`)
- **Source table:** `ecommerce.silver.events` (Unity Catalog managed table)
- **New optimized tables created:**
  - `ecommerce.silver.events_part` (partitioned by `event_date`)
  - `ecommerce.silver.events_part2` (partitioned by `event_date`, `event_type`)
- **Optimization applied:**
  - `OPTIMIZE ecommerce.silver.events_part ZORDER BY (user_id, product_id)`
- **Compute:** Databricks Serverless / notebook environment
- **Notes:** Table caching via `cache()` is **not supported** on Serverless compute (persist table limitation).

---

## Tasks Completed (Checklist)
- [x] Inspected query plans using `explain(True)`
- [x] Built partitioned Delta tables to improve pruning on common filters
- [x] Applied `OPTIMIZE` + `ZORDER` for compaction and better data skipping
- [x] Ran a small benchmark to compare timings
- [x] Tested partition pruning with a date-filter query plan
- [x] Attempted caching and documented why it fails on Serverless

---

## Key Learnings
- `explain(True)` is the fastest way to validate **filters, projections, and joins** are pushed down as expected.
- Partitioning helps when your queries frequently filter by the partition columns (e.g., `event_date`, `event_type`).
- `OPTIMIZE` compacts many small files into fewer larger files (better scan efficiency).
- `ZORDER` reorders data to improve **data skipping** for common filter columns (here: `user_id`, `product_id`).
- Benchmarks in Serverless can vary (warm vs cold runs). Small datasets might show minor differences.
- Serverless compute does not support persisted caching for tables, so `spark.table(...).cache()` can fail.

---

## Evidence
- Notebook: `day_10_performance_optimization.ipynb`
- Commands executed:
  - Plan inspection:
    - `spark.sql("SELECT * FROM ecommerce.silver.events WHERE event_type='purchase'").explain(True)`
  - Partitioned tables:
    - `ecommerce.silver.events_part` (PARTITIONED BY `event_date`)
    - `ecommerce.silver.events_part2` (PARTITIONED BY `event_date`, `event_type`)
  - Optimization:
    - `OPTIMIZE ecommerce.silver.events_part ZORDER BY (user_id, product_id)`
  - Benchmark runs (3 iterations each):
    - Base table times: ~`[0.53s, 0.37s, 0.35s]`
    - Partitioned table times: ~`[0.65s, 0.33s, 0.25s]`
  - Partition pruning validation:
    - `spark.sql("SELECT * FROM ecommerce.silver.events_part2 WHERE event_date = '2019-10-05'").explain(True)`
