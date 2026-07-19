---
title: Exception Handling Best Practices
aliases:
  - Exception Handling Best Practices
domain: Java
module: Exception Handling
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 5
tags:
  - java
  - exceptions
related:
  - "[[Custom Exceptions]]"
  - "[[try-catch-finally and try-with-resources]]"
---

# Exception Handling Best Practices

## Overview
Practical rules for exception handling in production Java services.

## Rules
- **Fail fast** on programming errors — throw `IllegalArgumentException`/`IllegalStateException` early.
- **Catch where you can act.** Otherwise let it propagate to a boundary (controller, message listener).
- **Never swallow.** No empty `catch`. If you truly ignore, comment why.
- **Preserve the cause** when wrapping: `throw new ServiceException("...", e)`.
- **Log once**, at the boundary — not at every layer (avoids duplicate stack traces).
- **Don't use exceptions for control flow** — they're expensive and obscure intent.
- **Clean up with try-with-resources**, not manual `finally`.
- **Translate** low-level exceptions into domain exceptions at layer boundaries.

## Spring / Web Boundary
- Use a global handler (`@ControllerAdvice` + `@ExceptionHandler`) to map exceptions to HTTP responses.
- Return a consistent error body (code, message, traceId); never leak stack traces to clients.

## Common Mistakes
- Logging and rethrowing the same exception (double logging).
- Catching `Exception` broadly deep in the stack.
- Losing the original cause.

## Interview Questions
- How do you structure exception handling across layers?
- Where should you log exceptions and why?
- How do you expose errors from a REST API safely?

## Related Topics
- [[Custom Exceptions]]
- [[try-catch-finally and try-with-resources]]
- [[Exception Handling]] (Spring)

## Quick Revision
- Fail fast, catch where you can act, preserve cause, log once at the boundary, translate to domain errors, don't use exceptions for control flow.
