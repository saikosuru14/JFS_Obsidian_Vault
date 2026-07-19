---
title: LinkedHashSet
aliases:
  - LinkedHashSet
domain: Java
module: Collections Framework
status: Not Started
difficulty: Easy
priority: Low
interview: 2
revision: Monthly
order: 9
tags:
  - java
  - collections
related:
  - "[[Set]]"
  - "[[HashSet]]"
---

# LinkedHashSet

## Overview
`HashSet` that also maintains **insertion order** by chaining entries in a doubly linked list (backed by `LinkedHashMap`).

## When to Use
- You need set semantics (uniqueness, O(1)) *and* predictable iteration order (e.g., stable, deduped output).

## Performance
- O(1) average add/contains/remove, like HashSet, with slightly higher memory for the linked pointers.

## Best Practices
- Choose over `HashSet` only when order matters; over `TreeSet` when you want insertion order rather than sorted order.

## Interview Questions
- HashSet vs LinkedHashSet vs TreeSet — order and cost?
- What backs LinkedHashSet?

## Related Topics
- [[Set]] · [[HashSet]]

## Quick Revision
- HashSet + insertion order (LinkedHashMap-backed), O(1), slightly more memory. Use when uniqueness + order both matter.
