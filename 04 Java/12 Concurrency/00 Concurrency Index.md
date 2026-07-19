---
title: Concurrency Index
aliases:
  - Concurrency Index
domain: Java
module: Concurrency
status: Learning
difficulty: Medium
priority: High
interview: 3
revision: Weekly
order: 0
tags:
  - java
  - index
related:
  - "[[Java Index|Java]]"
  - "[[Threads]]"
  - "[[Synchronization]]"
  - "[[Executor Framework]]"
  - "[[Virtual Threads]]"
---

# Concurrency

> Module index - part of the [[Java Index|Java]] learning path.

## Overview
Java concurrency lets a program make progress on multiple tasks at once, using OS threads (and, since Java 21, virtual threads). The hard parts are **visibility** (do other threads see my write?), **atomicity** (is this update indivisible?), and **ordering** (can the JVM/CPU reorder my instructions?). The Java Memory Model (JMM) defines the rules; `java.util.concurrent` gives you the tools.

## Branches (expand each)
- **[[Threads]]** — the execution primitive: creation, lifecycle, race conditions.
- **[[Synchronization]]** — coordinating access to shared state: `volatile`, locks, atomics, deadlocks.
- **[[Executor Framework]]** — higher-level task execution: thread pools, futures, fork/join.
- **[[Virtual Threads]]** — lightweight threads for massive I/O concurrency (Java 21+).

## Learning Roadmap
1. [[Threads]] -> [[Thread Lifecycle]] -> [[Race Conditions]]
2. [[Synchronization]] -> [[volatile]] -> [[Locks]] -> [[ReentrantLock]] -> [[Atomic Classes]] -> [[Deadlocks in Java]]
3. [[Executor Framework]] -> [[Thread Pools]] -> [[Callable & Future]] -> [[CompletableFuture]] -> [[ForkJoinPool]]
4. [[Virtual Threads]]

## Prerequisites
- Core Java (objects, exceptions) and the [[Java Memory Model]] concepts.

## Next
- [[JVM Performance Index|JVM Performance]]

## Related Modules
- [[Java Index|Java]]

## Quick Revision
- Three problems: visibility, atomicity, ordering. Prefer `java.util.concurrent` (executors, atomics, concurrent collections) over hand-rolled `synchronized`. Interview questions and gotchas live in each topic note.
