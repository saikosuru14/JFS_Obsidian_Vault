---
title: Event Versioning
aliases:
  - Event Versioning
domain: Microservices
module: Event-Driven
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - microservices
related:
  - "[[Event-Driven Architecture]]"
---

# Event Versioning

## Overview
Events are a long-lived contract between producers and independently-deployed consumers. Because you can't upgrade everyone at once, event schemas must **evolve without breaking** existing consumers.

## Why It Matters
A careless schema change breaks every downstream consumer and can corrupt replayed history. Compatibility rules + a schema registry are how you evolve safely.

## Compatibility Types
| Type | Safe change | Who upgrades first |
|------|-------------|--------------------|
| **Backward** | add optional field, remove field | consumers first |
| **Forward** | producers add fields old consumers ignore | producers first |
| **Full** | both | either |

Rule of thumb: **only add optional fields; never rename or repurpose; never remove required fields.**

## Techniques
- **Schema Registry** (Confluent) with Avro/Protobuf/JSON Schema — enforces compatibility at publish time and stores schema versions; messages carry a schema id.
- **Tolerant reader** — consumers ignore unknown fields and default missing ones.
- **Versioned event types/topics** (`OrderPlacedV2`) when a breaking change is unavoidable — run both during migration.

## Interview Questions
- **How do you evolve event schemas safely?** Backward-compatible changes (add optional fields), a schema registry to enforce compatibility, tolerant readers.
- **What is backward vs forward compatibility?** New schema reads old data vs old schema reads new data.
- **What if a breaking change is unavoidable?** Introduce a new version/topic and run both during migration.

## Related Topics
- [[Event-Driven Architecture]] · [[Apache Kafka]] · [[REST vs gRPC]]

## Quick Revision
- Events are a contract; evolve without breaking consumers. Add optional fields only; use a Schema Registry (Avro/Protobuf) + tolerant readers; version/topic-split for breaking changes.
