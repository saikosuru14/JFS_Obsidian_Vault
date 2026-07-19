---
title: Set
aliases:
  - Set
domain: Java
module: Collections Framework
status: Not Started
difficulty: Easy
priority: Medium
interview: 3
revision: Weekly
order: 7
tags:
  - java
  - collections
related:
  - "[[Collections Framework]]"
  - "[[HashSet]]"
  - "[[LinkedHashSet]]"
  - "[[TreeSet]]"
---

# Set

## Overview
`Set` models a collection with no duplicates. Uniqueness is determined by `equals()`/`hashCode()` (hash-based) or `compareTo`/`Comparator` (tree-based).

## Implementations
| Impl | Order | Complexity | Backed by |
|------|-------|-----------|-----------|
| [[HashSet]] | none | O(1) | [[HashMap]] |
| [[LinkedHashSet]] | insertion | O(1) | LinkedHashMap |
| [[TreeSet]] | sorted | O(log n) | [[TreeMap]] |

## Why It Matters
Deduplication, membership tests, and set algebra (`retainAll`, `removeAll`, `addAll`) are everyday operations.

## Best Practices
- Use immutable keys; a stable `equals`/`hashCode` is mandatory for hash sets.
- `Set.of(...)` for small immutable sets.

## Common Mistakes
- Mutating an element after insertion so its hash changes → the element becomes unreachable.
- Relying on iteration order of `HashSet` (there is none).

## Interview Questions
- How does a `Set` detect duplicates?
- HashSet vs LinkedHashSet vs TreeSet?

## Related Topics
- [[Collections Framework]] · [[HashSet]] · [[LinkedHashSet]] · [[TreeSet]]

## Quick Revision
- No duplicates via equals/hashCode (or comparator). HashSet=O(1) no order, LinkedHashSet=insertion order, TreeSet=sorted O(log n).
