---
title: Strings
aliases:
  - Strings
domain: DSA
module: Arrays and Strings
status: Learning
difficulty: Easy
priority: High
interview: 4
revision: Weekly
order: 2
tags:
  - dsa
related:
  - "[[Arrays and Strings Index|Arrays and Strings]]"
---

# Strings

## Overview
A string is an immutable sequence of characters. In Java, `String` is backed by a `char[]` (byte[] since Java 9 compact strings) and is **immutable** — every "modification" creates a new object. Use `StringBuilder` for in-place building.

## Why It Matters
String problems (palindromes, anagrams, substrings, parsing) are interview staples, and the immutability/`StringBuilder` distinction is a frequent performance gotcha.

## Immutability & Building
```java
String s = "abc";
s += "d";                 // creates a new String each time - O(n) per op

StringBuilder sb = new StringBuilder();
for (char c : chars) sb.append(c);   // O(1) amortized per append
String result = sb.toString();
```
Concatenating in a loop with `+` is O(n²); use `StringBuilder` -> O(n).

## Common Operations
```java
s.charAt(i); s.length(); s.substring(a, b);      // substring is O(k)
s.indexOf("x"); s.split(","); s.toCharArray();
s.equals(t);                 // value equality - never use == for content
Character.isDigit(c); Character.toLowerCase(c);
```

## Common Patterns
- **Frequency map / int[26]** — anagrams, character counts.
- **[[Two Pointers]]** — palindrome check, reverse.
- **[[Sliding Window]]** — longest substring without repeats.
- **[[Hashing Index|Hashing]]** — group anagrams, dedupe.

## Common Mistakes
- Using `==` instead of `.equals()` for content comparison.
- Building strings with `+` in loops (quadratic).
- Ignoring Unicode/`char` vs code point for non-ASCII.

## Interview Questions
- **Why is String immutable in Java?** Security, thread safety, and string-pool caching / hashcode caching.
- **String vs StringBuilder vs StringBuffer?** Immutable vs mutable vs mutable+synchronized.
- **Check anagram efficiently?** Count chars in an `int[26]` (or HashMap) in O(n) instead of sorting O(n log n).

## Related Topics
- [[Two Pointers]] · [[Sliding Window]] · [[Hashing Index|Hashing]] · [[StringBuilder]]

## Quick Revision
- Immutable char sequence; `+` in loops is O(n²) -> use StringBuilder. Compare with equals. Patterns: int[26] frequency, two pointers, sliding window.
