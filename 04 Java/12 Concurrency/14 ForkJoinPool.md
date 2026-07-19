---
title: ForkJoinPool
aliases:
  - ForkJoinPool
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 14
tags:
  - java
related:
  - "[[Executor Framework]]"
---

# ForkJoinPool

## Overview
`ForkJoinPool` implements divide-and-conquer parallelism using **work-stealing**: each worker has its own deque; idle workers steal tasks from the tail of busy workers' deques, keeping all cores busy.

## Why It Matters
It powers parallel streams and `CompletableFuture`'s default async execution. Understanding work-stealing explains why parallel streams shine for CPU-bound splittable work and hurt for blocking I/O.

## How It Works
Split a task recursively until subtasks are small enough, compute, then combine:

```java
class SumTask extends RecursiveTask<Long> {
    protected Long compute() {
        if (size <= THRESHOLD) return computeDirectly();
        SumTask left = new SumTask(...);
        left.fork();                    // schedule async
        long right = new SumTask(...).compute();
        return left.join() + right;     // wait + combine
    }
}
```

- `RecursiveTask<V>` returns a value; `RecursiveAction` returns void.
- `fork()` submits to the current worker's deque; `join()` waits for the result.

## Common Pool
`ForkJoinPool.commonPool()` (size = cores - 1) backs `parallelStream()` and default `CompletableFuture` async stages — a shared, JVM-wide resource.

## Best Practices
- Only for CPU-bound, splittable work. Blocking I/O starves the pool and stalls parallel streams elsewhere.
- Pick a threshold so subtasks are meaningful but numerous enough to balance load.
- For blocking tasks, use a dedicated executor or virtual threads, not the common pool.

## Interview Questions
- **What is work-stealing?** Idle workers take tasks from other workers' deques to stay busy, improving load balance.
- **Why avoid blocking in the common pool?** It's shared and small; a blocked task stalls parallel streams and CompletableFutures app-wide.
- **RecursiveTask vs RecursiveAction?** Returns a result vs returns void.

## Related Topics
- [[Executor Framework]] · [[Thread Pools]] · [[CompletableFuture]]

## Quick Revision
- Divide-and-conquer + work-stealing deques. RecursiveTask/Action, fork/join. Backs parallel streams. CPU-bound only; never block the common pool.
