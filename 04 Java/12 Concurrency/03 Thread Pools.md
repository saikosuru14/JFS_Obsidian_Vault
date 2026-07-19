---
title: Thread Pools
aliases:
  - Thread Pools
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - java
related:
  - "[[Executor Framework]]"
---

# Thread Pools

## Overview
A thread pool reuses a fixed set of worker threads to run many tasks from a shared queue, capping resource use and removing per-task thread creation cost. `ThreadPoolExecutor` is the engine behind the `Executors` factories.

## Why It Matters
Unbounded thread creation exhausts memory and CPU; a pool provides back-pressure and predictable behavior. Interviewers probe the constructor parameters because the defaults are dangerous.

## ThreadPoolExecutor Parameters
```java
new ThreadPoolExecutor(
    corePoolSize,      // threads kept alive even when idle
    maximumPoolSize,   // upper bound when the queue is full
    keepAliveTime,     // idle timeout for threads above core
    unit,
    workQueue,         // e.g. new ArrayBlockingQueue<>(1000)  (BOUNDED)
    threadFactory,     // name your threads
    rejectionHandler); // what to do when saturated
```
Growth order: fill core -> queue -> up to max -> reject.

## Factory Methods (know the traps)
- `newFixedThreadPool(n)` / `newSingleThreadExecutor` — **unbounded** `LinkedBlockingQueue` -> OOM risk under overload.
- `newCachedThreadPool()` — **unbounded thread count** -> can spawn thousands.
- `newScheduledThreadPool(n)` — delayed/periodic tasks.
- `newVirtualThreadPerTaskExecutor()` (Java 21) — one virtual thread per task for I/O.

## Rejection Policies
`AbortPolicy` (default, throws), `CallerRunsPolicy` (back-pressure onto caller), `DiscardPolicy`, `DiscardOldestPolicy`.

## Best Practices
- In production, construct `ThreadPoolExecutor` directly with a **bounded queue** and an explicit rejection policy.
- Size: CPU-bound ~ number of cores; I/O-bound = cores x (1 + wait/compute), or use virtual threads.
- Name threads via a `ThreadFactory` for debuggable dumps.

## Interview Questions
- **Why avoid `newFixedThreadPool` in production?** Its unbounded queue hides overload and can OOM instead of applying back-pressure.
- **What happens when core is full?** Tasks queue; only when the queue is full do new threads spin up to max, then rejection kicks in.
- **CallerRunsPolicy use?** Natural throttling — the submitting thread runs the task, slowing producers.

## Related Topics
- [[Executor Framework]] · [[Callable & Future]] · [[ForkJoinPool]] · [[Virtual Threads]]

## Quick Revision
- Reuse workers over a queue. Order: core -> queue -> max -> reject. Use bounded queues + explicit rejection in prod; the default factories are unbounded.
