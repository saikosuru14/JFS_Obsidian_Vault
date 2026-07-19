---
title: TreeSet
aliases:
  - TreeSet
domain: Java
module: Collections Framework
status: Not Started
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 10
tags:
  - java
  - collections
related:
  - "[[Set]]"
  - "[[TreeMap]]"
---

# TreeSet

## Overview
Sorted `Set` backed by a [[TreeMap]] (red-black tree). Iterates in sorted order; O(log n) operations. Implements `NavigableSet`.

## Internal Working
- Ordering comes from natural order ([[Comparable vs Comparator|Comparable]]) or a supplied `Comparator`.
- Navigation methods: `first`, `last`, `ceiling`, `floor`, `higher`, `lower`, `headSet`, `tailSet`, `subSet`.

## When to Use
- Need elements kept sorted, or range/nearest-neighbor queries.

## Performance
- O(log n) add/contains/remove — slower than HashSet's O(1), traded for ordering.

## Common Mistakes
- Elements not `Comparable` and no `Comparator` → `ClassCastException` at runtime.
- Using a comparator inconsistent with `equals` → "missing" elements.
- `null` elements are not allowed.

## Interview Questions
- TreeSet vs HashSet — cost and ordering?
- What backs TreeSet, and how is ordering determined?
- What does `NavigableSet` add?

## Related Topics
- [[Set]] · [[TreeMap]]

## Quick Revision
- Red-black tree (TreeMap-backed), sorted, O(log n), NavigableSet ops. Needs Comparable/Comparator; no nulls.
