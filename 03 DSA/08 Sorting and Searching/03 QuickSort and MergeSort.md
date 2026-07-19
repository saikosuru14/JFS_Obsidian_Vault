---
title: QuickSort and MergeSort
aliases:
  - QuickSort and MergeSort
  - QuickSort
  - MergeSort
  - Heap Sort
domain: DSA
module: Sorting and Searching
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 3
tags:
  - dsa
related:
  - "[[Sorting Algorithms]]"
---

# QuickSort and MergeSort

## Overview
The two canonical divide-and-conquer sorts. **Merge sort** splits, sorts halves, and merges — stable, guaranteed O(n log n), O(n) space. **Quicksort** partitions around a pivot and recurses — in-place, O(n log n) average but O(n²) worst. This note also covers **heap sort**.

## Why It Matters
They're the most-asked sorting internals, and the merge/partition routines reappear in other problems (count inversions, kth element, quickselect).

## Merge Sort
```java
void mergeSort(int[] a, int l, int r) {
    if (l >= r) return;
    int m = l + (r - l) / 2;
    mergeSort(a, l, m);
    mergeSort(a, m + 1, r);
    merge(a, l, m, r);              // merge two sorted halves - O(n)
}
```
- Stable, O(n log n) worst case, O(n) extra space.
- Great for linked lists and external sorting; the basis of counting inversions.

## Quick Sort
```java
void quickSort(int[] a, int lo, int hi) {
    if (lo >= hi) return;
    int p = partition(a, lo, hi);  // pivot in final place
    quickSort(a, lo, p - 1);
    quickSort(a, p + 1, hi);
}
```
- In-place, O(n log n) average, **O(n²) worst** (already-sorted with poor pivot).
- Mitigate worst case with randomized or median-of-three pivot.
- **Quickselect** (partition, recurse one side) finds the kth element in O(n) average.

## Heap Sort
Build a max-heap (O(n)), repeatedly extract the max to the end. In-place, O(n log n) worst case, but not stable and cache-unfriendly. See [[Heap]].

## Comparison
| | Merge | Quick | Heap |
|--|-------|-------|------|
| Worst | O(n log n) | O(n²) | O(n log n) |
| Space | O(n) | O(log n) | O(1) |
| Stable | yes | no | no |

## Interview Questions
- **Merge vs quick sort?** Merge: stable, O(n log n) guaranteed, O(n) space. Quick: in-place, faster in practice, but O(n²) worst.
- **How avoid quicksort's worst case?** Randomized/median-of-three pivot.
- **Find kth largest in O(n) average?** Quickselect (partition, recurse one side).

## Related Topics
- [[Sorting Algorithms]] · [[Heap]] · [[Binary Search]]

## Quick Revision
- Merge: split/merge, stable, O(n log n), O(n) space. Quick: partition, in-place, O(n log n) avg / O(n²) worst (randomize pivot); quickselect = kth in O(n) avg. Heap sort: in-place O(n log n), not stable.
