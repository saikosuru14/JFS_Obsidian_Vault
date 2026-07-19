---
title: Metaspace
aliases:
  - Metaspace
domain: Java
module: Memory Management
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 6
tags:
  - java
related:
  - "[[Memory Management Index|Memory Management]]"
---

# Metaspace

## Overview
Metaspace (Java 8+) stores **class metadata** — class structures, method data, and the runtime constant pool. It replaced **PermGen** and lives in **native (off-heap) memory**, so it grows dynamically instead of being capped by the heap.

## Why It Matters
PermGen's fixed size caused frequent `OutOfMemoryError: PermGen space`, especially in app servers that load many classes or redeploy often. Metaspace auto-grows, but unbounded class loading can still exhaust native memory.

## PermGen vs Metaspace
| | PermGen (<= Java 7) | Metaspace (Java 8+) |
|--|---------------------|---------------------|
| Location | heap | native memory |
| Sizing | fixed (`-XX:MaxPermSize`) | auto-grows |
| Flag | `-XX:MaxPermSize` | `-XX:MaxMetaspaceSize` |
| GC | with heap | on class-loader unload |

## What Triggers Metaspace GC
Class metadata is reclaimed when its **class loader** becomes unreachable. So leaks here come from class loaders that never get collected.

## Common Errors / Causes
- **`OutOfMemoryError: Metaspace`** — classloader leaks (repeated hot redeploys), heavy dynamic proxy/bytecode generation (some frameworks), or too many loaded classes.
- Set `-XX:MaxMetaspaceSize` to fail fast rather than consume all native memory.

## Interview Questions
- **Why was PermGen removed?** Fixed sizing caused frequent OOMs and hard tuning; Metaspace uses auto-growing native memory.
- **When is class metadata collected?** When its class loader is unloaded (unreachable).
- **What causes a Metaspace leak?** Class loaders that are never GC'd (classic redeploy leak) or unbounded dynamic class generation.

## Related Topics
- [[Heap Memory]] · [[Garbage Collection Overview]] · [[Memory Leaks in Java]]

## Quick Revision
- Off-heap class metadata; replaced PermGen; auto-grows. Freed on class-loader unload. Cap with -XX:MaxMetaspaceSize; leaks come from stuck class loaders.
