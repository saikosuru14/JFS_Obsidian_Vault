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

> Mid-level recall for databases — indexing, transactions, and query tuning.

## Execution Order
`FROM → JOIN → WHERE → GROUP BY → HAVING → SELECT → DISTINCT → ORDER BY → LIMIT`
(so column aliases from SELECT aren't visible in WHERE).

## Indexing (interview gold)
- B-tree serves equality, range, prefix, and ORDER BY. Hash index = equality only.
- **Composite index = leftmost-prefix rule**: `(a,b,c)` helps `a`, `a,b`, `a,b,c` — not `b` alone.
- **Covering index**: query served entirely from the index (no table lookup).
- Index selectivity matters; low-cardinality columns rarely help. Indexes slow writes + cost storage.
- A function on a column (`WHERE UPPER(x)=…`) kills index use → use expression/functional indexes.

## Query Tuning
- Read `EXPLAIN [ANALYZE]`: look for seq scans on big tables, bad row estimates, nested-loop vs hash join.
- Avoid `SELECT *`; filter early; batch writes; keyset pagination (`WHERE id > :last LIMIT n`) over `OFFSET` for deep pages.
- N+1 in ORMs → join/fetch or batch.

## Transactions / Isolation
- ACID. Isolation vs anomalies: Read Uncommitted (dirty), Read Committed (default in PG), Repeatable Read (no non-repeatable; PG also blocks phantoms via MVCC), Serializable (full).
- **MVCC** (PostgreSQL/InnoDB): readers don't block writers; each txn sees a snapshot.
- Locking: row locks, `SELECT … FOR UPDATE` (pessimistic), version column (optimistic). Deadlocks → consistent lock order, short txns, retry on deadlock error.

## Modeling
- Normalize to 3NF to remove redundancy; **denormalize** deliberately for read-heavy paths (accept write/consistency cost).
- Scaling: read replicas (read scaling), partitioning (by range/hash), sharding (write scaling; needs a shard key).

## SQL vs NoSQL
- SQL: strong schema, ACID, joins, ad-hoc queries. NoSQL: flexible schema, horizontal scale, denormalized access patterns, eventual consistency. Choose by access pattern, not hype.

## Sharp Interview Answers
- Why isn't my index used? leftmost-prefix miss, function on column, low selectivity, small table.
- `WHERE` vs `HAVING`; `DELETE` vs `TRUNCATE` vs `DROP`.
- Offset vs keyset pagination; how MVCC avoids read locks.
- Optimistic vs pessimistic locking; how to handle deadlocks.

## Revision Checklist
- [ ] Execution order + join types
- [ ] Composite/covering indexes + leftmost prefix
- [ ] EXPLAIN + keyset pagination
- [ ] Isolation levels, MVCC, locking, deadlocks
- [ ] Normalization vs denormalization; sharding
