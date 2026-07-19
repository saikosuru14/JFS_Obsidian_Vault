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

> Fast recall for databases. See [[Database Fundamentals]] for depth.

## Query Order of Execution
`FROM → WHERE → GROUP BY → HAVING → SELECT → DISTINCT → ORDER BY → LIMIT`

## Joins
- `INNER` = matching rows both sides.
- `LEFT` = all left + matched right (nulls otherwise); `RIGHT` = mirror.
- `FULL OUTER` = everything; `CROSS` = cartesian product.
- Self-join for hierarchies; anti-join via `LEFT JOIN ... WHERE right.id IS NULL`.

## Aggregation
- `COUNT/SUM/AVG/MIN/MAX` with `GROUP BY`; filter groups with `HAVING`.
- Window functions: `ROW_NUMBER() / RANK() / DENSE_RANK() OVER (PARTITION BY ... ORDER BY ...)`.

## Indexing
- B-tree indexes speed equality/range lookups and sorts; cost = slower writes + storage.
- Composite index follows **leftmost-prefix** rule.
- Covering index serves a query from the index alone.

## Transactions / ACID
- Atomicity, Consistency, Isolation, Durability.
- Isolation levels vs anomalies: Read Uncommitted (dirty), Read Committed, Repeatable Read (no non-repeatable), Serializable (no phantom).

## Normalization
- 1NF atomic values; 2NF no partial dependency; 3NF no transitive dependency.
- Denormalize for read-heavy workloads (trade writes/consistency for speed).

## SQL vs NoSQL
- SQL: strong schema, ACID, joins. NoSQL: flexible schema, horizontal scale, eventual consistency.

## Top Interview One-Liners
- `WHERE` filters rows before grouping; `HAVING` filters after.
- `DELETE` (logged, rollback-able) vs `TRUNCATE` (fast, resets) vs `DROP` (removes table).
- Index trade-off: faster reads, slower writes.

## Revision Checklist
- [ ] Execution order
- [ ] Join types
- [ ] Window functions
- [ ] Isolation levels vs anomalies
- [ ] Normalization forms
