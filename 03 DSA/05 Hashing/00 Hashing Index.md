---
title: Hashing Index
aliases:
  - Hashing Index
  - Hashing
domain: DSA
module: Hashing
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 0
tags:
  - dsa
  - index
related:
  - "[[DSA Index|DSA]]"
  - "[[Hash Tables]]"
---

# Hashing

> Module index - part of the [[DSA Index|DSA]] learning path.

## Overview
Hashing maps keys to array indices via a hash function, giving average O(1) insert/lookup/delete. It's the single most useful technique for cutting time complexity in interviews — most O(n²) brute forces become O(n) with a hash map or set.

## Branch (expand)
- **[[Hash Tables]]** — the structure and its O(1) average behavior.
  - [[Collision Handling]] — chaining vs open addressing.
  - [[Hashing Patterns]] — how to apply maps/sets to problems.
    - [[Frequency Counting Pattern]] — tally counts to answer in O(n).

## Learning Roadmap
1. [[Hash Tables]]
2. [[Collision Handling]]
3. [[Hashing Patterns]]
4. [[Frequency Counting Pattern]]

## Prerequisites
- [[Stacks and Queues Index|Stacks and Queues]]

## Related
- [[DSA Index|DSA]] · [[HashMap]] · [[HashSet]]
- Next: [[Trees Index|Trees]]

## Quick Revision
- Hash function -> bucket -> O(1) average. Collisions via chaining/open addressing. Pattern: trade O(n) space to drop time from O(n²) to O(n).
