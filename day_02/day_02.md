# Day 02 — Apache Spark Fundamentals

## Focus
- Spark architecture: **Driver**, **Executors**, **DAG**
- **DataFrames vs RDDs**
- **Lazy evaluation** (transformations vs actions)
- Notebook magic commands: **%sql**, **%python**, **%fs** (and useful extras like **%sh**)

---

## Key Learnings

### Spark Architecture (Driver / Executors / DAG)
- **Driver**: orchestrates the job, builds the execution plan (DAG), schedules tasks.
- **Executors**: run tasks in parallel and store data in memory/disk when needed.
- **DAG**: Spark builds a logical/physical plan from transformations, then executes it only when an **action** is called.

### DataFrames vs RDDs
- **DataFrames** are higher-level, optimized (Catalyst + Tungsten), easier to write/read, and usually faster.
- **RDDs** are lower-level, more manual, and generally used only for special cases.

### Lazy Evaluation
- Transformations (e.g., `select`, `filter`, `groupBy`) are **lazy** → Spark does not execute immediately.
- Actions (e.g., `count`, `show`, `collect`) trigger execution.

### Databricks Notebook Magics
- `%fs` to explore storage paths and files.
- `%sql` to run SQL directly in the notebook.
- `%python` to force Python mode (optional if notebook default is Python).
- (Extra) `%sh` for shell commands.

---

## Tasks Completed (Checklist)
- [x] Upload / prepare sample e-commerce CSV (using Unity Catalog Volumes)
- [x] Read data into a Spark DataFrame
- [x] Perform basic operations: select, filter, groupBy, orderBy
- [x] Export results (CSV and/or Delta)
