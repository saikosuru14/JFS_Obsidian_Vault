---
title: Kafka Index
aliases:
  - Kafka
  - Apache Kafka
  - Kafka Index
domain: Kafka
module: Index
status: Learning
difficulty: Hard
priority: High
interview: 5
revision: Weekly
order: 0
tags:
  - kafka
  - index
---

# Apache Kafka

> Domain hub — the distributed event-streaming platform, end to end.

## Overview
Apache Kafka is a distributed, partitioned, replicated commit log used for high-throughput event streaming and messaging. This domain covers its architecture, the producer/consumer model, replication guarantees, storage, schemas, the ecosystem (Connect, Streams), and operations.

## Learning Roadmap
1. [[Kafka Basics Index|Kafka Basics]] — architecture, brokers, topics, partitions, offsets.
2. [[Producers Index|Producers]] — sending records, retries, idempotence, acks.
3. [[Consumers Index|Consumers]] — consumer groups, rebalancing, offset commits.
4. [[Replication and Reliability Index|Replication & Reliability]] — ISR, delivery guarantees, exactly-once.
5. [[Storage and Retention Index|Storage & Retention]] — log segments, compaction, retention.
6. [[Schema and Serialization Index|Schema & Serialization]] — Schema Registry, Avro, Protobuf.
7. [[Kafka Ecosystem Index|Kafka Ecosystem]] — Connect, Streams, KSQL, MirrorMaker.
8. [[Operations Index|Operations]] — monitoring, ZooKeeper vs KRaft.

## Suggested Study Order
Learn the log/partition model first, then producers and consumers, then the reliability guarantees (the heart of Kafka interviews), followed by storage, schemas, ecosystem, and operations.

## Prerequisites
- [[Computer Networks]] and [[Microservices]] fundamentals.

## Related Concepts
- [[Event-Driven Index|Event-Driven Architecture]] in [[Microservices]].
- [[Message Queues]] in [[System Design]].

## Interview Focus
- Partitions, offsets, and ordering guarantees.
- Consumer groups and rebalancing.
- Delivery semantics: at-most/at-least/exactly-once.
- ISR and replication; ZooKeeper vs KRaft.

## Topic Tracker

> Live, auto-updating table of every note in this domain, grouped by module.

![[Kafka.base]]
