---
title: Vector
aliases:
  - Vector
domain: Java
module: Collections Framework
status: Not Started
difficulty: Easy
priority: Low
interview: 2
revision: Monthly
order: 6
tags:
  - java
  - collections
related:
  - "[[List]]"
  - "[[ArrayList]]"
---

# Vector

## Overview
Legacy, synchronized resizable-array `List` (pre-Collections). Every method is `synchronized`, so it's thread-safe but slow and rarely used in new code.

## Why It Matters
Mainly an interview comparison point (`Vector` vs `ArrayList`) and appears in old codebases.

## Vector vs ArrayList
| | Vector | ArrayList |
|---|--------|-----------|
| Sync | Every method synchronized | Not synchronized |
| Growth | Doubles (100%) | ~1.5× |
| Age | Legacy (JDK 1.0) | Since 1.2 |

## Best Practices
- Prefer `ArrayList`; for concurrency use `CopyOnWriteArrayList` or explicit locks.
- Method-level synchronization doesn't make compound operations atomic — you still need external locking for check-then-act.

## Interview Questions
- Vector vs ArrayList?
- Why isn't per-method synchronization enough for thread safety?

## Related Topics
- [[List]] · [[ArrayList]]

## Quick Revision
- Legacy synchronized list; doubles on growth. Prefer ArrayList; per-method sync ≠ compound atomicity.
