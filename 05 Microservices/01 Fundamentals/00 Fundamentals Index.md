---
title: Fundamentals Index
aliases:
  - Fundamentals Index
domain: Microservices
module: Fundamentals
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 0
tags:
  - microservices
  - index
related:
  - "[[Microservices Index|Microservices]]"
  - "[[Monolith vs Microservices]]"
  - "[[Service Communication]]"
---

# Fundamentals

> Module index - part of the [[Microservices Index|Microservices]] learning path.

## Overview
Before the platform machinery (discovery, gateways, resilience), you need the core decisions: **when** microservices are worth it, and **how** services talk to each other (sync vs async, REST vs gRPC). These trade-offs drive every later design choice.

## Branches (expand each)
- **[[Monolith vs Microservices]]** — when to split, and when not to.
- **[[Service Communication]]** — the communication landscape.
  - [[Synchronous vs Asynchronous Communication]] — coupling vs latency.
    - [[REST vs gRPC]] — choosing a synchronous protocol.

## Learning Roadmap
1. [[Monolith vs Microservices]]
2. [[Service Communication]]
3. [[Synchronous vs Asynchronous Communication]]
4. [[REST vs gRPC]]

## Prerequisites
- None - this is the starting module.

## Related
- [[Microservices Index|Microservices]]
- Next: [[Service Discovery and Config Index|Service Discovery and Config]]

## Quick Revision
- Split for independent scaling/deploy, not by default. Sync (REST/gRPC) couples in time; async (Kafka) decouples. REST for reach, gRPC for internal performance.
