---
title: Collections Framework
aliases:
  - Collections Framework
domain: Java
module: Collections Framework
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - java
  - collections
related:
  - "[[Java]]"
  - "[[List]]"
  - "[[Set]]"
  - "[[Queue]]"
  - "[[Map]]"
---

# Collections Framework

## Overview
The Java Collections Framework (JCF) is a unified set of interfaces and implementations for storing and manipulating groups of objects. `Collection` is the root for `List`/`Set`/`Queue`; `Map` is a separate hierarchy. This note is the module **hub** — expand a sub-hub to reach its implementations.

## Why It Matters
Choosing the right collection is the most common performance and correctness decision in day-to-day Java. Interviewers probe internals (HashMap, ConcurrentHashMap) constantly.

## Structure (expand each hub)
- **[[List]]** — ordered, indexed, duplicates → ArrayList, LinkedList, Vector.
- **[[Set]]** — unique elements → HashSet, LinkedHashSet, TreeSet.
- **[[Queue]]** — FIFO / deque → ArrayDeque, PriorityQueue.
- **[[Map]]** — key→value → HashMap, LinkedHashMap, TreeMap, Hashtable, ConcurrentHashMap.
- **[[Iterator]]** — traversal and fail-fast behavior.
- **[[Concurrent Collections]]** — thread-safe variants.

## Choosing an Implementation
| Need | Interface | Typical impl |
|------|-----------|--------------|
| Indexed, mostly reads | List | ArrayList |
| Unique, O(1) | Set | HashSet |
| Unique + sorted | Set | TreeSet |
| Key-value, O(1) | Map | HashMap |
| Key-value, sorted | Map | TreeMap |
| Insertion order | List/Set/Map | LinkedHash* |
| Concurrent access | — | ConcurrentHashMap |

## Complexity (average)
| Op | ArrayList | LinkedList | HashMap/HashSet | TreeMap/TreeSet |
|----|-----------|------------|-----------------|-----------------|
| get/contains | O(1) / O(n) | O(n) | O(1) | O(log n) |
| add (end) | amortized O(1) | O(1) | O(1) | O(log n) |
| remove (middle) | O(n) | O(1)* | O(1) | O(log n) |

\*with a node reference; finding it is still O(n).

## Best Practices
- Declare fields/parameters by interface (`List`, `Map`), not implementation.
- Size collections up front for large datasets to avoid resizes.
- Return empty collections, never `null`; expose unmodifiable views.

## Interview Questions
- Why is `Map` not a `Collection`?
- How do you pick between the main implementations?
- Fail-fast vs fail-safe iterators?

## Related Topics
- [[List]] · [[Set]] · [[Queue]] · [[Map]] · [[Iterator]] · [[Concurrent Collections]]

## Quick Revision
- Collection root (List/Set/Queue) + separate Map. Pick by access pattern; program to interfaces; size up front.
