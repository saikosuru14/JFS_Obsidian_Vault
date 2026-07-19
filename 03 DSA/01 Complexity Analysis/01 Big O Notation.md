---
title: Big O Notation
aliases:
  - Big O Notation
  - Big O
domain: DSA
module: Complexity Analysis
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 1
tags:
  - dsa
related:
  - "[[Complexity Analysis Index|Complexity Analysis]]"
  - "[[Time Complexity]]"
  - "[[Space Complexity]]"
  - "[[Amortized Analysis]]"
---

# Big O Notation

## Overview
Big O describes the **asymptotic upper bound** of an algorithm's growth as input size `n` increases. It drops constants and lower-order terms to capture how cost scales, not exact runtime. This is the sub-hub for complexity concepts.

## Why It Matters
It's the shared language for comparing algorithms in every interview and code review. Choosing O(n log n) over O(n²) is the difference between a solution that scales and one that times out.

## Common Classes (fastest to slowest)
| Big O | Name | Example |
|-------|------|---------|
| O(1) | constant | array index, HashMap get |
| O(log n) | logarithmic | binary search, balanced BST |
| O(n) | linear | scan an array |
| O(n log n) | linearithmic | efficient sorts (merge/quick) |
| O(n²) | quadratic | nested loops, bubble sort |
| O(2ⁿ) | exponential | naive subsets/recursion |
| O(n!) | factorial | permutations |

## Related Notations
- **O (Big O)** — upper bound (worst case). Most used.
- **Ω (Omega)** — lower bound (best case).
- **Θ (Theta)** — tight bound (upper = lower).

## Rules Of Thumb
- Drop constants: O(2n) -> O(n). Drop lower-order terms: O(n² + n) -> O(n²).
- Sequential steps add; nested loops multiply.
- Different inputs get different variables: O(a + b), not O(n).

## Interview Questions
- **What does Big O describe?** The asymptotic upper bound on growth (worst-case scaling), ignoring constants.
- **O vs Θ vs Ω?** Upper bound, tight bound, lower bound.
- **Why drop constants?** Asymptotic behavior dominates as n grows; constants are hardware/impl details.

## Related Topics
- [[Time Complexity]] · [[Space Complexity]] · [[Amortized Analysis]] · [[Binary Search]]

## Quick Revision
- Asymptotic worst-case growth, constants dropped. Know the ladder O(1)<log<n<n log n<n²<2ⁿ<n!. O/Ω/Θ = upper/lower/tight.
