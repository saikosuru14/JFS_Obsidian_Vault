---
title: Performance Profiling
aliases:
  - Performance Profiling
domain: Java
module: JVM Performance
status: Learning
difficulty: Medium
priority: High
interview: 3
revision: Weekly
order: 4
tags:
  - java
  - performance
related:
  - "[[GC Tuning]]"
  - "[[JIT Compilation]]"
---

# Performance Profiling

## Overview
Profiling finds *where* time and memory actually go. Measure before optimizing — intuition about hotspots is usually wrong.

## Tools
- **JFR (Java Flight Recorder)** + **JDK Mission Control** — low-overhead production profiling (CPU, allocation, locks, GC).
- **async-profiler** — flame graphs for CPU and allocations with minimal bias.
- **JMH** — microbenchmarking done correctly (warmup, forks, dead-code elimination).
- **Heap dumps** (`jmap`) + Eclipse MAT — find leaks and dominators.
- **jstack / thread dumps** — diagnose contention and deadlocks.

## Workflow
1. Establish a baseline metric (latency p99, throughput).
2. Profile under realistic load (JFR/async-profiler).
3. Find the dominant cost (CPU hotspot, allocation, lock contention, GC).
4. Fix one thing; re-measure; confirm improvement.

## What To Look For
- High allocation rate → GC pressure (reduce object churn).
- Lock contention → see [[Synchronization]], [[Locks]].
- Hot methods not inlined → see [[JIT Compilation]].

## Common Mistakes
- Optimizing without profiling.
- Microbenchmarking without JMH (misleading due to JIT/DCE).
- Profiling a cold JVM.

## Interview Questions
- How do you find a CPU hotspot in production?
- Difference between sampling and instrumenting profilers?
- Why use JMH for microbenchmarks?

## Related Topics
- [[GC Tuning]] · [[JIT Compilation]] · [[Memory Leaks in Java]]

## Quick Revision
- Measure first: JFR/async-profiler in prod, JMH for micro, MAT for heaps. Fix the dominant cost, then re-measure.
