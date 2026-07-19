---
title: GC Tuning
aliases:
  - GC Tuning
domain: Java
module: JVM Performance
status: Learning
difficulty: Hard
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - java
  - performance
  - gc
related:
  - "[[Garbage Collection Overview]]"
  - "[[G1 GC]]"
  - "[[Performance Profiling]]"
---

# GC Tuning

## Overview
GC tuning balances **throughput**, **latency (pause time)**, and **footprint**. Pick a collector for your goal, size the heap, then measure — don't guess.

## Choosing a Collector
| Goal | Collector |
|------|-----------|
| Balanced default | [[G1 GC]] |
| Low pause, large heaps | [[ZGC]] / [[Shenandoah GC]] |
| Max throughput (batch) | Parallel GC |

## Key Flags
```
-Xms / -Xmx           # set equal to avoid resize pauses
-XX:+UseG1GC          # collector selection
-XX:MaxGCPauseMillis  # G1 pause target
-Xlog:gc*             # GC logging (Java 9+)
```

## How To Tune
1. Set a clear SLO (e.g., p99 pause < 50 ms).
2. Enable GC logs; analyze with GCViewer / GCeasy.
3. Size the heap so live set fits comfortably; set `-Xms == -Xmx`.
4. Change one thing at a time; measure under realistic load.

## Common Mistakes
- Tuning flags before fixing allocation rate (the real driver of GC frequency).
- Oversized heaps causing long pauses; undersized heaps causing constant GC.
- Copy-pasting flags without measuring.

## Best Practices
- Reduce allocations first (object churn) — see [[Memory Leaks in Java]] and [[Escape Analysis]].
- Prefer modern low-pause collectors (ZGC/Shenandoah) for latency-sensitive services.

## Interview Questions
- How do you choose a GC for a low-latency service?
- What drives GC frequency? (allocation rate)
- Why set `-Xms == -Xmx`?

## Related Topics
- [[Garbage Collection Overview]] · [[G1 GC]] · [[ZGC]] · [[Performance Profiling]]

## Quick Revision
- Pick collector for goal (G1 default, ZGC/Shenandoah low-pause), size heap, set SLO, log + measure, cut allocations first.
