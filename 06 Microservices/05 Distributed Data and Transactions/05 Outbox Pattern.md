---
title: Outbox Pattern
aliases:
  - Outbox Pattern
domain: Microservices
module: Distributed Data and Transactions
status: Learning
difficulty: Hard
priority: High
interview: 4
revision: Weekly
order: 5
tags:
  - microservices
related:
  - "[[Distributed Data and Transactions Index|Distributed Data and Transactions]]"
  - "[[Saga Pattern]]"
  - "[[Idempotency]]"
---

# Outbox Pattern

## Overview
The transactional outbox solves the **dual-write problem**: you can't atomically write to your database *and* publish to a broker (no shared transaction). Instead, write the business change and an event row to an **outbox table in the same local transaction**; a separate process publishes those rows to the broker.

## Why It Matters
Without it you either lose events (DB commits, publish fails) or emit phantom events (publish succeeds, DB rolls back). The outbox guarantees the event is published **if and only if** the data was committed.

## How It Works
```
BEGIN TX
  update orders ...            -- business data
  insert into outbox (event)   -- event, same transaction
COMMIT
-- later, asynchronously:
Relay reads unpublished outbox rows -> publishes to Kafka -> marks as sent
```
The relay is typically **Change Data Capture (CDC)** via **Debezium** reading the DB log, or a polling publisher.

## Delivery Semantics
- Provides **at-least-once** delivery -> consumers must be [[Idempotency|idempotent]] (the relay may publish a row twice after a crash).
- Preserves ordering per aggregate if you partition by aggregate id.

## Related Pattern
- **Inbox** — consumer side: record processed message ids to dedupe (idempotent consumption).

## Interview Questions
- **What problem does the outbox solve?** The dual-write problem — atomically committing data and publishing an event.
- **How is the event actually published?** A relay/CDC (e.g., Debezium) reads the outbox/DB log and publishes asynchronously.
- **What delivery guarantee?** At-least-once -> consumers must be idempotent.

## Related Topics
- [[Saga Pattern]] · [[Idempotency]] · [[Event-Driven Architecture]] · [[Eventual Consistency]]

## Quick Revision
- Write data + event in one local tx (outbox table); a relay/CDC (Debezium) publishes async. Solves dual-write; at-least-once -> idempotent consumers. Inbox dedupes on the consumer side.
