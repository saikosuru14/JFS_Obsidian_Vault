---
title: Garbage Collection Overview
aliases:
  - Garbage Collection Overview
  - Garbage Collection
domain: Java
module: Memory Management
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 7
tags:
  - java
related:
  - "[[Memory Management Index|Memory Management]]"
  - "[[G1 GC]]"
  - "[[ZGC]]"
  - "[[Shenandoah GC]]"
---

# Garbage Collection

## Overview
Garbage collection automatically reclaims memory held by unreachable objects. Reachability is determined from **GC roots** (stack references, statics, JNI); anything not reachable is garbage. This note is the sub-hub for the collectors.

## Why It Matters
Choosing and tuning the collector trades **throughput** against **pause time**. It's the single biggest lever for latency-sensitive JVM services, and a constant interview theme.

## How It Works (mark-sweep-compact)
1. **Mark** — trace live objects from GC roots.
2. **Sweep** — reclaim unmarked objects.
3. **Compact** — move survivors together to remove fragmentation.
Generational collectors apply this per region (cheap Minor GC on Young, costlier Major GC on Old). "**Stop-the-world (STW)**" pauses all app threads during certain phases.

## The Collectors
| Collector | Focus | Use when |
|-----------|-------|----------|
| Serial | single-thread, small heaps | tiny apps / containers |
| Parallel | max throughput | batch jobs, throughput over latency |
| **[[G1 GC]]** | balanced, predictable pauses | default for most services |
| **[[ZGC]]** | ultra-low pause, huge heaps | large heap, latency-critical |
| **[[Shenandoah GC]]** | low pause, concurrent compaction | latency-critical (OpenJDK) |

## Key Concepts
- **Throughput** = % time doing app work; **latency** = pause length.
- **STW** — unavoidable for some phases; modern collectors minimize it by working concurrently.
- **Reference types** — strong / soft (cache) / weak (`WeakHashMap`) / phantom (cleanup) affect reclaim timing.

## Interview Questions
- **What is Stop-The-World?** A pause where all application threads halt so GC can work safely.
- **Can Java still leak memory?** Yes — objects that are reachable but never used aren't garbage (see [[Memory Leaks in Java]]).
- **Throughput vs low-pause collector?** Parallel maximizes total work; G1/ZGC/Shenandoah minimize pause length.

## Related Topics
- [[G1 GC]] · [[ZGC]] · [[Shenandoah GC]] · [[Memory Leaks in Java]]

## Quick Revision
- Reclaims unreachable objects from GC roots via mark-sweep-compact. Trade throughput vs pause. Serial/Parallel/G1/ZGC/Shenandoah. STW = all app threads paused.
