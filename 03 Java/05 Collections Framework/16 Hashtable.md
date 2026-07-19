---
title: Hashtable
aliases:
  - Hashtable
domain: Java
module: Collections Framework
status: Not Started
difficulty: Easy
priority: Low
interview: 3
revision: Monthly
order: 16
tags:
  - java
  - collections
related:
  - "[[Map]]"
  - "[[HashMap]]"
  - "[[ConcurrentHashMap]]"
---

# Hashtable

## Overview
Legacy synchronized `Map` (JDK 1.0). Thread-safe via method-level synchronization, but coarse-grained and slow. Superseded by [[ConcurrentHashMap]].

## HashMap vs Hashtable vs ConcurrentHashMap
| | HashMap | Hashtable | ConcurrentHashMap |
|---|---------|-----------|-------------------|
| Thread-safe | No | Yes (whole-map lock) | Yes (fine-grained) |
| Null key/value | 1 key, N values | None | None |
| Performance | Fast | Slow | Fast under contention |
| Since | 1.2 | 1.0 | 1.5 |

## Why It Matters
Almost purely an interview comparison and legacy-code topic.

## Best Practices
- Don't use in new code. For concurrency use `ConcurrentHashMap`; single-threaded use `HashMap`.
- Whole-map locking still doesn't make check-then-act atomic.

## Interview Questions
- HashMap vs Hashtable vs ConcurrentHashMap?
- Why does Hashtable forbid null keys/values?

## Related Topics
- [[Map]] · [[HashMap]] · [[ConcurrentHashMap]]

## Quick Revision
- Legacy, whole-map synchronized, no nulls. Replaced by ConcurrentHashMap. Comparison-only relevance.
