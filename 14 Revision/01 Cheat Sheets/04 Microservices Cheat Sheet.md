---
title: Microservices Cheat Sheet
aliases:
  - Microservices Cheat Sheet
domain: Revision
module: Cheat Sheets
status: Learning
difficulty: Hard
priority: High
interview: 5
revision: Weekly
order: 4
tags:
  - revision
  - microservices
---

# Microservices Cheat Sheet

> Interview-ready revision for [[Microservices]] (4–5 YOE). Concepts, code, tables, and Q&A with answers.

---

## 1. Fundamentals
Independently deployable services, each owning its data and communicating over the network. Adopt them for **independent scaling/deployment and team autonomy** — not by default (they add distributed-systems complexity).

- **Boundaries:** model around business capabilities / DDD bounded contexts, not technical layers. A service owns its schema (no shared DB).
- **Monolith vs microservices:** start monolith; split when scaling/team/deploy pain justifies the operational cost.

| Communication | When | Trade-off |
|---------------|------|-----------|
| Sync REST | simple request/response | tight coupling, latency adds up, cascading failures |
| Sync gRPC | low-latency internal, streaming | binary/proto, HTTP/2 |
| Async (Kafka/queue) | events, decoupling, spikes | eventual consistency, harder debugging |

Rule of thumb: **queries** sync, **state changes/side-effects** async where possible.

---

## 2. Service Discovery & Config
- **Discovery:** services register with Eureka/Consul; clients resolve logical names → instances (client-side LB). In k8s, this is native (Services + DNS) — often no Eureka needed.
- **Centralized config:** Spring Cloud Config / Consul; externalize per-environment config, refreshable without redeploy (`/actuator/refresh`, bus).

---

## 3. API Gateway & Routing
Single entry point for cross-cutting concerns: routing, auth/token validation, rate limiting, TLS termination, aggregation.
- **Spring Cloud Gateway** (reactive) routes + filters. A **BFF** (backend-for-frontend) tailors APIs per client.
- Internal calls: **OpenFeign** declarative clients + client-side load balancing.

```java
@FeignClient(name = "inventory")
interface InventoryClient {
    @GetMapping("/stock/{sku}")
    StockDto stock(@PathVariable String sku);
}
```

---

## 4. Resilience (interview-heavy)
A slow/failing dependency must not take down the caller. Combine patterns (Resilience4j):

| Pattern | Purpose |
|---------|---------|
| Timeout | never block indefinitely |
| Retry (backoff + jitter) | transient faults; only for **idempotent** ops |
| Circuit breaker | stop hammering a failing dependency (closed→open→half-open) |
| Bulkhead | isolate resource pools so one dep can't exhaust threads |
| Rate limiter | protect from overload |
| Fallback | graceful degradation |

```java
@CircuitBreaker(name = "inventory", fallbackMethod = "fromCache")
@Retry(name = "inventory")
public Stock get(String sku) { return client.stock(sku); }
public Stock fromCache(String sku, Throwable t) { return cache.get(sku); }
```

---

## 5. Distributed Data & Transactions
No 2PC across services (blocking, poor availability). Use the **Saga** pattern — a sequence of local transactions with compensating actions.

- **Orchestration** (central coordinator drives steps; easier to reason/monitor) vs **Choreography** (services react to events; looser coupling, harder to trace).
- **Outbox pattern:** write the domain change + event to an outbox table in the **same local transaction**, then a relay publishes to the broker → reliable "exactly-once-ish" publishing (no dual-write problem).
- **Idempotency:** consumers must dedupe (idempotency key / processed-id table) because delivery is at-least-once.
- **Eventual consistency:** design UX for it; provide read-your-writes where needed.

---

## 6. Event-Driven
- Backbone is usually [[Apache Kafka|Kafka]]. Ordering only within a partition (key by aggregate id).
- **Event versioning:** evolve schemas with a registry (Avro/Protobuf, BACKWARD compatibility). **DLQ** for poison messages; retry topics with backoff.
- Prefer **event-carried state transfer** or thin events + query, depending on coupling/latency needs.

---

## 7. Observability (non-negotiable at scale)
- **Distributed tracing** (OpenTelemetry / Micrometer Tracing → Jaeger/Zipkin): propagate a trace/correlation ID across every hop.
- **Centralized logging** (ELK/Loki) with the correlation ID in every log line.
- **Metrics** (Micrometer → Prometheus + Grafana): RED (Rate, Errors, Duration) per service; alert on SLOs.
- Health: liveness/readiness endpoints wired to the orchestrator.

---

## 8. Deployment
Containerize ([[Docker]]) → orchestrate ([[Kubernetes]]) → automate ([[CI-CD]]). Independent pipelines per service; contract testing (Pact) to catch breaking API changes; blue-green/canary rollouts.

---

## 9. Interview Q&A (with answers)

**Q: When should you NOT use microservices?**
A: Small teams/products, unclear domain boundaries, or when you can't invest in automation/observability. Distributed systems add latency, partial failure, and operational overhead — a modular monolith is often better first.

**Q: How do you handle a transaction spanning services?**
A: Avoid distributed 2PC. Use a Saga (orchestration or choreography) with compensating transactions, and the Outbox pattern for reliable event publishing. Accept eventual consistency.

**Q: How do you make async consumers safe?**
A: Delivery is at-least-once, so make processing idempotent — dedupe via an idempotency key or a processed-message table; use DLQ + retries for failures.

**Q: Circuit breaker states?**
A: Closed (calls pass, failures counted) → Open (calls fail fast / fallback after threshold) → Half-Open (trial calls; success closes it, failure re-opens).

**Q: Orchestration vs choreography Saga?**
A: Orchestration uses a central coordinator — easier to monitor and reason about, but a coupling point. Choreography is event-driven and loosely coupled but harder to trace and reason about end to end.

**Q: How do services find each other?**
A: A service registry (Eureka/Consul) with client-side load balancing, or platform-native discovery (Kubernetes Services + DNS).

**Q: How do you debug a request across services?**
A: Distributed tracing with a propagated correlation/trace ID, aggregated logs keyed by that ID, and per-service metrics/dashboards.

**Q: Shared database across services — why avoid it?**
A: It couples deployments and schemas, breaking independence. Each service owns its data; share via APIs/events.

---

## Revision Checklist
- [ ] When to use (and not use) microservices; DDD boundaries
- [ ] Sync vs async communication trade-offs
- [ ] Discovery + centralized config
- [ ] Gateway + Feign + client-side LB
- [ ] Resilience: timeout/retry/circuit breaker/bulkhead + Resilience4j
- [ ] Saga (orchestration vs choreography), Outbox, idempotency
- [ ] Event versioning + DLQ
- [ ] Tracing, correlation IDs, RED metrics
