---
title: Prefix Sum
aliases:
  - Prefix Sum
domain: DSA
module: Arrays and Strings
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 5
tags:
  - dsa
related:
  - "[[Arrays]]"
---

# Prefix Sum

## Overview
A prefix-sum array stores cumulative sums so any range sum can be answered in O(1): `sum(i..j) = prefix[j+1] - prefix[i]`. Precompute once in O(n), then query many times in O(1).

## Why It Matters
It converts repeated O(n) range-sum queries into O(1), and underlies subarray-sum problems (with hashing) and 2D range queries.

## 1D Prefix Sum
```java
int[] prefix = new int[n + 1];              // prefix[0] = 0
for (int i = 0; i < n; i++)
    prefix[i + 1] = prefix[i] + a[i];
// range sum of a[i..j] inclusive:
int rangeSum = prefix[j + 1] - prefix[i];   // O(1)
```

## Subarray Sum = K (prefix + hashing)
```java
// Count subarrays summing to k: O(n)
Map<Integer,Integer> count = new HashMap<>();
count.put(0, 1);
int sum = 0, ans = 0;
for (int x : a) {
    sum += x;
    ans += count.getOrDefault(sum - k, 0);  // a prior prefix makes sum-k
    count.merge(sum, 1, Integer::sum);
}
```

## Variants
- **2D prefix sum** — O(1) submatrix sums after O(mn) precompute.
- **Difference array** — O(1) range updates, sum at the end (inverse idea).

## When To Use
- Many range-sum queries on a static array.
- "Count/where subarray sums to k" (combine with a hash map).
- Range updates (difference array).

## Interview Questions
- **How does prefix sum give O(1) range queries?** `prefix[j+1] - prefix[i]`; precompute cumulative sums once.
- **Subarray-sum-equals-k in O(n)?** Track running prefix sum in a hash map; look for `sum - k`.
- **When not to use it?** When the array changes frequently — updates are O(n); use a Fenwick/segment tree instead.

## Related Topics
- [[Arrays]] · [[Sliding Window]] · [[Hashing Index|Hashing]]

## Quick Revision
- Cumulative sums -> O(1) range queries after O(n) precompute. Range = prefix[j+1]-prefix[i]. With a hash map, count subarrays summing to k in O(n). Mutable data -> Fenwick tree.
