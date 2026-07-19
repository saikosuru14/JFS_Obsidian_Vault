---
title: CAP Theorem
aliases:
  - CAP Theorem
domain: Computer Science
module: Database Fundamentals
status: Not Started
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 6
tags:
  - computer-science
---

# CAP Theorem

A distributed system can guarantee at most two of:

- Consistency
- Availability
- Partition Tolerance

Examples:
- PostgreSQL: CP (single-node focus)
- Cassandra: AP
- Distributed systems always assume partition tolerance.

Related:
[[Microservices]]
