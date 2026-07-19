---
title: Sorting Algorithms
aliases:
  - Sorting Algorithms
domain: DSA
module: Sorting and Searching
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 1
tags:
  - dsa
related:
  - "[[Sorting and Searching Index|Sorting and Searching]]"
  - "[[QuickSort and MergeSort]]"
---

# Sorting Algorithms

## Overview
Sorting arranges elements by a comparator. Comparison-based sorts have a proven lower bound of **O(n log n)**; non-comparison sorts (counting/radix) beat it under special conditions.

## Why It Matters
Sorting is a preprocessing step for countless techniques (two pointers, greedy, dedup, binary search). Knowing the trade-offs (stability, in-place, worst case) is essential.

## Comparison Sorts
| Algorithm | Best | Average | Worst | Space | Stable |
|-----------|------|---------|-------|-------|--------|
| Bubble/Insertion | O(n) | O(n²) | O(n²) | O(1) | yes |
| Selection | O(n²) | O(n²) | O(n²) | O(1) | no |
| **Merge** | O(n log n) | O(n log n) | O(n log n) | O(n) | yes |
| **Quick** | O(n log n) | O(n log n) | O(n²) | O(log n) | no |
| **Heap** | O(n log n) | O(n log n) | O(n log n) | O(1) | no |

## Key Properties
- **Stable** — equal elements keep their relative order (merge sort; important for multi-key sorts).
- **In-place** — O(1) extra space (quick, heap).
- **Lower bound** — comparison sorts can't beat O(n log n).

## Non-Comparison Sorts
- **Counting sort** — O(n + k) for small integer ranges k.
- **Radix sort** — O(d·(n + k)) digit by digit.

## Java's Sort
- `Arrays.sort(int[])` — dual-pivot **quicksort** (primitives, not stable).
- `Arrays.sort(Object[])` / `Collections.sort` — **TimSort** (stable, merge+insertion hybrid), O(n log n).

## Interview Questions
- **Lower bound of comparison sorting?** O(n log n).
- **Why is merge sort stable and quicksort not?** Merge preserves order on equal keys; quicksort's swaps can reorder equal elements.
- **What does Java use?** TimSort for objects (stable), dual-pivot quicksort for primitives.
- **When beat O(n log n)?** Counting/radix for bounded integer keys.

## Related Topics
- [[QuickSort and MergeSort]] · [[Heap Sort]] · [[Binary Search]]

## Quick Revision
- Comparison sorts >= O(n log n). Merge (stable, O(n) space), quick (in-place, O(n²) worst), heap (in-place, O(n log n)). Counting/radix beat the bound for bounded ints. Java: TimSort (objects), dual-pivot quicksort (primitives).
