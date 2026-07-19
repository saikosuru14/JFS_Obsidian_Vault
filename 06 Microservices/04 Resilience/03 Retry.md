---
title: Retry
aliases:
  - Retry
domain: Microservices
module: Resilience
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 3
tags:
  - microservices
related:
  - "[[Resilience4j]]"
  - "[[Circuit Breaker]]"
---

# Retry

## Overview
Retry automatically re-attempts a call that failed with a **transient** error (timeout, brief network blip, 503). It buys reliability for temporary faults — but only for operations that are safe to repeat.

## Why It Matters
Naive retries make outages worse (retry storms) and can duplicate side effects. Doing retries correctly — idempotency, backoff, jitter, and coordination with the circuit breaker — is the real skill.

## Rules For Safe Retries
- **Only retry idempotent operations** (GET, or writes protected by [[Idempotency]] keys). Never blindly retry a non-idempotent POST that charges a card.
- **Exponential backoff + jitter** — spread retries to avoid synchronized retry storms.
- **Cap attempts** and total time; then fail or fall back.
- **Retry only retryable errors** (5xx/timeouts), not 4xx (client errors won't fix themselves).

## Config (Resilience4j)
```yaml
resilience4j:
  retry:
    instances:
      svc:
        maxAttempts: 3
        waitDuration: 200ms
        enableExponentialBackoff: true
        retryExceptions: [java.io.IOException]
        ignoreExceptions: [com.app.BadRequestException]
```

## Interaction With Circuit Breaker
Combine so Retry wraps the [[Circuit Breaker]]: retries stop once the breaker opens, preventing hammering a dead dependency.

## Interview Questions
- **When is it unsafe to retry?** Non-idempotent operations, or on 4xx client errors.
- **Why backoff and jitter?** To avoid synchronized retry storms that amplify an outage.
- **How do retry and circuit breaker interact?** The breaker short-circuits once open, so retries don't pile onto a failing service.

## Related Topics
- [[Circuit Breaker]] · [[Idempotency]] · [[Resilience4j]]

## Quick Revision
- Re-attempt transient failures — idempotent ops only, exponential backoff + jitter, cap attempts, retry only retryable errors. Wrap the circuit breaker so retries stop when it opens.
