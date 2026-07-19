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
order: 5
tags:
  - revision
  - kafka
---

# Kafka Cheat Sheet

> Interview-ready revision for [[Apache Kafka|Kafka]] (4–5 YOE). Concepts, config, tables, and Q&A with answers.

---

## 1. Core Model
A distributed, partitioned, replicated **commit log**.
- **Topic** → N **partitions**. A partition is an ordered, immutable, append-only sequence; each record has a monotonic **offset**.
- Partition = unit of **parallelism** *and* **ordering**. Ordering is guaranteed **only within a partition**.
- **Broker** = a server holding partitions; a partition has one **leader** + follower replicas.
- Consumers **pull**; the broker doesn't track per-consumer state beyond committed offsets.

```
Topic "orders" (3 partitions)
 P0: [0][1][2][3]...        leader on broker1
 P1: [0][1][2]...           leader on broker2
 P2: [0][1][2][3][4]...     leader on broker3
```

---

## 2. Producers
Record routing: if a **key** is set → `partition = hash(key) % n` (same key → same partition → ordered). No key → sticky partitioning (batches to one partition then rotates).

```properties
acks=all                         # wait for ISR
enable.idempotence=true          # dedupe retries (default in modern clients)
max.in.flight.requests.per.connection=5   # safe ordering with idempotence
retries=2147483647
linger.ms=10                     # small wait to batch
batch.size=32768
compression.type=zstd            # or lz4
```
- **Durability vs latency:** `acks=0` (fire-and-forget) → `1` (leader only) → `all` (all ISR). `all` + `min.insync.replicas=2` (RF=3) survives one broker loss with no data loss.
- **Idempotent producer** eliminates duplicates from retries (per partition). Without it, retries can duplicate or reorder.
- Throughput: bigger `batch.size` + `linger.ms` + compression.

---

## 3. Consumers
Members of a **consumer group** split partitions — each partition consumed by exactly one member in the group. More consumers than partitions → idle consumers (partition count caps parallelism).

```java
props.put("group.id", "order-processor");
props.put("enable.auto.commit", "false");     // commit AFTER processing
props.put("auto.offset.reset", "earliest");   // no committed offset → start
props.put("max.poll.records", "500");
props.put("partition.assignment.strategy",
          "org.apache.kafka.clients.consumer.CooperativeStickyAssignor");

while (running) {
    var records = consumer.poll(Duration.ofMillis(200));
    for (var r : records) process(r);          // idempotent!
    consumer.commitSync();                      // at-least-once
}
```
- Key timings: `max.poll.interval.ms` (max gap between polls — exceed it and you're kicked and a rebalance triggers), `session.timeout.ms`/`heartbeat.interval.ms` (liveness).
- **Slow processing** between polls is the #1 cause of surprise rebalances → reduce `max.poll.records` or process async.

---

## 4. Delivery Semantics
| Semantic | How | Note |
|----------|-----|------|
| At-most-once | commit offset *before* processing | may lose on crash |
| At-least-once | commit *after* processing (default) | may reprocess → make consumers **idempotent** |
| Exactly-once (EOS) | idempotent producer + transactions + `isolation.level=read_committed` | within Kafka / Kafka Streams |

```java
producer.initTransactions();
producer.beginTransaction();
producer.send(rec);
producer.sendOffsetsToTransaction(offsets, groupMetadata);  // atomic consume-process-produce
producer.commitTransaction();
```

---

## 5. Replication & Reliability
- **RF** copies per partition; leader handles reads/writes, followers replicate.
- **ISR** (in-sync replicas): replicas caught up within `replica.lag.time.max.ms`. `acks=all` waits for all ISR; a leader can only come from ISR.
- `min.insync.replicas`: minimum ISR for an `acks=all` write to succeed — else producer errors (protects against silent data loss).
- `unclean.leader.election.enable=false`: never elect an out-of-sync replica (availability vs durability — keep off for correctness).

---

## 6. Storage & Retention
- Partition = segments on disk; old segments deleted by policy.
- `cleanup.policy=delete` (time/size retention: `retention.ms`, `retention.bytes`) **or** `compact` (**log compaction** keeps the latest value per key — great for changelogs/state; deletes via **tombstone** = null value). Can combine `delete,compact`.

---

## 7. Ordering & Keys
- Global ordering ⇒ single partition (kills parallelism). Usually you only need **per-entity** ordering → key by aggregate id (e.g., `orderId`).
- Repartitioning changes key→partition mapping, breaking prior ordering guarantees. Choose partition count with headroom (hard to reduce).
- **Hot partition** from skewed keys → better key design or custom partitioner.

---

## 8. Schema & Serialization
- **Schema Registry** with Avro/Protobuf/JSON-Schema; producers/consumers validate against registered schemas.
- **Compatibility** (BACKWARD is common): add optional fields with defaults; don't remove/rename required fields. Enables independent producer/consumer evolution.

---

## 9. Ecosystem (know what they're for)
- **Kafka Connect**: source/sink connectors (DB ↔ Kafka) without code; CDC via Debezium.
- **Kafka Streams**: stateful stream processing (joins, windows, aggregations) with local state stores + changelog topics; supports EOS.
- **KRaft** replaces ZooKeeper (metadata as an internal Raft quorum) in modern clusters.

---

## 10. Ops & Tuning
- **Consumer lag** (log-end offset − committed offset) is *the* health metric → alert on it.
- Reduce rebalances: **CooperativeStickyAssignor** (incremental, no stop-the-world), **static membership** (`group.instance.id`), tune `max.poll.*`.
- Sizing: partitions ≈ target throughput ÷ per-partition throughput, and ≥ max consumers.
- Poison messages: send to a **DLQ / dead-letter topic** after N retries (retry topics with backoff).

---

## 11. Interview Q&A (with answers)

**Q: How does Kafka guarantee ordering?**
A: Only within a partition. Records with the same key go to the same partition, so per-key ordering is preserved; there's no global ordering across partitions unless you use a single partition.

**Q: How do you achieve exactly-once?**
A: Idempotent producer (dedupes retries) + transactions (atomic writes across partitions, and atomic consume-process-produce via `sendOffsetsToTransaction`) + consumers reading `read_committed`. Kafka Streams gives EOS out of the box.

**Q: `acks=all` vs `min.insync.replicas`?**
A: `acks=all` waits for all *current* ISR to ack. `min.insync.replicas` sets the floor — if ISR drops below it, an `acks=all` write fails instead of silently accepting fewer copies. Use `acks=all` + `min.insync.replicas=2` with RF=3.

**Q: Why is my consumer group constantly rebalancing / lagging?**
A: Usually processing takes longer than `max.poll.interval.ms` (member deemed dead), too few partitions, GC pauses, or scaling churn. Fix: lower `max.poll.records`, process faster/async, use cooperative-sticky + static membership.

**Q: What happens if you have more consumers than partitions?**
A: Extra consumers sit idle — partition count is the max parallelism for a group. Add partitions to scale (can't reduce later).

**Q: Log compaction vs retention?**
A: Retention deletes old data by time/size. Compaction keeps the latest record per key (a materialized "current state"); deletes are tombstones. Use compaction for changelogs/KTables.

**Q: At-least-once vs exactly-once in practice?**
A: At-least-once is the pragmatic default — commit after processing and make consumers idempotent (dedupe by key/id). Full EOS adds transaction overhead; use it when duplicates are unacceptable and you stay within Kafka.

**Q: How do you handle a poison message?**
A: Retry with backoff a bounded number of times, then route to a dead-letter topic for inspection/replay so it doesn't block the partition.

---

## Revision Checklist
- [ ] Topic/partition/offset + per-key ordering
- [ ] acks, idempotence, min.insync.replicas, ISR
- [ ] Consumer groups, offset commit, rebalance causes + cooperative-sticky
- [ ] Delivery semantics + EOS (transactions)
- [ ] Retention vs compaction (tombstones)
- [ ] Schema Registry compatibility
- [ ] Connect / Streams / KRaft
- [ ] Consumer lag, sizing, DLQ
