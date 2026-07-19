---
title: Frequency Counting Pattern
aliases:
  - Frequency Counting Pattern
  - HashMap Frequency Pattern
domain: DSA
module: Hashing
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 4
tags:
  - dsa
related:
  - "[[Hashing Patterns]]"
---

# Frequency Counting Pattern

## Overview
The frequency-counting pattern uses a hash map (or a fixed array like `int[26]`) to tally how often each element/character appears, then answers questions from those counts in O(n). It's the single most common hashing technique in interviews.

## Why It Matters
A huge class of problems — anagrams, majority element, top-k frequent, first unique character, valid permutations — reduces to "count, then reason about the counts," turning nested-loop O(n²) checks into O(n).

## The Core
```java
Map<Character,Integer> freq = new HashMap<>();
for (char c : s.toCharArray())
    freq.merge(c, 1, Integer::sum);        // count++ (or getOrDefault + put)

// fixed alphabet is faster:
int[] count = new int[26];
for (char c : s.toCharArray()) count[c - 'a']++;
```

## Common Problems & Techniques
| Problem | Technique |
|---------|-----------|
| Valid anagram | compare two count maps / `int[26]` |
| Group anagrams | count-signature as the map key |
| Majority element | count > n/2 (or Boyer-Moore voting) |
| First unique character | count, then find the first with count 1 |
| Top-K frequent elements | count -> heap of size k, or bucket sort |
| Ransom note / permutation-in-string | compare/slide frequency windows |

## Top-K Frequent (count + heap)
```java
Map<Integer,Integer> freq = new HashMap<>();
for (int x : nums) freq.merge(x, 1, Integer::sum);
PriorityQueue<int[]> heap = new PriorityQueue<>((a, b) -> a[1] - b[1]); // min-heap by freq
for (var e : freq.entrySet()) {
    heap.offer(new int[]{e.getKey(), e.getValue()});
    if (heap.size() > k) heap.poll();      // keep k most frequent
}
```

## Frequency + Sliding Window
Anagram/substring problems combine a frequency map with a [[Sliding Window|sliding window]]: maintain counts as the window moves and compare against a target frequency.

## Interview Questions
- **How check if two strings are anagrams in O(n)?** Compare character frequency counts (`int[26]` or a map), not sorting.
- **Top-K frequent efficiently?** Count with a map, then a size-k min-heap -> O(n log k) (or bucket sort by frequency -> O(n)).
- **Map vs int[26]?** Fixed-size array is faster and simpler for a known small alphabet; map for arbitrary keys.

## Related Topics
- [[Hashing Patterns]] · [[Hash Tables]] · [[Heap]] · [[Sliding Window]]

## Quick Revision
- Tally counts in a map / `int[26]`, then reason -> O(n). Anagrams, majority, first-unique, top-k (count+heap or buckets). Combine with a sliding window for substring problems.
