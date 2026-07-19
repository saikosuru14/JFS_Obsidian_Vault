---
title: Database Fundamentals
aliases:
  - Database Fundamentals
  - DBMS Fundamentals
  - Database
domain: Computer Science
module: Database Fundamentals
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 0
tags:
  - computer-science
  - databases
  - index
---

# Database Fundamentals

> Module index — how databases store, protect, and serve data.

## Overview
A Database Management System (DBMS) stores, retrieves, and manages data while ensuring consistency, durability, security, and safe concurrent access.

## Learning Path
1. [[ACID Properties]]
2. [[Transactions]]
3. [[Isolation Levels]]
4. [[Normalization]]
5. [[Indexing]]
6. [[CAP Theorem]]

## Why Use a DBMS
- Reduce redundancy and maintain consistency.
- Support concurrent users with isolation.
- Recover after failures (durability).
- Enforce security and access control.

## Types
- **Relational** (PostgreSQL, MySQL) — structured, ACID, SQL.
- **NoSQL** (MongoDB, Cassandra, Redis) — flexible schema, horizontal scale.

## Interview Questions
- Explain ACID with an example.
- What do isolation levels prevent (dirty/non-repeatable/phantom reads)?
- When would you denormalize?
- How does an index speed up queries, and what's the cost?

## Revision Summary
- ACID + transactions + isolation guarantee correctness.
- Normalization reduces redundancy; indexing speeds reads at write cost.
