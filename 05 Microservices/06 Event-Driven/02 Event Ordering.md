---
title: Event Ordering
aliases:
  - Event Ordering
domain: Microservices
module: Event-Driven
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 2
tags:
  - microservices
related:
  - "[[Event-Driven Architecture]]"
---

# Event Ordering

## Overview
Order matters for state changes (`AccountCreated` before `AccountUpdated`). In Kafka, ordering is guaranteed **only within a partition**, not across a topic — so how you partition determines what stays ordered.

## Why It Matters
Out-of-order processing corrupts state. The classic fix — partition by entity key — is a guaranteed follow-up whenever you mention Kafka in an interview.

## The Rule
- **Same key -> same partition -> ordered.** Use the aggregate id (e.g., `orderId`) as the partition key so all events for one entity are processed in order.
- Across partitions there is **no global order** — and that's the trade-off for parallelism/scale.

## Consequences
- More partitions = more parallelism but no cross-partition ordering.
- A single consumer per partition (within a consumer group) preserves order on the consumer side.
- Producer retries can reorder unless you enable idempotent producer / `max.in.flight` limits.

## Handling Out-of-Order
- **Version/sequence numbers** in events; consumers ignore stale updates.
- **Idempotent + commutative** handlers where possible ([[Idempotency]]).
- Buffer and reorder by sequence if strict order across keys is truly required (rare, expensive).

## Interview Questions
- **Does Kafka guarantee ordering?** Only within a partition — pick a partition key (entity id) to keep an entity's events ordered.
- **How do you keep an entity's events ordered?** Partition by its id so they land on the same partition.
- **How to handle possible reordering?** Version numbers + idempotent consumers; enable idempotent producer.

## Related Topics
- [[Event-Driven Architecture]] · [[Apache Kafka]] · [[Idempotency]]

## Quick Revision
- Order guaranteed per partition only. Partition by entity id to keep its events ordered; no global order across partitions. Use versions + idempotency to tolerate reordering.
