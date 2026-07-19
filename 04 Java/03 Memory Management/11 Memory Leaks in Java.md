---
title: Memory Leaks in Java
aliases:
  - Memory Leaks in Java
domain: Java
module: Memory Management
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 11
tags:
  - java
related:
  - "[[Memory Management Index|Memory Management]]"
  - "[[Garbage Collection Overview]]"
---

# Memory Leaks in Java

## Overview
Garbage collection frees **unreachable** objects — but a leak in Java means objects stay **reachable** (via some lingering reference) long after they're needed. They accumulate, and eventually the heap fills.

## Why It Matters
The signature is a slow climb in Old-Gen usage, rising GC frequency, and finally `OutOfMemoryError` after hours or days. Diagnosing it is a core senior skill.

## Common Causes
- **Static collections** — a `static Map`/`List` that only ever grows; classic unbounded cache.
- **Unbounded caches** — no eviction/TTL; use `WeakHashMap`, soft references, or a real cache (Caffeine) with size/time limits.
- **Unclosed resources** — streams, connections, sessions not closed (use try-with-resources).
- **Listener / callback leaks** — registered but never deregistered observers.
- **`ThreadLocal` misuse** — values not removed on pooled threads keep their referents alive; always `remove()` in a `finally`.
- **Classloader leaks** — cause [[Metaspace]] OOM on repeated redeploys.

## How to Diagnose
1. Confirm the trend: monitor heap over time (rising baseline after Full GC = leak).
2. Capture a **heap dump** (`-XX:+HeapDumpOnOutOfMemoryError`, or `jmap`).
3. Analyze with **Eclipse MAT** — find the largest retained sets and the **dominator tree**; follow GC-root reference chains to the culprit.
4. Profile live with **VisualVM**, **JConsole**, or **Java Flight Recorder**.

## Best Practices
- Bound every cache (size + TTL); prefer weak/soft references for caches.
- Always `remove()` ThreadLocals on pooled threads; close resources with try-with-resources.
- Deregister listeners in lifecycle teardown.

## Interview Questions
- **How can a GC'd language leak?** Objects remain reachable through unintended references, so GC won't collect them.
- **Most common real-world cause?** Unbounded static collections/caches and un-removed ThreadLocals on pooled threads.
- **How would you find one?** Trend heap usage, take a heap dump, analyze retained sets and GC-root paths in MAT.

## Related Topics
- [[Garbage Collection Overview]] · [[Old Generation]] · [[Metaspace]]

## Quick Revision
- Leak = still-reachable but unused objects piling up. Causes: static/unbounded caches, unclosed resources, listeners, ThreadLocals, classloaders. Diagnose via heap dump + MAT dominator tree.
