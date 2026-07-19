---
title: Map
aliases:
  - Map
domain: Java
module: Collections Framework
status: Not Started
difficulty: Easy
priority: High
interview: 4
revision: Weekly
order: 12
tags:
  - java
  - collections
related:
  - "[[Collections Framework]]"
  - "[[HashMap]]"
  - "[[LinkedHashMap]]"
  - "[[TreeMap]]"
  - "[[Hashtable]]"
  - "[[ConcurrentHashMap]]"
---

# Map

## Overview
`Map<K,V>` stores key→value associations with unique keys. It's a separate hierarchy from `Collection` because its element model (pairs) differs.

## Implementations
| Impl | Order | Complexity | Null keys |
|------|-------|-----------|-----------|
| [[HashMap]] | none | O(1) | one |
| [[LinkedHashMap]] | insertion/access | O(1) | one |
| [[TreeMap]] | sorted | O(log n) | none |
| [[Hashtable]] | none | O(1), synced | none |
| [[ConcurrentHashMap]] | none | O(1), concurrent | none |

## Useful Methods
`getOrDefault`, `putIfAbsent`, `computeIfAbsent`, `merge`, `compute` — prefer these over manual check-then-put.

## Example
```java
// group / count idioms
map.merge(key, 1, Integer::sum);
map.computeIfAbsent(key, k -> new ArrayList<>()).add(v);
```

## Best Practices
- Immutable keys with correct `equals`/`hashCode`.
- Use the functional methods for aggregation; `Map.of(...)` for small immutable maps.

## Interview Questions
- Why is `Map` not part of `Collection`?
- When TreeMap vs HashMap vs LinkedHashMap?
- `computeIfAbsent` vs `putIfAbsent`?

## Related Topics
- [[Collections Framework]] · [[HashMap]] · [[LinkedHashMap]] · [[TreeMap]] · [[Hashtable]] · [[ConcurrentHashMap]]

## Quick Revision
- Key→value, unique keys, separate from Collection. HashMap O(1)/no order, TreeMap sorted O(log n). Use merge/computeIfAbsent.
