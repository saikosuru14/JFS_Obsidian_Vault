---
title: Hash Tables
aliases:
  - Hash Tables
  - Hash Table
domain: DSA
module: Hashing
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 1
tags:
  - dsa
related:
  - "[[Hashing Index|Hashing]]"
  - "[[Collision Handling]]"
  - "[[Hashing Patterns]]"
---

# Hash Tables

## Overview
A hash table stores key-value pairs in buckets indexed by `hash(key)`. With a good hash function and load factor, insert/lookup/delete are **average O(1)**; worst case degrades to O(n) (or O(log n) after treeify in Java's `HashMap`).

## Why It Matters
It's the workhorse for membership tests, frequency counts, caching, and deduplication — and the tool that turns most quadratic solutions linear.

## How It Works
1. Compute `hash(key)`, map to a bucket index (`(n-1) & hash` in Java).
2. Store the entry; collisions share a bucket ([[Collision Handling]]).
3. Resize (rehash) when the **load factor** (size/capacity, default 0.75) is exceeded.

See [[HashMap]] for Java internals (treeify at 8, resize doubling).

## Java Structures
```java
Map<String,Integer> freq = new HashMap<>();
freq.merge(word, 1, Integer::sum);           // frequency count
Set<Integer> seen = new HashSet<>();
seen.add(x);                                 // membership
Map<K,V> ordered = new LinkedHashMap<>();    // insertion order
Map<K,V> sorted  = new TreeMap<>();          // sorted keys, O(log n)
```

## Complexity
| Operation | Average | Worst |
|-----------|---------|-------|
| insert/get/delete | O(1) | O(n) / O(log n) treeified |

## Requirements For Keys
- Consistent `hashCode()` **and** `equals()` (equal objects -> equal hashCodes).
- Prefer **immutable** keys; mutating a key's hash-relevant fields corrupts lookups.

## Interview Questions
- **Average vs worst case?** O(1) average; O(n) worst (all collide), O(log n) in Java after treeify.
- **What must a key implement?** Consistent `equals` + `hashCode`; immutability recommended.
- **What is load factor?** size/capacity threshold (0.75) triggering resize to keep O(1).

## Related Topics
- [[Collision Handling]] · [[Hashing Patterns]] · [[HashMap]] · [[HashSet]]

## Quick Revision
- Key -> hash -> bucket, average O(1). Load factor 0.75 triggers resize. Keys need consistent equals/hashCode, ideally immutable. Worst case O(n)/O(log n).
