---
title: Distributed Tracing
aliases:
  - Distributed Tracing
domain: Microservices
module: Observability
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - microservices
related:
  - "[[Observability Index|Observability]]"
  - "[[Centralized Logging]]"
---

# Distributed Tracing

## Overview
Distributed tracing follows a single request as it flows across services, recording the timing of each hop. A **trace** is the whole journey; each unit of work is a **span**; a **trace id** ties them together and is propagated across service calls.

## Why It Matters
It answers "where did the latency/error come from?" in a request that touched 8 services — impossible from isolated logs. It's the observability pillar most specific to microservices.

## Key Concepts
- **Trace id** — unique per request, propagated end-to-end.
- **Span** — one operation (a service call, a DB query) with start/end + tags; spans nest via **parent span id**.
- **Context propagation** — trace/span ids passed in headers (**W3C `traceparent`**, or B3) across HTTP/messaging.
- **Sampling** — record a fraction of traces to control overhead (head vs tail sampling).

## Tooling
- **OpenTelemetry (OTel)** — vendor-neutral standard for generating/exporting traces (and metrics/logs).
- Backends: **Jaeger**, **Zipkin**, Tempo, vendor APMs.
- Spring: **Micrometer Tracing** (successor to Spring Cloud Sleuth) auto-instruments and propagates context.

## Best Practices
- Propagate trace context through [[OpenFeign]]/RestClient and Kafka headers (including [[Choreography Saga|choreographed]] flows).
- Put the trace id in logs (MDC) to join traces with [[Centralized Logging|logs]].
- Sample sensibly; always keep error traces.

## Interview Questions
- **Trace vs span?** A trace is the full request journey; a span is one operation within it (spans nest).
- **How is context propagated?** Via headers (W3C traceparent / B3) across sync and async hops.
- **What tools?** OpenTelemetry + Jaeger/Zipkin; Micrometer Tracing in Spring.

## Related Topics
- [[Centralized Logging]] · [[Health Checks]] · [[OpenFeign]]

## Quick Revision
- Follow a request across services: trace id + nested spans, propagated via headers (W3C traceparent). OpenTelemetry -> Jaeger/Zipkin; Micrometer Tracing in Spring. Sample, keep errors, log the trace id.
