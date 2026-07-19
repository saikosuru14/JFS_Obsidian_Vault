---
title: Two Pointers
aliases:
  - Two Pointers
domain: DSA
module: Arrays and Strings
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 3
tags:
  - dsa
related:
  - "[[Arrays and Strings Index|Arrays and Strings]]"
  - "[[Sliding Window]]"
---

# Two Pointers

## Overview
The two-pointer technique uses two indices moving through a structure to solve in O(n) what would otherwise be O(n²). Variants: **converging** (ends moving inward), **fast/slow** (different speeds), and **parallel** (two sequences).

## Why It Matters
It turns many array/string problems (pairs, palindromes, partitioning, merging) from quadratic to linear with O(1) space — one of the highest-frequency interview patterns.

## Patterns
### Converging (sorted array)
```java
// Two-sum on a SORTED array: O(n), O(1) space
int l = 0, r = n - 1;
while (l < r) {
    int sum = a[l] + a[r];
    if (sum == target) return new int[]{l, r};
    if (sum < target) l++; else r--;
}
```

### Fast / Slow
Detect cycles, find middle — see [[Fast and Slow Pointers]] (linked lists).

### Same-direction (read/write)
```java
// Remove duplicates from sorted array in place: O(n)
int w = 1;
for (int r = 1; r < n; r++)
    if (a[r] != a[r - 1]) a[w++] = a[r];
return w;   // new length
```

## When To Use
- Sorted array + find a pair/triplet (2-sum, 3-sum).
- Palindrome / reverse in place.
- Partitioning (Dutch national flag), merging two sorted arrays.
- In-place removal/compaction.

## Interview Questions
- **When do two pointers apply?** Often on sorted data or when you can move two indices monotonically to avoid a nested loop.
- **Two-sum sorted vs unsorted?** Sorted -> two pointers O(n) O(1); unsorted -> hash map O(n) O(n).
- **3-sum approach?** Sort, fix one element, two-pointer the rest -> O(n²).

## Related Topics
- [[Sliding Window]] · [[Arrays]] · [[Fast and Slow Pointers]] · [[Binary Search]]

## Quick Revision
- Two moving indices -> O(n), O(1). Converging (sorted pairs/palindrome), fast/slow (cycle/middle), read/write (in-place compaction). Sort first if it enables it.
