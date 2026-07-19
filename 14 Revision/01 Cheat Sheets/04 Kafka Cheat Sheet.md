---
title: Kafka Cheat Sheet
aliases:
  - Kafka Cheat Sheet
domain: Revision
module: Cheat Sheets
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 4
tags:
  - revision
  - kafka
---

# Kafka Cheat Sheet

> Fast recall for [[Apache Kafka|Kafka]]. See the [[Kafka Index|Kafka domain]] for depth.

## Core Model
- Topic → partitions → ordered, immutable log of records (offset per partition).
- Order guaranteed **within a partition**, not across.
- Partition key decides partition (same key → same partition → ordered).

## Producers
- `acks=0` (fire-forget), `1` (leader), `all` (ISR) — durability vs latency.
- Idempotent producer prevents duplicates on retry; enables exactly-once with transactions.

## Consumers
- Consumer group: each partition consumed by exactly one consumer in the group.
- More consumers than partitions → idle consumers.
- Rebalancing on membership change; commit offsets (auto vs manual).

## Reliability
- Replication factor N; leader + followers; **ISR** = in-sync replicas.
- Delivery: at-most-once, at-least-once (default, idempotent consumers needed), exactly-once (txns).
- `min.insync.replicas` with `acks=all` for durability.

## Storage
- Retention by time/size; log compaction keeps latest value per key.

## Ecosystem
- Connect (source/sink), Streams (stateful processing), Schema Registry (Avro/Protobuf), KRaft (no ZooKeeper).

## Top Interview One-Liners
- How is ordering guaranteed? Per partition, via key.
- Exactly-once? Idempotent producer + transactions + read-committed.
- Scale consumers? Add partitions (up to consumer count).

## Revision Checklist
- [ ] Partitions, offsets, ordering
- [ ] acks and idempotence
- [ ] Consumer groups & rebalancing
- [ ] ISR and delivery semantics
- [ ] Compaction vs retention
