# Day 04 — Delta Lake Introduction

## Focus
- What is Delta Lake?
- ACID transactions (reliability on data lake storage)
- Schema enforcement
- Delta vs Parquet

---

## Key Learnings

### What is Delta Lake?
Delta Lake is an open storage layer that brings **reliability and performance** to data lakes by adding:
- Transaction log (`_delta_log/`)
- ACID-like guarantees for writes/updates
- Schema enforcement and evolution
- Support for upserts (MERGE), deletes, and time travel (Delta features)

### ACID Transactions (Why it matters)
Delta tables handle concurrent reads/writes safely:
- Prevents partial writes and corrupted outputs
- Enables consistent reads while data is being updated
- Supports safe batch + streaming patterns

### Schema Enforcement
Delta prevents accidentally writing incompatible schemas (e.g., wrong column names/types) unless explicitly allowed (schema evolution).

### Delta vs Parquet
- **Parquet** is a file format (fast, columnar), but it doesn’t include transactional guarantees by itself.
- **Delta** is typically Parquet **plus** a transaction log, enabling governance, reliability, and advanced operations (MERGE/DELETE/UPDATE).

---

## Tasks Completed (Checklist)
- [x] Converted CSV dataset to Delta format
- [x] Created Delta tables (PySpark + SQL)
- [x] Tested schema enforcement (append with wrong schema fails)
- [x] Handled duplicate inserts using a deterministic `event_id` + MERGE
