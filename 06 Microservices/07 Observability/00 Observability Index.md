---
title: Observability Index
aliases:
  - Observability Index
domain: Microservices
module: Observability
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
  - "[[Distributed Tracing]]"
  - "[[Centralized Logging]]"
---

# Observability

> Module index - part of the [[Microservices Index|Microservices]] learning path.

## Overview
In a distributed system a single request touches many services, so you can't debug by reading one log file. Observability rests on three pillars — **logs**, **metrics**, and **traces** — that together answer "what happened, how much, and where." This module covers distributed tracing and centralized logging (metrics via Prometheus/Micrometer sit alongside them).

## The Three Pillars
- **Logs** — discrete events -> [[Centralized Logging]] (aggregate + search).
- **Metrics** — numeric time series (latency, error rate, throughput) -> Prometheus + Micrometer.
- **Traces** — a request's path across services -> [[Distributed Tracing]].

## Branches (expand each)
- **[[Distributed Tracing]]** — follow one request across service boundaries.
- **[[Centralized Logging]]** — aggregate logs with correlation ids.

## Learning Roadmap
1. [[Distributed Tracing]]
2. [[Centralized Logging]]

## Prerequisites
- [[Event-Driven Index|Event-Driven]]

## Related
- [[Microservices Index|Microservices]] · [[Health Checks]]

## Quick Revision
- Three pillars: logs, metrics, traces. Correlate with a trace/correlation id. Tracing shows the request path; centralized logging aggregates + searches; metrics quantify.
