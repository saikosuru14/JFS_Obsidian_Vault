---
title: Arrays
aliases:
  - Arrays
domain: DSA
module: Arrays and Strings
status: Learning
difficulty: Easy
priority: High
interview: 5
revision: Weekly
order: 1
tags:
  - dsa
related:
  - "[[Arrays and Strings Index|Arrays and Strings]]"
  - "[[Prefix Sum]]"
---

# Arrays

## Overview
An array is a contiguous block of memory storing elements of the same type, accessed by index in O(1). Java has fixed-size primitive/object arrays and the resizable `ArrayList` (see [[ArrayList]]).

## Why It Matters
Arrays are the default sequence structure and the substrate for most interview problems. Their O(1) random access and cache-friendliness make them fast; their fixed size and O(n) insertion are the trade-offs.

## Complexity
| Operation | Array |
|-----------|-------|
| Access by index | O(1) |
| Search (unsorted) | O(n) |
| Search (sorted) | O(log n) via [[Binary Search]] |
| Insert/delete at end (ArrayList) | amortized O(1) |
| Insert/delete in middle | O(n) (shift) |

## Java Essentials
```java
int[] a = new int[n];          // fixed size, defaults 0
int[] b = {1, 2, 3};
Arrays.sort(a);                 // O(n log n)
int i = Arrays.binarySearch(a, key);   // requires sorted
int[] copy = Arrays.copyOfRange(a, 1, 4);
List<Integer> list = new ArrayList<>(); // dynamic array
```

## Common Techniques
- **[[Two Pointers]]** — pairs/partitions on sorted arrays.
- **[[Sliding Window]]** — contiguous subarray problems.
- **[[Prefix Sum]]** — O(1) range-sum queries.
- **In-place** manipulation to achieve O(1) extra space.

## Common Mistakes
- Off-by-one and out-of-bounds at boundaries.
- Modifying an array while iterating.
- Forgetting arrays are fixed-size (use `ArrayList` when growth is needed).

## Interview Questions
- **Array vs ArrayList?** Array is fixed-size, can hold primitives; ArrayList is resizable (amortized O(1) add), objects only, richer API.
- **Why is array access O(1)?** Address = base + index × elementSize — direct arithmetic.
- **How to remove from the middle efficiently?** You can't in O(1) with an array; consider a different structure or swap-with-last if order doesn't matter.

## Related Topics
- [[Prefix Sum]] · [[Two Pointers]] · [[Binary Search]] · [[ArrayList]]

## Quick Revision
- Contiguous, O(1) index, O(n) middle insert. Cache-friendly. Use ArrayList for growth. Patterns: two pointers, sliding window, prefix sum.
