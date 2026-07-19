---
title: Shenandoah GC
aliases:
  - Shenandoah GC
domain: Java
module: Memory Management
status: Learning
difficulty: Hard
priority: Medium
interview: 3
revision: Weekly
order: 10
tags:
  - java
related:
  - "[[Garbage Collection Overview]]"
  - "[[ZGC]]"
---

# Shenandoah GC

## Overview
Shenandoah is a **low-pause** collector (Red Hat / OpenJDK) that performs **concurrent compaction** — it evacuates and relocates live objects while application threads keep running. Pauses stay short and largely independent of heap size.

## Why It Matters
Like ZGC, it targets latency-sensitive apps, but it works well across a broader range of heap sizes (including smaller heaps) and has been available/backported across several JDKs.

## How It Works
- **Brooks forwarding pointers** — each object carries an indirection pointer so it can be moved concurrently; references are forwarded to the new location.
- **Load reference barriers** — ensure threads read the up-to-date object during concurrent evacuation.
- Marking, evacuation, and update-references phases run mostly concurrently; only brief STW pauses for init/final mark.

## Key Flags
- `-XX:+UseShenandoahGC`.

## Shenandoah vs ZGC
| | Shenandoah | ZGC |
|--|-----------|-----|
| Origin | Red Hat / OpenJDK | Oracle |
| Technique | forwarding pointers + barriers | colored pointers + load barriers |
| Sweet spot | small to large heaps | very large heaps |
| Pauses | low, heap-size independent | sub-ms, heap-size independent |

## Interview Questions
- **How does Shenandoah keep pauses low?** Concurrent evacuation/compaction using forwarding pointers, so relocation doesn't require a long STW pause.
- **Shenandoah vs G1?** Shenandoah compacts concurrently for lower pauses; G1's evacuation pauses grow with the collected set.
- **Trade-off?** Extra barrier/indirection overhead reduces peak throughput vs Parallel GC.

## Related Topics
- [[ZGC]] · [[G1 GC]] · [[Garbage Collection Overview]]

## Quick Revision
- Concurrent compaction via Brooks forwarding pointers + load barriers. Low, heap-size-independent pauses. -XX:+UseShenandoahGC. Similar goals to ZGC, broader heap range.
