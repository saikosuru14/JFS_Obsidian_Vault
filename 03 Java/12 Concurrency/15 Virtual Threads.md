---
title: Virtual Threads
aliases:
  - Virtual Threads
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 15
tags:
  - java
related:
  - "[[Concurrency Index|Concurrency]]"
  - "[[Threads]]"
---

# Virtual Threads

## Overview
Virtual threads (Project Loom, stable in **Java 21**) are lightweight threads managed by the JVM, not the OS. Many virtual threads are multiplexed onto a small pool of platform (carrier) threads, so you can run millions concurrently.

## Why It Matters
They make the simple **thread-per-request** blocking style scale like async/reactive code — without callback complexity. This is a hot senior-interview topic.

## How It Works
When a virtual thread blocks (I/O, lock, sleep), the JVM **unmounts** it from its carrier thread and mounts another runnable virtual thread. Blocking is cheap because it parks the virtual thread, not an OS thread.

```java
Thread.startVirtualThread(() -> handle(request));

try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
    IntStream.range(0, 1_000_000)
             .forEach(i -> executor.submit(() -> callService()));
}   // one virtual thread per task - fine at this scale
```

## Platform vs Virtual
| | Platform thread | Virtual thread |
|--|-----------------|----------------|
| Backing | 1:1 OS thread | Multiplexed on carriers |
| Cost | ~1 MB stack | ~few KB, cheap |
| Count | thousands | millions |
| Best for | CPU-bound | blocking I/O |

## Gotchas
- **Don't pool them** — create one per task; pooling defeats the purpose.
- **Pinning**: a virtual thread inside a `synchronized` block (or native call) can't unmount, pinning its carrier. Prefer `ReentrantLock` in hot paths (largely mitigated in later releases).
- No throughput gain for pure CPU-bound work — that's still bounded by cores.

## Interview Questions
- **Virtual vs platform threads?** Virtual are JVM-scheduled, ultra-cheap, multiplexed onto carriers; ideal for blocking I/O at massive scale.
- **Why not pool virtual threads?** They're cheap to create; pooling adds contention and limits concurrency for no benefit.
- **What is pinning?** A virtual thread stuck to its carrier (e.g., inside `synchronized`), preventing unmount and reducing scalability.

## Related Topics
- [[Threads]] · [[Thread Pools]] · [[Executor Framework]]

## Quick Revision
- Java 21 lightweight threads multiplexed on carriers. Millions for blocking I/O; one per task, don't pool. Watch pinning in synchronized blocks; no CPU-bound gain.
