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

> Mid-level recall for [[Apache Kafka|Kafka]] — guarantees, config, and operations.

## Model
- Topic → partitions → ordered, immutable, append-only log; offset per partition.
- **Ordering only within a partition**; same key → same partition → ordered. Partitions = unit of parallelism + ordering.
- Retention by time/size; **compaction** keeps latest value per key (changelog/state).

## Producer (durability vs latency)
- `acks=0|1|all`; `all` + `min.insync.replicas=2` (RF=3) tolerates one broker loss without data loss.
- **Idempotent producer** (`enable.idempotence=true`) dedupes retries; needed for exactly-once. `max.in.flight ≤ 5` to keep ordering with retries.
- Batching: `linger.ms` + `batch.size` for throughput; `compression.type` (lz4/zstd).

## Consumer
- Consumer group: each partition consumed by exactly one member; more consumers than partitions → idle ones.
- Rebalancing strategies: prefer **cooperative-sticky** (incremental, avoids stop-the-world). Static membership (`group.instance.id`) reduces rebalances.
- Offsets: commit after processing (at-least-once); manual commit for control. `max.poll.interval.ms` too low + slow processing → kicked from group.
- **Consumer lag** is the key health metric.

## Delivery Semantics
- At-most-once (commit before process), at-least-once (default — make consumers **idempotent**), exactly-once (idempotent producer + transactions + `read_committed` / EOS in Streams).

## Reliability & Ops
- RF, leader + followers, **ISR**; unclean leader election off for safety.
- DLQ / dead-letter topic for poison messages; retry topics with backoff.
- Schema Registry: Avro/Protobuf with compatibility (BACKWARD is common) for safe evolution.
- KRaft replaces ZooKeeper (metadata quorum) in modern clusters.

## Sizing / Design
- Partition count = target throughput / per-partition throughput, and ≥ max consumers; hard to reduce later.
- Hot partitions from skewed keys → better key or custom partitioner.

## Sharp Interview Answers
- How is ordering guaranteed? per partition via key.
- Exactly-once: idempotent producer + transactions + read_committed.
- Why is my consumer rebalancing / lagging? slow processing vs `max.poll.interval.ms`, too few partitions, GC pauses.
- Compaction vs retention; ISR and `acks=all`.

## Revision Checklist
- [ ] Partitions/offsets/ordering + keys
- [ ] acks, idempotence, min.insync.replicas
- [ ] Consumer groups, cooperative-sticky rebalancing, lag
- [ ] Delivery semantics + EOS
- [ ] Schema evolution, DLQ, KRaft
