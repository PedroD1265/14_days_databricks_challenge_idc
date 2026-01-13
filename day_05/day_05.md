# Day 05 — Delta Lake Advanced

## Focus
- Time travel (version history)
- MERGE operations (upserts / incremental loads)
- OPTIMIZE & ZORDER
- VACUUM cleanup

---

## What I Used (My Setup)
- **Delta path (from Day 04):**  
  `dbfs:/Volumes/workspace/ecommerce/ecommerce_data/delta/events`
- **Managed table (from Day 04):**  
  `events_table`

> Note: Some features (OPTIMIZE/ZORDER/VACUUM) may depend on workspace/edition permissions.

---

## Tasks Completed (Checklist)
- [x] Implemented incremental MERGE (upsert) into Delta table
- [x] Queried historical versions (time travel)
- [x] Ran OPTIMIZE + ZORDER (or validated availability)
- [x] Ran VACUUM cleanup (or validated availability)
