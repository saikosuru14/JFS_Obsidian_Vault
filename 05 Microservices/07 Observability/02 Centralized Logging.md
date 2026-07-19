---
title: Centralized Logging
aliases:
  - Centralized Logging
domain: Microservices
module: Observability
status: Learning
difficulty: Medium
priority: High
interview: 3
revision: Weekly
order: 2
tags:
  - microservices
related:
  - "[[Observability Index|Observability]]"
  - "[[Distributed Tracing]]"
---

# Centralized Logging

## Overview
Centralized logging ships logs from every service instance to one searchable platform. With ephemeral containers and many instances, logging to local files is useless — you need aggregation, indexing, and correlation.

## Why It Matters
When a request spans services and pods restart constantly, the only way to investigate is a central store you can query by trace/correlation id and time range.

## How It Works
```
service -> stdout (structured JSON) -> collector (Fluent Bit / Logstash)
        -> store/index (Elasticsearch / Loki) -> query/dashboard (Kibana / Grafana)
```
Common stacks: **ELK/EFK** (Elasticsearch + Logstash/Fluentd + Kibana) or **Grafana Loki**.

## Best Practices
- **Structured logging** (JSON) — machine-parseable fields, not free text.
- **Correlation/trace id** on every line (MDC) to join with [[Distributed Tracing]] and stitch a request's logs.
- **Log to stdout** in containers; let the platform collect (12-Factor) — don't manage files in the app.
- **Consistent levels** and no sensitive data (PII, secrets, tokens).
- **Retention + sampling** for volume/cost; alert on error-rate spikes.

## Interview Questions
- **Why centralize logs?** Instances are ephemeral and requests span services; you need one searchable, correlated store.
- **How do you correlate logs across services?** A shared trace/correlation id on every log line (MDC), propagated with the request.
- **Common stack?** ELK/EFK or Grafana Loki; apps log structured JSON to stdout.

## Related Topics
- [[Distributed Tracing]] · [[Observability Index|Observability]] · [[Health Checks]]

## Quick Revision
- Ship structured (JSON) logs to a central store (ELK/EFK/Loki). Log to stdout, add a trace/correlation id (MDC), no secrets, set retention. Correlate with tracing.
