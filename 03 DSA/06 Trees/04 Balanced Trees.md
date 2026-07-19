---
title: Balanced Trees
aliases:
  - Balanced Trees
  - Self-Balancing Trees
domain: DSA
module: Trees
status: Learning
difficulty: Hard
priority: Medium
interview: 3
revision: Monthly
order: 4
tags:
  - dsa
related:
  - "[[Binary Search Tree]]"
---

# Balanced Trees

## Overview
Self-balancing BSTs automatically keep height O(log n) through rotations during insert/delete, guaranteeing O(log n) operations even for sorted input. The common ones are **AVL** and **red-black** trees.

## Why It Matters
They give the worst-case guarantees plain BSTs lack. Java's `TreeMap`/`TreeSet` and `HashMap`'s treeified buckets use red-black trees — so this shows up in real code.

## Rotations
Balance is restored via **left/right rotations** — local O(1) pointer rearrangements that reduce height while preserving the BST invariant.

## AVL vs Red-Black
| | AVL | Red-Black |
|--|-----|-----------|
| Balance | strict (heights differ ≤ 1) | looser (≤ 2× height) |
| Lookups | faster (more balanced) | slightly slower |
| Insert/delete | more rotations | fewer rotations |
| Used by | read-heavy | Java TreeMap, most libraries |

Red-black trees trade a bit of lookup speed for fewer rebalancing operations — the better all-round default, which is why the JDK uses them.

## Other Balanced Structures
- **B-tree / B+ tree** — high-fan-out, disk-friendly; used by databases and filesystems for indexes.

## Interview Questions
- **Why self-balancing trees?** Guarantee O(log n) even for sorted input, which degenerates a plain BST to O(n).
- **AVL vs red-black?** AVL is more strictly balanced (faster reads, more rotations); red-black balances less strictly (fewer rotations) — the common library choice.
- **What uses red-black trees in Java?** `TreeMap`, `TreeSet`, and treeified `HashMap` buckets.

## Related Topics
- [[Binary Search Tree]] · [[TreeMap]] · [[Collision Handling]]

## Quick Revision
- Auto-keep height O(log n) via rotations. AVL = strict (fast reads), red-black = looser (fewer rotations, JDK default). B/B+ trees for disk/DB indexes.
