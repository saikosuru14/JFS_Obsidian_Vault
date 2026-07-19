---
title: Merge Intervals
aliases:
  - Merge Intervals
domain: DSA
module: Arrays and Strings
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 6
tags:
  - dsa
related:
  - "[[Arrays and Strings Index|Arrays and Strings]]"
  - "[[Sorting Algorithms]]"
---

# Merge Intervals

## Overview
The merge-intervals pattern handles problems on ranges `[start, end]`: overlapping intervals are combined, gaps are found, or a new interval is inserted. The unlock is almost always **sort by start, then sweep once**.

## Why It Matters
Interval problems are a distinct, high-frequency interview family (merge intervals, insert interval, meeting rooms, non-overlapping intervals, interval intersections). Recognizing "these are ranges that may overlap" instantly suggests sort + sweep.

## Core Idea
```java
// Merge overlapping intervals: O(n log n)
Arrays.sort(intervals, (a, b) -> a[0] - b[0]);      // sort by start
List<int[]> merged = new ArrayList<>();
for (int[] iv : intervals) {
    if (merged.isEmpty() || merged.get(merged.size() - 1)[1] < iv[0])
        merged.add(iv);                              // no overlap -> new interval
    else
        merged.get(merged.size() - 1)[1] =           // overlap -> extend end
            Math.max(merged.get(merged.size() - 1)[1], iv[1]);
}
return merged.toArray(new int[0][]);
```

## Overlap Test
Two intervals `a` and `b` overlap when `a.start <= b.end && b.start <= a.end`. After sorting by start, you only compare each interval with the last merged one.

## Pattern Variants
| Problem | Approach |
|---------|----------|
| Merge intervals | sort by start, extend end on overlap |
| Insert interval | add non-overlapping before/after, merge the middle |
| Meeting rooms (can attend all?) | sort, check any overlap |
| Meeting rooms II (min rooms) | min-heap of end times, or sort starts/ends |
| Non-overlapping intervals (min removals) | sort by **end**, greedy keep earliest finish |
| Interval list intersections | two pointers over two sorted lists |

## Complexity
O(n log n) for the sort, O(n) sweep -> **O(n log n)** time, O(n) output.

## Interview Questions
- **First step for interval problems?** Sort by start (or by end for greedy scheduling).
- **When do two intervals overlap?** `a.start <= b.end && b.start <= a.end`.
- **Minimum meeting rooms?** Track concurrent meetings with a min-heap of end times (or a sweep of sorted start/end events) -> peak count.
- **Non-overlapping intervals (min removals)?** Greedy: sort by end, keep the earliest-finishing, drop overlaps.

## Related Topics
- [[Sorting Algorithms]] · [[Two Pointers]] · [[Heap]] · [[Greedy Approach]]

## Quick Revision
- Ranges that may overlap -> sort by start, sweep once, extend end on overlap (O(n log n)). Overlap: `a.start <= b.end && b.start <= a.end`. Min rooms = min-heap of ends; min removals = sort by end + greedy.
