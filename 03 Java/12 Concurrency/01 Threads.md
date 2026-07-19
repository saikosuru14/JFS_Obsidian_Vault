---
title: Threads
aliases:
  - Threads
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - java
related:
  - "[[Concurrency Index|Concurrency]]"
  - "[[Thread Lifecycle]]"
  - "[[Race Conditions]]"
---

# Threads

## Overview
A thread is the smallest unit of scheduling within a process. Each thread has its own stack and program counter but shares the process heap, so all threads see the same objects — which is exactly why coordination is hard.

## Why It Matters
Threads are the foundation of every concurrency abstraction (pools, futures, parallel streams). Understanding cost and creation models drives every downstream design choice.

## How It Works
Three ways to define work for a thread:
- **Extend `Thread`** — couples task to thread; wastes the single-inheritance slot. Avoid.
- **Implement `Runnable`** — task is decoupled from execution; the preferred low-level option.
- **`Callable` + `ExecutorService`** — returns a value and can throw checked exceptions; the production default.

```java
Runnable task = () -> System.out.println("run on " + Thread.currentThread().getName());
Thread t = new Thread(task);
t.start();   // schedules and calls run() on a NEW thread
t.join();    // caller waits for completion
```

`start()` creates a new call stack; calling `run()` directly just executes on the current thread — a classic mistake.

## Platform vs Virtual
Each platform thread maps 1:1 to an OS thread (~1 MB stack), so you can only have a few thousand. [[Virtual Threads]] (Java 21+) are cheap and scale to millions for I/O work.

## Best Practices
- Never subclass `Thread` for business logic; submit tasks to an [[Executor Framework|executor]].
- Name your threads (via a `ThreadFactory`) for readable stack traces.
- Always handle `InterruptedException` — restore the flag with `Thread.currentThread().interrupt()`.

## Common Mistakes
- Calling `run()` instead of `start()`.
- Swallowing `InterruptedException`.
- Creating a raw `new Thread()` per request instead of pooling.

## Interview Questions
- **Why prefer `Runnable`/`Callable` over extending `Thread`?** Decouples the task from the execution mechanism, keeps inheritance free, and works directly with executors.
- **`start()` vs `run()`?** `start()` schedules a new thread; `run()` executes synchronously on the caller.
- **What does interrupting a thread do?** Sets a flag / throws `InterruptedException` in blocking calls; it is cooperative, not a forced kill.

## Related Topics
- [[Thread Lifecycle]] · [[Race Conditions]] · [[Executor Framework]] · [[Virtual Threads]]

## Quick Revision
- Thread = own stack, shared heap. Prefer `Runnable`/`Callable` + executors. `start()` not `run()`. Interruption is cooperative.
