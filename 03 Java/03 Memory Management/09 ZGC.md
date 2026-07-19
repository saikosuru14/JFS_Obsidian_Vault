---
title: ZGC
aliases:
  - ZGC
  - Z Garbage Collector
domain: Java
module: Memory Management
status: Learning
difficulty: Hard
priority: Medium
interview: 3
revision: Weekly
order: 9
tags:
  - java
related:
  - "[[Garbage Collection Overview]]"
  - "[[Shenandoah GC]]"
---

# Z Garbage Collector (ZGC)

## Overview
ZGC is a **concurrent, low-latency** collector designed for large heaps (up to terabytes) with pause times that stay **sub-millisecond** regardless of heap size. Production-ready since Java 15; generational ZGC arrived in Java 21.

## Why It Matters
When tail latency matters more than raw throughput — trading systems, low-latency APIs, huge in-memory datasets — ZGC keeps pauses flat even as the heap grows, unlike G1.

## How It Works
- **Colored pointers** — metadata bits stored inside 64-bit references to track object state without extra headers.
- **Load barriers** — a check on each reference load that lets ZGC **relocate objects concurrently** while the app runs.
- Nearly all work (marking, relocation, remapping) is concurrent; only tiny STW pauses remain, independent of heap/live-set size.

## Key Flags
- `-XX:+UseZGC` ; `-XX:+ZGenerational` (Java 21+, generational mode).

## Trade-offs
- Slightly lower throughput and higher CPU/memory overhead than Parallel/G1.
- 64-bit only; benefits show most on large heaps.

## Interview Questions
- **What makes ZGC pauses independent of heap size?** Marking and relocation run concurrently; STW work is bounded and doesn't scale with the live set.
- **What are colored pointers and load barriers?** Metadata packed into references plus a per-load check enabling concurrent relocation.
- **ZGC vs G1?** ZGC targets sub-ms pauses on huge heaps; G1 balances pause and throughput on moderate heaps.

## Related Topics
- [[Shenandoah GC]] · [[G1 GC]] · [[Garbage Collection Overview]]

## Quick Revision
- Concurrent, sub-ms pauses on TB heaps. Colored pointers + load barriers = concurrent relocation. Java 15+ (generational in 21). Lower throughput, needs 64-bit.
