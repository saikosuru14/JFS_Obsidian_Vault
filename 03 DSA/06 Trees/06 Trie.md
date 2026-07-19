---
title: Trie
aliases:
  - Trie
  - Prefix Tree
domain: DSA
module: Trees
status: Learning
difficulty: Medium
priority: Medium
interview: 4
revision: Weekly
order: 6
tags:
  - dsa
related:
  - "[[Trees Index|Trees]]"
---

# Trie (Prefix Tree)

## Overview
A trie stores strings by sharing common prefixes: each node represents a character, and a path from the root spells a prefix. Lookups and inserts are O(L) where L is the word length — independent of how many words are stored.

## Why It Matters
Tries power autocomplete, spell-check, prefix search, and IP routing. They're the go-to when the problem is about **prefixes** rather than whole-key equality (where a hash map wins).

## Structure
```java
class TrieNode {
    TrieNode[] children = new TrieNode[26];   // or a Map for large alphabets
    boolean isWord;
}

void insert(TrieNode root, String w) {
    TrieNode cur = root;
    for (char c : w.toCharArray()) {
        int i = c - 'a';
        if (cur.children[i] == null) cur.children[i] = new TrieNode();
        cur = cur.children[i];
    }
    cur.isWord = true;
}
```
`search` walks the same way and checks `isWord`; `startsWith` just checks the path exists.

## Complexity
| Operation | Trie |
|-----------|------|
| insert / search / startsWith | O(L) |
| space | O(total chars × alphabet) |

## Trie vs Hash Map
- **Trie**: prefix queries, ordered traversal, autocomplete; more memory.
- **Hash map**: whole-key lookup O(1) average, no prefix support.

## Use Cases
Autocomplete, spell-checkers, word games (Boggle), IP routing tables, and "word search II" type problems.

## Interview Questions
- **When use a trie over a hash map?** When you need prefix operations (autocomplete, startsWith), not just exact-key lookup.
- **Complexity of trie operations?** O(L) in the word length, independent of dictionary size.
- **Downside of a trie?** Higher memory (a node per char, per alphabet slot).

## Related Topics
- [[Trees Index|Trees]] · [[Hash Tables]] · [[Strings]]

## Quick Revision
- Prefix tree; path = prefix, O(L) insert/search/startsWith regardless of count. Use for autocomplete/prefix search. More memory than a hash map; hash map for exact-key only.
