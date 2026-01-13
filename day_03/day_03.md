# Day 03 — PySpark Transformations Deep Dive (11/01/26)

## Focus
- PySpark vs Pandas (when to use each)
- Joins: inner, left (and conceptually right/outer)
- Window functions: running totals, rankings
- UDFs (User-Defined Functions) and when to avoid them

---

## Key Learnings

### PySpark vs Pandas
- **PySpark** is built for **distributed** processing and scales to large datasets.
- **Pandas** is great for **small** datasets or post-processing once you’ve already reduced data size.
- Best practice: use Spark for heavy lifting, convert to Pandas only for small results.

### Joins
- **Inner join** keeps only matching keys in both tables.
- **Left join** keeps all rows from the left table even if no match exists on the right.
- Right/outer joins are useful for completeness checks and data quality validation.

### Window Functions
- Window functions let you compute metrics **across related rows** without collapsing the dataset like `groupBy`.
- Typical use cases: **running totals**, **rankings**, **session/user timelines**.

### UDFs
- UDFs are flexible but often slower than built-in Spark SQL functions.
- Prefer built-in functions (`pyspark.sql.functions`) whenever possible.
- Use UDFs only when logic can’t be expressed with native Spark functions.

---

## Tasks Completed (Checklist)
- [x] Loaded full e-commerce dataset (Oct + Nov)
- [x] Performed joins using a derived product dimension
- [x] Calculated running totals and rankings with window functions
- [x] Created derived features (date parts, conversion rate, price buckets)
