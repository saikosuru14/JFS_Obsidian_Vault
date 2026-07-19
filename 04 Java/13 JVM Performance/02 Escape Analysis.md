---
title: Escape Analysis
aliases:
  - Escape Analysis
domain: Java
module: JVM Performance
status: Learning
difficulty: Hard
priority: Medium
interview: 3
revision: Weekly
order: 2
tags:
  - java
  - performance
related:
  - "[[JIT Compilation]]"
  - "[[GC Tuning]]"
---

# Escape Analysis

## Overview
Escape analysis is a JIT optimization that determines whether an object **escapes** the method or thread that created it. If it provably doesn't, the JVM can avoid allocating it on the heap altogether.

## Why It Matters
It's why "just allocate a small object" is often free in hot code: the JIT can eliminate the allocation, cutting GC pressure without any code change. Understanding it tempers premature "avoid all allocations" instincts.

## Escape States
- **No escape** — object stays within the method -> eligible for scalar replacement / stack allocation.
- **Method escape** — passed to another method that might retain it.
- **Thread/global escape** — stored in a field or returned -> must live on the heap.

## Enabled Optimizations
- **Scalar replacement** — the object is never actually created; its fields become local variables in registers/stack. (This, not literal "stack allocation," is what HotSpot mainly does.)
- **Stack allocation** — conceptually allocate on the stack, freed automatically on return.
- **Lock elision** — if a synchronized object never escapes a thread, the JVM removes the lock entirely (`-XX:+EliminateLocks`).

## Example
```java
Point p = new Point(x, y);   // if p doesn't escape, JIT may
return p.dist();             // never allocate it - fields become locals
```

## Caveats
- Only kicks in after JIT warmup (see [[JIT Compilation]]); interpreted code still allocates.
- Escape analysis is conservative — passing the object to a non-inlined method usually defeats it.
- Enabled by default (`-XX:+DoEscapeAnalysis`); rarely tuned manually.

## Interview Questions
- **What optimizations can escape analysis enable?** Scalar replacement, stack allocation, and lock elision.
- **Does Java allocate objects on the stack?** Not literally by default — via scalar replacement the object may never be materialized at all.
- **When does it not apply?** Objects that escape (stored in fields, returned, or passed to non-inlined methods), or before JIT warmup.

## Related Topics
- [[JIT Compilation]] · [[GC Tuning]] · [[Memory Leaks in Java]]

## Quick Revision
- JIT proves an object doesn't escape -> scalar replacement / stack allocation / lock elision. Cuts GC pressure automatically. Needs warmup; defeated by escaping refs.
