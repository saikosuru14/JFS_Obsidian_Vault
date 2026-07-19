---
title: SQL Cheat Sheet
aliases:
  - SQL Cheat Sheet
domain: Revision
module: Cheat Sheets
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - revision
  - sql
  - databases
---

# SQL Cheat Sheet

> Interview-ready revision for databases ([[Database Fundamentals]]) (4–5 YOE). Concepts, code, tables, and Q&A with answers.

---

## 1. Logical Execution Order
`FROM → JOIN → WHERE → GROUP BY → HAVING → SELECT → DISTINCT → ORDER BY → LIMIT/OFFSET`
Implication: `SELECT` aliases aren't visible in `WHERE`/`GROUP BY`; `WHERE` filters rows, `HAVING` filters groups.

## 2. Joins
| Join | Returns |
|------|---------|
| INNER | rows matching both sides |
| LEFT/RIGHT | all of one side + matches (NULLs otherwise) |
| FULL OUTER | everything, matched where possible |
| CROSS | cartesian product |
| Self | table joined to itself (hierarchies) |
Anti-join: `LEFT JOIN … WHERE r.id IS NULL`. Semi-join: `EXISTS (…)`.

## 3. Indexing (interview gold)
B-tree indexes serve equality, range, prefix, `ORDER BY`, `MIN/MAX`.
- **Composite index leftmost-prefix:** `(a,b,c)` helps `a`, `(a,b)`, `(a,b,c)`, not `b` alone or `c` alone.
- **Covering index:** all selected columns are in the index → no table lookup ("index-only scan").
- **Clustered vs non-clustered:** InnoDB stores rows in PK order (clustered); secondary indexes store the PK and require a lookup. Keep PK small/monotonic.
- **Partial/functional indexes:** `CREATE INDEX ... WHERE active`, or on `LOWER(email)`.

**Why an index isn't used:** function on the column (`WHERE UPPER(x)=…`), leading wildcard (`LIKE '%x'`), implicit type cast, low selectivity, or a small table (seq scan is cheaper).

## 4. Query Tuning
```sql
EXPLAIN ANALYZE
SELECT o.id FROM orders o WHERE o.customer_id = 42 AND o.status = 'NEW';
```
Read the plan: **Seq Scan on a big table** = missing/unused index; check row-estimate accuracy (stale stats → `ANALYZE`); join type (nested loop for few rows, hash/merge for many). Avoid `SELECT *`; filter early; batch writes.

**Keyset pagination** (fast deep pages) beats `OFFSET` (which scans+discards):
```sql
SELECT * FROM orders WHERE id > :last_id ORDER BY id LIMIT 20;
```

**Window functions** (no collapsing rows):
```sql
SELECT id, amount,
       ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY created DESC) AS rn,
       SUM(amount)  OVER (PARTITION BY customer_id) AS cust_total
FROM orders;
```

## 5. Transactions & Isolation
ACID. Isolation levels vs anomalies:
| Level | Dirty read | Non-repeatable | Phantom |
|-------|-----------|----------------|---------|
| Read Uncommitted | ✅ | ✅ | ✅ |
| Read Committed (PG default) | ❌ | ✅ | ✅ |
| Repeatable Read (MySQL InnoDB default) | ❌ | ❌ | ❌* |
| Serializable | ❌ | ❌ | ❌ |

\*InnoDB RR blocks phantoms via gap locks; PG RR (snapshot) prevents non-repeatable but allows some phantoms.

**MVCC** (PostgreSQL, InnoDB): each transaction sees a consistent snapshot; **readers don't block writers** and vice versa. Old row versions are cleaned by vacuum/purge.

## 6. Locking & Deadlocks
- Shared (read) vs exclusive (write); row vs table. `SELECT … FOR UPDATE` = pessimistic row lock; `@Version` column = optimistic.
- **Deadlock**: two txns lock rows in opposite order → DB kills one (`deadlock detected`). Prevent: consistent lock ordering, short transactions, retry on deadlock error.

## 7. Modeling & Scaling
- Normalize to 3NF (remove redundancy/anomalies); **denormalize deliberately** for read-heavy paths (accept write cost + consistency handling).
- **Replication** (read replicas → read scaling, HA) vs **partitioning** (split one table by range/hash/list) vs **sharding** (split across nodes; needs a shard key that avoids hot spots).
- Upsert: PG `INSERT … ON CONFLICT (id) DO UPDATE`; MySQL `ON DUPLICATE KEY UPDATE`.

## 8. SQL vs NoSQL
SQL: strong schema, ACID, joins, ad-hoc queries. NoSQL: flexible schema, horizontal scale, denormalized to access patterns, often eventual consistency. Choose by access pattern and consistency needs.

---

## 9. Interview Q&A (with answers)

**Q: Why isn't my index being used?**
A: Common causes — a function/cast on the indexed column, a leading `%` in `LIKE`, breaking the leftmost-prefix rule on a composite index, low selectivity (optimizer prefers a scan), or stale statistics giving bad estimates.

**Q: Clustered vs non-clustered index?**
A: A clustered index defines the physical row order (InnoDB = the PK); there's one per table. Non-clustered/secondary indexes are separate structures pointing back to the row (via PK in InnoDB), so they may need an extra lookup unless the index is covering.

**Q: Explain isolation levels and the anomalies they prevent.**
A: Read Committed stops dirty reads; Repeatable Read also stops non-repeatable reads; Serializable stops phantoms too (full isolation). Higher levels cost concurrency.

**Q: How does MVCC avoid read locks?**
A: Writers create new row versions instead of overwriting; readers see the snapshot valid at their transaction start, so reads never block writes. Cleanup happens via vacuum (PG) / purge (InnoDB).

**Q: How do you handle deadlocks?**
A: Acquire locks in a consistent order, keep transactions short, and retry the victim transaction on the deadlock error. Monitor with the DB's deadlock log.

**Q: OFFSET vs keyset pagination?**
A: `OFFSET n` scans and discards n rows (slow for deep pages); keyset (`WHERE id > :last`) uses the index to jump directly — O(1)-ish per page, stable under inserts.

**Q: When would you denormalize?**
A: For read-heavy, latency-sensitive paths where joins are expensive — duplicate data or precompute aggregates, and handle the added write/consistency cost (triggers, app logic, or async updates).

**Q: `DELETE` vs `TRUNCATE` vs `DROP`?**
A: `DELETE` is row-by-row, logged, transactional, fires triggers; `TRUNCATE` fast-resets the table (minimal logging, resets identity, usually not row-trigger-firing); `DROP` removes the table entirely.

**Q: How do you find a slow query in production?**
A: Slow-query log / `pg_stat_statements`, then `EXPLAIN ANALYZE` the offender, check for scans/bad estimates/missing indexes, and fix (index, rewrite, or denormalize).

---

## Revision Checklist
- [ ] Execution order + join/anti/semi
- [ ] Composite (leftmost prefix) + covering + clustered indexes
- [ ] EXPLAIN ANALYZE + keyset pagination + window functions
- [ ] Isolation levels vs anomalies + MVCC
- [ ] Locking, FOR UPDATE, deadlock handling
- [ ] Normalization vs denormalization; replication/partitioning/sharding
- [ ] Upsert; SQL vs NoSQL
