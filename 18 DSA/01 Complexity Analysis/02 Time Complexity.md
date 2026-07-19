---
title: Time Complexity
aliases:
  - Time Complexity
domain: DSA
module: Complexity Analysis
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 2
tags:
  - dsa
related:
  - "[[Big O Notation]]"
  - "[[Space Complexity]]"
---

# Time Complexity

## Overview
Time complexity expresses how an algorithm's running time grows with input size, in [[Big O Notation]]. You derive it by counting the dominant operations as a function of `n`.

## Why It Matters
It predicts whether a solution scales before you run it — essential for choosing between approaches and passing interview constraints (e.g., n = 10⁵ rules out O(n²)).

## How To Analyze
- **Single loop over n** -> O(n).
- **Nested loops** -> multiply: two nested over n -> O(n²).
- **Halving each step** -> O(log n) (binary search).
- **Divide and combine** -> often O(n log n) (merge sort).
- **Sequential blocks** -> add, keep the dominant term.

```java
// O(n^2): for each element, scan the rest
for (int i = 0; i < n; i++)
    for (int j = i + 1; j < n; j++)
        if (a[i] + a[j] == target) ...   // brute-force two-sum

// O(n) with a HashMap instead
Map<Integer,Integer> seen = new HashMap<>();
for (int i = 0; i < n; i++) {
    if (seen.containsKey(target - a[i])) return ...;
    seen.put(a[i], i);
}
```

## Best/Average/Worst
Report the case that matters — usually **worst case**. Example: quicksort is O(n log n) average but O(n²) worst; HashMap get is O(1) average, O(n) worst (or O(log n) after treeify).

## Input-Size Intuition (1s budget)
| n | feasible complexity |
|---|---------------------|
| ≤ 10 | O(n!) / O(2ⁿ) |
| ≤ 20 | O(2ⁿ) |
| ≤ 5,000 | O(n²) |
| ≤ 10⁶ | O(n log n) / O(n) |
| > 10⁷ | O(n) / O(log n) |

## Interview Questions
- **How do you find time complexity?** Count dominant operations vs n; multiply nested loops, add sequential blocks, drop constants.
- **Worst vs average case?** Report worst unless told otherwise; know where they differ (quicksort, hashing).
- **How does n guide the target complexity?** Large n forces near-linear/log solutions; small n allows exponential.

## Related Topics
- [[Big O Notation]] · [[Space Complexity]] · [[Sorting Algorithms]]

## Quick Revision
- Count dominant ops vs n. Nested = multiply, sequential = add. Report worst case. Use n to back into the required complexity.
