---
title: Divide and Conquer
aliases:
  - Divide and Conquer
domain: DSA
module: Recursion and Backtracking
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 3
tags:
  - dsa
related:
  - "[[Recursion]]"
---

# Divide and Conquer

## Overview
Divide and conquer solves a problem by (1) **dividing** it into independent subproblems, (2) **conquering** each recursively, and (3) **combining** the results. Unlike DP, the subproblems don't overlap.

## Why It Matters
It's the paradigm behind merge sort, quicksort, binary search, and quickselect, and the Master Theorem gives a quick way to derive their complexity.

## Structure
```
solve(problem):
    if small: return base solution
    split into subproblems
    solve each recursively
    combine results
```

## Examples
- **[[QuickSort and MergeSort|Merge sort]]** — split in half, sort, merge: O(n log n).
- **[[Binary Search]]** — halve the range: O(log n).
- **Quickselect** — partition, recurse one side: O(n) average.
- Maximum subarray (D&C), closest pair of points, fast exponentiation.

## Master Theorem (intuition)
For `T(n) = a·T(n/b) + O(nᵈ)`:
- If `d > log_b a` -> O(nᵈ) (combine dominates).
- If `d = log_b a` -> O(nᵈ log n) (balanced) — e.g., merge sort (a=2,b=2,d=1) -> O(n log n).
- If `d < log_b a` -> O(n^(log_b a)) (recursion dominates).

## Divide & Conquer vs Dynamic Programming
- D&C: **independent** subproblems, combine once.
- [[Dynamic Programming]]: **overlapping** subproblems, cache results.

## Interview Questions
- **Three steps of divide and conquer?** Divide, conquer (recurse), combine.
- **D&C vs DP?** Independent vs overlapping subproblems (DP memoizes).
- **Merge sort complexity via Master Theorem?** a=2, b=2, d=1 -> O(n log n).

## Related Topics
- [[QuickSort and MergeSort]] · [[Binary Search]] · [[Dynamic Programming]] · [[Recursion]]

## Quick Revision
- Divide -> conquer -> combine on independent subproblems. Merge/quick sort, binary search, quickselect. Master Theorem gives complexity. DP = D&C with overlapping subproblems cached.
