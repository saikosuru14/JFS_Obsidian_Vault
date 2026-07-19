---
title: Old Generation
aliases:
  - Old Generation
  - Tenured Generation
domain: Java
module: Memory Management
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 5
tags:
  - java
related:
  - "[[Heap Memory]]"
  - "[[Young Generation]]"
---

# Old Generation

## Overview
The Old (Tenured) Generation holds long-lived objects promoted from the [[Young Generation]] after surviving several Minor GCs. It is larger and collected less often, but its collection (**Major / Full GC**) is more expensive.

## Why It Matters
Long, frequent Old-Gen collections are the usual cause of latency spikes. The goal of tuning is to keep genuinely long-lived data here and stop short-lived garbage from being promoted.

## How It Works
- Filled by **promotion** from Survivor spaces (age threshold reached) or direct allocation of large objects.
- **Major GC** reclaims dead objects here; often involves marking + compaction to reduce fragmentation.
- Modern collectors (G1, ZGC, Shenandoah) do much of this **concurrently** to shrink pauses.

## Failure Modes
- **`OutOfMemoryError: Java heap space`** — Old Gen full of reachable objects (real growth or a [[Memory Leaks in Java|leak]]).
- **Promotion failure / concurrent mode failure** — Old Gen can't accept promotions fast enough, forcing a costly Full GC.

## Interview Questions
- **Minor vs Major vs Full GC?** Minor = Young Gen; Major = Old Gen; Full = entire heap (+ Metaspace), the most expensive.
- **Why is Old Gen GC expensive?** It's larger, holds live data, and typically needs marking + compaction.
- **How to reduce Old-Gen pressure?** Prevent premature promotion (size Young/Survivor), reduce long-lived allocations, tune the collector.

## Related Topics
- [[Young Generation]] · [[Heap Memory]] · [[Garbage Collection Overview]] · [[Memory Leaks in Java]]

## Quick Revision
- Long-lived promoted objects. Collected by Major/Full GC - larger, rarer, costlier. Prevent premature promotion to avoid latency spikes.
