---
title: Callable & Future
aliases:
  - "Callable & Future"
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 11
tags:
  - java
related:
  - "[[Executor Framework]]"
  - "[[CompletableFuture]]"
---

# Callable & Future

## Overview
`Callable<V>` is a task that returns a value and may throw a checked exception (unlike `Runnable`). Submitting it to an executor returns a `Future<V>` — a handle to the eventual result.

## Why It Matters
It's the basic request/response model for async work: fire a task, do other things, collect the result later.

## How It Works
```java
ExecutorService pool = Executors.newFixedThreadPool(4);
Future<Integer> f = pool.submit(() -> heavyCompute());   // Callable
// ... do other work ...
Integer result = f.get(2, TimeUnit.SECONDS);             // blocks (with timeout)
```

`Future` methods:
- `get()` — blocks until done; `get(timeout)` throws `TimeoutException`.
- `cancel(mayInterrupt)` — attempts cancellation.
- `isDone()` / `isCancelled()`.

## Limitations
`Future` is **blocking and non-composable**: you can't chain "when done, do X" or combine several without blocking on `get()`. That gap is exactly what [[CompletableFuture]] fills.

## Exceptions
A task exception is wrapped and rethrown as `ExecutionException` from `get()`; unwrap with `getCause()`.

## Interview Questions
- **Callable vs Runnable?** Callable returns a value and can throw checked exceptions; Runnable returns void.
- **Why is plain Future limited?** No non-blocking completion callbacks or composition — you must block on `get()`.
- **What does `get()` do while the task runs?** Blocks the calling thread until the result (or timeout/exception).

## Related Topics
- [[CompletableFuture]] · [[Executor Framework]] · [[Thread Pools]]

## Quick Revision
- Callable returns a value/throws checked; submit -> Future. Future.get() blocks and can't compose -> use CompletableFuture.
