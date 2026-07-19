---
title: Idempotency
aliases:
  - Idempotency
domain: Microservices
module: Distributed Data and Transactions
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 7
tags:
  - microservices
related:
  - "[[Distributed Data and Transactions Index|Distributed Data and Transactions]]"
  - "[[Outbox Pattern]]"
---

# Idempotency

## Overview
An operation is idempotent if performing it multiple times has the **same effect as performing it once**. In distributed systems messages get redelivered and clients retry, so consumers must dedupe or design operations to be naturally idempotent.

## Why It Matters
At-least-once delivery (Kafka, [[Outbox Pattern|outbox]], [[Retry|retries]]) means duplicates are inevitable. Idempotency is what makes "process this again" safe — without it you double-charge, double-ship, double-count.

## Techniques
- **Idempotency key** — client sends a unique key; server records processed keys and returns the prior result on repeat (standard for payment APIs).
- **Natural idempotency** — design the effect to be a set/upsert rather than an increment (`status = SHIPPED` vs `count = count + 1`).
- **Unique constraints** — DB unique index on a business key rejects duplicates.
- **Inbox table** — record processed message ids; skip if already seen.
- **Conditional updates** — optimistic version/`WHERE status = 'PENDING'` so a repeat is a no-op.

## HTTP Semantics
GET/PUT/DELETE are idempotent by definition; **POST is not** — protect create/charge endpoints with idempotency keys.

## Example
```java
if (processed.contains(msg.id())) return;   // dedupe
process(msg);
processed.add(msg.id());                     // ideally in the same tx
```

## Interview Questions
- **What is idempotency and why does it matter here?** Same effect on repeat; required because delivery is at-least-once (duplicates happen).
- **How do you make a payment endpoint idempotent?** Idempotency keys stored server-side returning the original result on retry.
- **Which HTTP methods are idempotent?** GET, PUT, DELETE — not POST.

## Related Topics
- [[Outbox Pattern]] · [[Retry]] · [[Saga Pattern]] · [[Eventual Consistency]]

## Quick Revision
- Repeat = same effect. Needed for at-least-once delivery. Use idempotency keys, unique constraints, inbox dedupe, upserts/conditional updates. POST isn't idempotent — protect it.
