---
title: equals() vs ==
aliases:
  - equals() vs ==
domain: Java
module: Core Java
status: Not Started
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 3
tags:
  - java
  - core
related:
  - "[[Object Class]]"
  - "[[hashCode()]]"
---

# equals() vs ==

## Overview
`==` compares **references** (identity) for objects, or values for primitives. `equals()` compares **logical equality** when overridden (default `Object.equals` is identity).

## Example
```java
String a = "abc";
String b = new String("abc");
a == b;        // false — different objects
a.equals(b);   // true  — same content

String c = "abc";
a == c;        // true  — both from the string pool (interned literals)
```

## The equals Contract
Reflexive, symmetric, transitive, consistent, and `x.equals(null) == false`. Break these and collections misbehave.

## Best Practices
- Override `equals` and [[hashCode()]] together and consistently.
- Use `Objects.equals(a, b)` to null-safely compare.
- Compare by value fields, not by mutable state that can change after insertion into a set/map.
- `record` auto-generates value-based `equals`/`hashCode`.

## Common Mistakes
- Comparing objects (especially `Integer`/`String`) with `==`.
- Overriding `equals` but not `hashCode`.

## Interview Questions
- Output of `==` vs `equals` for `new String("abc")`?
- State the `equals` contract.
- Why does `Integer` caching make `==` "work" for small values but not large ones?

## Related Topics
- [[Object Class]] · [[hashCode()]] · [[String]]

## Quick Revision
- `==` identity/primitive value; `equals` logical (if overridden). Override with hashCode; use `Objects.equals`; records do it for you.
