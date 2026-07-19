---
title: Sliding Window
aliases:
  - Sliding Window
domain: DSA
module: Arrays and Strings
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 4
tags:
  - dsa
related:
  - "[[Two Pointers]]"
---

# Sliding Window

## Overview
A sliding window maintains a contiguous range `[left, right]` over an array/string, expanding `right` to include elements and shrinking `left` to restore a constraint. It solves subarray/substring problems in O(n) instead of O(n²).

## Why It Matters
Any "longest/shortest/count of contiguous subarray or substring satisfying X" problem is a sliding-window candidate. Extremely common in interviews.

## Fixed-Size Window
```java
// Max sum of any window of size k: O(n)
int sum = 0, best;
for (int i = 0; i < k; i++) sum += a[i];
best = sum;
for (int i = k; i < n; i++) {
    sum += a[i] - a[i - k];      // add new, drop old
    best = Math.max(best, sum);
}
```

## Variable-Size Window
```java
// Longest substring without repeating chars: O(n)
Map<Character,Integer> last = new HashMap<>();
int left = 0, best = 0;
for (int right = 0; right < s.length(); right++) {
    char c = s.charAt(right);
    if (last.containsKey(c) && last.get(c) >= left)
        left = last.get(c) + 1;          // shrink past the duplicate
    last.put(c, right);
    best = Math.max(best, right - left + 1);
}
```

## Template
Expand `right`; while the window is invalid, advance `left`; update the answer each step.

## When To Use
- Contiguous subarray/substring with a constraint (sum, distinct chars, at most k).
- Fixed window (size k) or variable window (grow/shrink to satisfy a condition).

## Interview Questions
- **Sliding window vs two pointers?** Sliding window is a two-pointer specialization for contiguous ranges, tracking window state (sum/counts).
- **Fixed vs variable window?** Fixed size k slides by one; variable grows/shrinks to maintain a constraint.
- **How is it O(n)?** Each index enters and leaves the window at most once.

## Related Topics
- [[Two Pointers]] · [[Prefix Sum]] · [[Strings]] · [[Hashing Index|Hashing]]

## Quick Revision
- Contiguous range [left,right]; expand right, shrink left to keep it valid, update answer. O(n) since each element enters/leaves once. Fixed (size k) or variable.
