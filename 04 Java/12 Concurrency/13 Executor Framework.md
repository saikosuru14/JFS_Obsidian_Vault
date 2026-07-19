---
title: Executor Framework
aliases:
  - Executor Framework
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 13
tags:
  - java
related:
  - "[[Concurrency Index|Concurrency]]"
  - "[[Thread Pools]]"
  - "[[Callable & Future]]"
  - "[[ForkJoinPool]]"
---

# Executor Framework

## Overview
The Executor framework (`java.util.concurrent`) decouples **task submission** from **task execution**. You submit `Runnable`/`Callable` tasks; the executor manages a pool of threads and a work queue. This note is the sub-hub for higher-level execution.

## Why It Matters
Creating a thread per task doesn't scale and gives no back-pressure. Executors bound resources, reuse threads, and return [[Callable & Future|futures]] — the production standard for concurrency.

## Core Interfaces
- **`Executor`** — `execute(Runnable)`.
- **`ExecutorService`** — adds `submit`, `invokeAll`, lifecycle (`shutdown`, `awaitTermination`).
- **`ScheduledExecutorService`** — delayed and periodic tasks.

```java
ExecutorService pool = Executors.newFixedThreadPool(8);
Future<Integer> f = pool.submit(() -> compute());
Integer result = f.get();
pool.shutdown();                       // stop accepting; finish queued work
pool.awaitTermination(30, TimeUnit.SECONDS);
```

## Lifecycle
- `shutdown()` — graceful: no new tasks, finishes queued ones.
- `shutdownNow()` — attempts to interrupt running tasks, returns pending ones.
- Always shut down pools; otherwise non-daemon threads keep the JVM alive.

## Best Practices
- Prefer a custom `ThreadPoolExecutor` over `Executors.newXxx` factories in production (see [[Thread Pools]]) for a bounded queue and named threads.
- Handle exceptions — a task that throws silently kills only itself; inspect via `Future.get()`.
- Size pools by workload: CPU-bound ~ cores; I/O-bound higher, or use [[Virtual Threads]].

## Interview Questions
- **Why executors over raw threads?** Reuse, bounded resources, back-pressure, and futures.
- **shutdown vs shutdownNow?** Graceful drain vs interrupt-and-return-pending.
- **What happens to an uncaught exception in a submitted task?** It's captured in the `Future` and rethrown as `ExecutionException` on `get()`.

## Related Topics
- [[Thread Pools]] · [[Callable & Future]] · [[CompletableFuture]] · [[ForkJoinPool]]

## Quick Revision
- Decouples submit from execute. ExecutorService = submit + lifecycle. Prefer custom bounded pools; always shut down.
