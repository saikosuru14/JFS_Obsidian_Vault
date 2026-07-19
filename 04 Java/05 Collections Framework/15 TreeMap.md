---
title: TreeMap
aliases:
  - TreeMap
domain: Java
module: Collections Framework
status: Not Started
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 15
tags:
  - java
  - collections
related:
  - "[[Map]]"
  - "[[HashMap]]"
---

# TreeMap

## Overview
Sorted `Map` backed by a red-black (self-balancing) tree. Keys are kept in order; O(log n) operations. Implements `NavigableMap`.

## Internal Working
- Ordering via natural order ([[Comparable vs Comparator|Comparable]]) or a `Comparator`.
- Navigation: `firstKey`, `lastKey`, `ceilingKey`, `floorKey`, `headMap`, `tailMap`, `subMap`.
- Rebalances on insert/delete to keep height ~log n.

## When to Use
- Need keys sorted, or range queries / nearest-key lookups.
- Otherwise prefer [[HashMap]] for O(1).

## Performance
- O(log n) get/put/remove; ordered iteration is free.

## Common Mistakes
- Keys not `Comparable` and no `Comparator` → `ClassCastException`.
- Comparator inconsistent with `equals` → keys appear "missing".
- `null` keys not allowed.

## Interview Questions
- TreeMap vs HashMap — cost and use cases?
- What is a red-black tree and why balanced?
- What does `NavigableMap` add?

## Related Topics
- [[Map]] · [[HashMap]]

## Quick Revision
- Red-black tree, sorted keys, O(log n), NavigableMap. Needs Comparable/Comparator; no null keys.
