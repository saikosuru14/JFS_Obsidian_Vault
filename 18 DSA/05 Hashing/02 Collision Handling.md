---
title: Collision Handling
aliases:
  - Collision Handling
domain: DSA
module: Hashing
status: Learning
difficulty: Medium
priority: Medium
interview: 4
revision: Weekly
order: 2
tags:
  - dsa
related:
  - "[[Hash Tables]]"
---

# Collision Handling

## Overview
A collision happens when two distinct keys hash to the same bucket. Since collisions are unavoidable (pigeonhole principle), every hash table needs a resolution strategy. The two families are **separate chaining** and **open addressing**.

## Why It Matters
Collision strategy determines worst-case behavior, memory layout, and deletion complexity — and it's why Java's `HashMap` treeifies long chains.

## Separate Chaining
Each bucket holds a list (or tree) of entries that hashed there.
- Java `HashMap`: linked list per bucket, converted to a **red-black tree** when a bucket exceeds 8 entries (and capacity ≥ 64), giving O(log n) worst case instead of O(n).
- Simple, handles high load factors gracefully; extra memory for pointers.

## Open Addressing
All entries live in the array itself; on collision, **probe** for the next free slot.
- **Linear probing** — try i+1, i+2, ... (cache-friendly, but clustering).
- **Quadratic probing** — try i+1², i+2², ... (reduces clustering).
- **Double hashing** — step size from a second hash.
- Deletion needs tombstones; performance degrades sharply as load factor -> 1.

## Comparison
| | Chaining | Open Addressing |
|--|----------|-----------------|
| Storage | lists/trees in buckets | entries in the array |
| Load factor | can exceed 1 | must stay < 1 |
| Cache | worse (pointer chasing) | better (contiguous) |
| Deletion | easy | needs tombstones |

## Interview Questions
- **What is a collision and why inevitable?** Two keys map to one bucket; pigeonhole — more keys than buckets.
- **Chaining vs open addressing?** Lists per bucket vs probing within the array; chaining tolerates high load, open addressing is cache-friendly but needs low load + tombstones.
- **How does Java's HashMap limit worst case?** Treeifies a bucket (red-black tree) beyond 8 entries -> O(log n).

## Related Topics
- [[Hash Tables]] · [[HashMap]] · [[Balanced Trees]]

## Quick Revision
- Collisions are inevitable. Chaining (lists/trees per bucket; Java treeifies >8) vs open addressing (probe: linear/quadratic/double, needs tombstones, low load). Chaining tolerates high load; open addressing is cache-friendly.
