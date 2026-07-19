---
title: Hashing Patterns
aliases:
  - Hashing Patterns
domain: DSA
module: Hashing
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 3
tags:
  - dsa
related:
  - "[[Hash Tables]]"
---

# Hashing Patterns

## Overview
Practical patterns that use a hash map/set to reduce time complexity, usually by trading O(n) space to remember what you've seen.

## Why It Matters
Recognizing "I can remember seen values / counts in a map" is the fastest way to move from O(n²) to O(n) in an interview.

## Core Patterns
### 1. Seen-set / complement (two-sum)
```java
Map<Integer,Integer> seen = new HashMap<>();
for (int i = 0; i < n; i++) {
    if (seen.containsKey(target - a[i])) return new int[]{seen.get(target - a[i]), i};
    seen.put(a[i], i);
}
```

### 2. Frequency counting
```java
Map<Character,Integer> freq = new HashMap<>();
for (char c : s.toCharArray()) freq.merge(c, 1, Integer::sum);
// anagrams, majority element, top-k
```

### 3. Grouping by key
```java
// Group anagrams: key = sorted chars (or char-count signature)
Map<String,List<String>> groups = new HashMap<>();
for (String w : words)
    groups.computeIfAbsent(signature(w), k -> new ArrayList<>()).add(w);
```

### 4. Prefix sum + map
Count subarrays summing to k in O(n) — see [[Prefix Sum]].

### 5. Deduplication / membership
`HashSet` for O(1) contains; detect duplicates, cycle presence, visited nodes in [[BFS]]/[[DFS]].

## Trade-off
These spend O(n) memory to save time. State it explicitly in interviews.

## Interview Questions
- **How turn O(n²) into O(n)?** Remember seen values/counts/complements in a hash map/set.
- **Group anagrams key?** Sorted string or a 26-length count signature.
- **When is hashing the wrong choice?** When you need ordering/range queries (use a tree) or worst-case guarantees.

## Related Topics
- [[Hash Tables]] · [[Prefix Sum]] · [[Two Pointers]] · [[Sliding Window]]

## Quick Revision
- Map/set to remember seen/counts/complements -> O(n). Patterns: two-sum complement, frequency count, group-by-signature, prefix-sum+map, dedupe/visited. Costs O(n) space.
