---
title: REST vs gRPC
aliases:
  - REST vs gRPC
domain: Microservices
module: Fundamentals
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 4
tags:
  - microservices
related:
  - "[[Synchronous vs Asynchronous Communication]]"
---

# REST vs gRPC

## Overview
Both are synchronous request/response protocols. **REST** uses HTTP/1.1 + JSON and is universal and human-readable. **gRPC** uses HTTP/2 + Protocol Buffers (binary) with generated strongly-typed stubs and streaming.

## Why It Matters
The default for external/public APIs is REST; for high-throughput internal service-to-service calls, gRPC is often faster and safer. Knowing the trade-offs signals real-world experience.

## Comparison
| | REST | gRPC |
|--|------|------|
| Transport | HTTP/1.1 | HTTP/2 (multiplexed) |
| Payload | JSON (text) | Protobuf (binary, compact) |
| Contract | OpenAPI (optional) | `.proto` (enforced) |
| Streaming | limited (SSE/polling) | bi-directional streaming |
| Browser support | native | needs gRPC-Web proxy |
| Readability | human-readable | binary |
| Performance | good | higher throughput, lower latency |

## When To Use Which
- **REST**: public APIs, browser clients, broad interoperability, simple CRUD.
- **gRPC**: internal microservice calls, low-latency/high-volume, polyglot services with strict contracts, streaming.

## Notes
- gRPC's `.proto` gives compile-time contracts and easy versioning (add fields, keep tags).
- REST's ubiquity, caching (HTTP), and tooling make it the safer default externally.

## Interview Questions
- **When is gRPC preferable to REST?** Internal, high-throughput, low-latency calls; streaming; strict cross-language contracts.
- **Why is gRPC faster?** HTTP/2 multiplexing + compact binary Protobuf vs text JSON over HTTP/1.1.
- **Why still use REST?** Universality, browser support, human-readability, HTTP caching, and mature tooling.

## Related Topics
- [[Synchronous vs Asynchronous Communication]] · [[API Gateway]] · [[OpenFeign]]

## Quick Revision
- REST = HTTP/JSON, universal, external default. gRPC = HTTP/2 + Protobuf, fast, streaming, strong contracts, internal default. Choose by audience + performance.
