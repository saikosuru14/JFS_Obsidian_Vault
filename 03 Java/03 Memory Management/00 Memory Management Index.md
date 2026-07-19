---
title: Memory Management Index
aliases:
  - Memory Management Index
domain: Java
module: Memory Management
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 0
tags:
  - java
  - index
related:
  - "[[Java Index|Java]]"
  - "[[Java Memory Model]]"
  - "[[Stack Memory]]"
  - "[[Heap Memory]]"
  - "[[Garbage Collection Overview]]"
  - "[[Memory Leaks in Java]]"
---

# Memory Management

> Module index - part of the [[Java Index|Java]] learning path.

## Overview
The JVM manages memory automatically across a few distinct regions: per-thread **stacks**, the shared **heap** (where objects live and GC operates), and off-heap **Metaspace** (class metadata). Garbage collection reclaims unreachable objects; understanding generations and collectors is key to tuning latency and throughput.

## Branches (expand each)
- **[[Java Memory Model]]** — visibility/ordering rules for threads (the concurrency contract).
- **[[Stack Memory]]** — per-thread frames, locals, method calls.
- **[[Heap Memory]]** — shared object store -> [[Young Generation]], [[Old Generation]].
- **[[Metaspace]]** — off-heap class metadata (replaced PermGen).
- **[[Garbage Collection Overview]]** — reclaiming memory -> [[G1 GC]], [[ZGC]], [[Shenandoah GC]].
- **[[Memory Leaks in Java]]** — why GC'd languages still leak.

## Learning Roadmap
1. [[Java Memory Model]]
2. [[Stack Memory]] -> [[Heap Memory]] -> [[Young Generation]] -> [[Old Generation]] -> [[Metaspace]]
3. [[Garbage Collection Overview]] -> [[G1 GC]] -> [[ZGC]] -> [[Shenandoah GC]]
4. [[Memory Leaks in Java]]

## Prerequisites
- [[JVM Internals Index|JVM Internals]]

## Next
- [[Core Java Index|Core Java]]

## Related Modules
- [[Java Index|Java]] · [[Concurrency Index|Concurrency]]

## Quick Revision
- Regions: stack (per-thread), heap (shared, GC'd), Metaspace (off-heap classes). Objects age young -> old. Pick a collector by latency vs throughput. GC doesn't stop leaks from lingering references.
