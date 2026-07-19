---
title: Binary Search
aliases:
  - Binary Search
domain: DSA
module: Sorting and Searching
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 2
tags:
  - dsa
related:
  - "[[Sorting and Searching Index|Sorting and Searching]]"
---

# Binary Search

## Overview
Binary search finds a target in a **sorted** array by repeatedly halving the search range, giving O(log n). Beyond arrays, "binary search on the answer" solves optimization problems with a monotonic feasibility check.

## Why It Matters
It's the classic O(log n) technique and a frequent source of off-by-one bugs. The "search the answer space" variant appears in many hard problems (min capacity, Koko eating bananas, allocate pages).

## Standard Template
```java
int binarySearch(int[] a, int target) {
    int lo = 0, hi = a.length - 1;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;      // avoid overflow (not (lo+hi)/2)
        if (a[mid] == target) return mid;
        if (a[mid] < target) lo = mid + 1;
        else hi = mid - 1;
    }
    return -1;
}
```

## Lower / Upper Bound
Find the first index where a condition becomes true (leftmost). Java: `Arrays.binarySearch` (any match), `Collections.binarySearch`; for bounds, use a predicate template.
```java
// first index with a[i] >= target
int lo = 0, hi = n;                 // half-open
while (lo < hi) {
    int mid = lo + (hi - lo) / 2;
    if (a[mid] >= target) hi = mid; else lo = mid + 1;
}
return lo;
```

## Binary Search on the Answer
When the answer is monotonic (feasible below/above a threshold), binary-search the value range and test feasibility: min ship capacity, min days, split array largest sum, sqrt.

## Common Mistakes
- Overflow with `(lo + hi) / 2` — use `lo + (hi - lo) / 2`.
- Wrong loop condition (`<` vs `<=`) / boundary update -> infinite loop or off-by-one.
- Forgetting the array must be sorted.

## Interview Questions
- **Requirement for binary search?** The data (or answer space) must be sorted/monotonic.
- **How avoid the mid overflow bug?** `lo + (hi - lo) / 2`.
- **What is "binary search on the answer"?** Binary-search a value range using a monotonic feasibility predicate.

## Related Topics
- [[Sorting Algorithms]] · [[Arrays]] · [[Binary Search Tree]]

## Quick Revision
- Halve a sorted range -> O(log n). Use `lo + (hi-lo)/2`; mind `<`/`<=`. Lower/upper bound via predicate template. "Search the answer" for monotonic optimization.
