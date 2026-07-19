---
title: HashSet
aliases:
  - HashSet
domain: Java
module: Collections Framework
status: Not Started
difficulty: Medium
priority: Medium
interview: 4
revision: Weekly
order: 8
tags:
  - java
  - collections
related:
  - "[[Set]]"
  - "[[HashMap]]"
---

# HashSet

## Overview
`Set` implementation backed by a [[HashMap]] (elements are keys, values are a shared dummy object). Average O(1) `add`/`contains`/`remove`; no ordering.

## Internal Working
- `add(e)` delegates to `map.put(e, PRESENT)`; returns `false` if the key already existed.
- Uniqueness relies entirely on the element's `hashCode()` + `equals()`.
- Inherits HashMap behavior: bucketing, treeification after 8 collisions, resize at load factor 0.75.

## Performance
- O(1) average; O(n) worst case with poor hashing (mitigated by treeification to O(log n) in Java 8+).
- Presize (`new HashSet<>(expected / 0.75 + 1)`) for large sets.

## Best Practices
- Store immutable elements with correct, stable `equals`/`hashCode`.
- Not thread-safe — use `ConcurrentHashMap.newKeySet()` for concurrency.

## Common Mistakes
- Overriding `equals` but not `hashCode` → duplicates slip in.
- Mutating stored elements so their hash changes.

## Interview Questions
- How are duplicates detected?
- What backs a HashSet?
- Why must you override both `equals` and `hashCode`?

## Related Topics
- [[Set]] · [[HashMap]]

## Quick Revision
- Backed by HashMap; O(1) average; uniqueness via equals/hashCode; no order; presize for large sets.
