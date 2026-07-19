---
title: try-catch-finally and try-with-resources
aliases:
  - try-catch-finally and try-with-resources
  - try-with-resources
domain: Java
module: Exception Handling
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - java
  - exceptions
related:
  - "[[Checked vs Unchecked Exceptions]]"
  - "[[Exception Handling Best Practices]]"
---

# try-catch-finally and try-with-resources

## Overview
`try/catch/finally` handles exceptions and guarantees cleanup. `try-with-resources` (Java 7+) auto-closes resources implementing `AutoCloseable`, replacing error-prone `finally` blocks.

## How It Works
- `finally` always runs (except `System.exit`/JVM crash) — even on `return`.
- `try-with-resources` closes resources in **reverse** order of declaration, before any `catch`/`finally`.
- Exceptions thrown during close are **suppressed** (accessible via `getSuppressed()`), not lost.

## Example
```java
// try-with-resources: no explicit finally needed
try (var in = Files.newBufferedReader(path)) {
    return in.readLine();
} catch (IOException e) {
    throw new UncheckedIOException(e);   // keep the cause
}
```

## Performance
- `try` blocks are effectively free when no exception is thrown; throwing/filling stack traces is expensive. Don't use exceptions for control flow.

## Best Practices
- Prefer `try-with-resources` for anything closeable (streams, connections, locks via wrappers).
- Never `return` inside `finally` (it swallows exceptions and overrides returns).
- Keep `try` blocks small and specific.

## Common Mistakes
- Closing resources manually in `finally` and leaking on exception in the close.
- Empty `catch` blocks; logging *and* rethrowing (double logging).

## Interview Questions
- Does `finally` run after a `return` in `try`? (Yes.)
- What are suppressed exceptions?
- Why is `try-with-resources` preferred over `finally`?

## Related Topics
- [[Checked vs Unchecked Exceptions]]
- [[Exception Handling Best Practices]]

## Quick Revision
- `finally` always runs; try-with-resources auto-closes (reverse order) and suppresses close errors. Don't return in finally.
