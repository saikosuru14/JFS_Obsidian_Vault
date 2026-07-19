---
title: Amortized Analysis
aliases:
  - Amortized Analysis
domain: DSA
module: Complexity Analysis
status: Learning
difficulty: Hard
priority: Medium
interview: 3
revision: Monthly
order: 4
tags:
  - dsa
related:
  - "[[Big O Notation]]"
---

# Amortized Analysis

## Overview
Amortized analysis measures the **average cost per operation over a sequence** of operations, when an occasional expensive operation is spread across many cheap ones. It's not the same as average-case (which is about input distribution) — amortized is a worst-case guarantee across a sequence.

## Why It Matters
It explains why `ArrayList.add` is "O(1)" despite occasional O(n) resizes, and why you shouldn't fear dynamic arrays/hash tables. A common interview follow-up.

## Canonical Example: Dynamic Array
When an `ArrayList` fills, it doubles capacity and copies all elements — an O(n) step. But doublings are rare: across n insertions the total copy work is n + n/2 + n/4 + ... ≈ 2n, so the **amortized cost per add is O(1)**.

```java
List<Integer> list = new ArrayList<>();
for (int i = 0; i < n; i++) list.add(i);  // each add amortized O(1)
```

## Techniques
- **Aggregate** — total cost of n ops / n.
- **Accounting** — cheap ops "prepay" for future expensive ones (credits).
- **Potential** — a potential function tracks stored work.

## Where It Shows Up
- Dynamic arrays ([[Arrays]], `ArrayList`), hash-table resizing ([[Hash Tables]]), incrementing a binary counter, `StringBuilder`.

## Amortized vs Average vs Worst
- **Worst** — the single most expensive op (resize = O(n)).
- **Average** — expected over random inputs.
- **Amortized** — guaranteed average per op over any sequence (O(1) for ArrayList add).

## Interview Questions
- **Why is ArrayList add O(1) amortized?** Doubling makes total copy work ~2n over n inserts, so per-insert averages O(1).
- **Amortized vs average-case?** Amortized is a per-op guarantee across a sequence (no probability); average-case depends on input distribution.
- **Name amortized structures.** Dynamic array, hash table (resize), binary counter, StringBuilder.

## Related Topics
- [[Big O Notation]] · [[Arrays]] · [[Hash Tables]]

## Quick Revision
- Average cost per op across a sequence (worst-case guarantee, not probabilistic). ArrayList add = amortized O(1) via doubling (~2n total). Techniques: aggregate, accounting, potential.
