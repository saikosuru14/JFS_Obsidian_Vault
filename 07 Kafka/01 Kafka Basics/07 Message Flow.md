---
title: Message Flow
aliases:
  - Message Flow
domain: Kafka
module: Kafka Basics
status: Not Started
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 7
tags:
  - kafka
---

# Message Flow

Producer → Broker Leader → Followers (replication) → Consumer.

Messages are appended to partition logs sequentially.