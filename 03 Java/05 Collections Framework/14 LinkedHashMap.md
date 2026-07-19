---
title: LinkedHashMap
aliases:
  - LinkedHashMap
domain: Java
module: Collections Framework
status: Not Started
difficulty: Medium
priority: Medium
interview: 4
revision: Weekly
order: 14
tags:
  - java
  - collections
related:
  - "[[Map]]"
  - "[[HashMap]]"
---

# LinkedHashMap

## Overview
`HashMap` that preserves iteration order via a doubly linked list across entries. Supports **insertion order** (default) or **access order** — the basis of a simple LRU cache.

## Internal Working
- Extends `HashMap`; each entry also has `before`/`after` links.
- With `accessOrder = true`, `get`/`put` move the entry to the tail (most-recently-used).
- Override `removeEldestEntry` to evict when size exceeds a limit.

## Example — LRU cache
```java
new LinkedHashMap<K,V>(capacity, 0.75f, true) {
    protected boolean removeEldestEntry(Map.Entry<K,V> e) {
        return size() > capacity;
    }
};
```

## Performance
- O(1) average like HashMap, with extra memory/time for the linked pointers.

## Best Practices
- Use for deterministic iteration order or a small in-process LRU.
- For real caching at scale, prefer Caffeine/Guava over hand-rolled LRU.

## Interview Questions
- How do you build an LRU cache in Java?
- Insertion order vs access order?
- LinkedHashMap vs HashMap vs TreeMap?

## Related Topics
- [[Map]] · [[HashMap]]

## Quick Revision
- HashMap + linked order (insertion/access). Access-order + removeEldestEntry = LRU. O(1), slightly more memory.
