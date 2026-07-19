---
title: Retry
aliases:
  - Retry
domain: Microservices
module: Resilience
status: Not Started
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 3
tags:
  - microservices
---

# Retry

Automatically retries transient failures.

Configure:
- maxAttempts
- waitDuration

Avoid retrying non-idempotent operations blindly.