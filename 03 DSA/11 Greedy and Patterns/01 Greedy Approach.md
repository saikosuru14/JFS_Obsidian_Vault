---
title: Greedy Approach
aliases:
  - Greedy Approach
  - Greedy Algorithms
domain: DSA
module: Greedy and Patterns
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - dsa
related:
  - "[[Greedy and Patterns Index|Greedy and Patterns]]"
  - "[[Greedy vs DP]]"
---

# Greedy Approach

## Overview
A greedy algorithm builds a solution step by step, always taking the choice that looks best **right now**, never reconsidering. It works only when the problem has the **greedy-choice property** (a local optimum leads to a global optimum) and optimal substructure.

## Why It Matters
When applicable, greedy is simpler and faster (often O(n log n)) than DP. The risk is applying it where it doesn't hold — you must justify correctness, not assume it.

## When Greedy Works
- **Greedy-choice property** — a locally optimal choice is part of some global optimum.
- **Optimal substructure** — the remaining problem is the same kind.
- Prove correctness via an **exchange argument** (swapping to the greedy choice never worsens the solution).

## Classic Greedy Problems
- **Activity selection / interval scheduling** — pick the earliest finish time.
- **Huffman coding** — merge two least-frequent nodes.
- **Fractional knapsack** — take highest value/weight first (note: **0/1** knapsack needs [[Common DP Patterns|DP]]).
- **Dijkstra**, **Kruskal/Prim** MST — greedy at their core.
- Jump game, gas station, assign cookies.

## Example: Interval Scheduling
```java
// Max non-overlapping intervals: sort by end time, greedily pick
Arrays.sort(intervals, (a, b) -> a[1] - b[1]);
int end = Integer.MIN_VALUE, count = 0;
for (int[] iv : intervals)
    if (iv[0] >= end) { count++; end = iv[1]; }   // take earliest-finishing
```

## Interview Questions
- **When does greedy work?** With the greedy-choice property + optimal substructure; prove via exchange argument.
- **Greedy vs DP?** Greedy commits to local choices (no reconsideration); DP explores all choices — see [[Greedy vs DP]].
- **Fractional vs 0/1 knapsack?** Fractional is greedy (value density); 0/1 needs DP.

## Related Topics
- [[Greedy vs DP]] · [[Common DP Patterns]] · [[Shortest Path]]

## Quick Revision
- Take the best local choice, never revisit. Needs greedy-choice property + optimal substructure; prove with an exchange argument. Interval scheduling, Huffman, fractional knapsack, Dijkstra/MST. 0/1 knapsack is NOT greedy.
