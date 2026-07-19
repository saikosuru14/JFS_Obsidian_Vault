---
title: hashCode()
aliases:
  - hashCode()
domain: Java
module: Core Java
status: Not Started
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 4
tags:
  - java
  - core
related:
  - "[[equals() vs ==]]"
  - "[[HashMap]]"
---

# hashCode()

## Overview
`hashCode()` returns an int used to place objects into buckets in hash-based collections ([[HashMap]], [[HashSet]], [[ConcurrentHashMap]]).

## The Contract
- Equal objects (`equals` true) **must** have equal hash codes.
- Unequal objects *may* share a hash code (collision) — allowed but should be rare.
- Must be consistent across calls while equality-relevant fields don't change.

## Why It Matters
Violating the contract makes objects "disappear" from maps/sets: `put` goes to one bucket, `get` computes a different one.

## Example
```java
@Override public int hashCode() { return Objects.hash(id, email); }
@Override public boolean equals(Object o) { /* compare id, email */ }
```

## Performance
- A poor hash (many collisions) degrades HashMap toward O(n); Java 8+ treeifies large buckets to O(log n).
- Use the same fields in `equals` and `hashCode`.

## Common Mistakes
- Overriding one but not the other.
- Including mutable fields, then mutating a key after insertion.
- Hand-rolling weak hashes instead of `Objects.hash`.

## Interview Questions
- State the hashCode/equals contract.
- What happens if two equal objects have different hash codes?
- Why can unequal objects share a hash code?

## Related Topics
- [[equals() vs ==]] · [[HashMap]] · [[Object Class]]

## Quick Revision
- Equal ⇒ equal hashCode; collisions allowed. Use same fields as equals via `Objects.hash`; never mutate key fields after insertion.
