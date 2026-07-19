---
title: JVM Internals Index
aliases:
  - JVM Internals Index
domain: Java
module: JVM Internals
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 0
tags:
  - java
  - index
related:
  - "[[Java Index|Java]]"
  - "[[JVM Architecture]]"
---

# JVM Internals

> Module index - part of the [[Java Index|Java]] learning path.

## Overview
The JVM turns portable `.class` bytecode into running native code. It **loads** classes, lays out memory in **runtime data areas**, and **executes** bytecode via an interpreter plus a JIT compiler — while a garbage collector reclaims memory. Understanding this pipeline explains startup vs warm-up performance, `ClassNotFound`/`NoClassDefFound` errors, and how tuning flags work.

## The Pipeline
```
.java --javac--> .class (bytecode)
   -> Class Loader (load, link, init)
   -> Runtime Data Areas (heap, stacks, PC, Metaspace)
   -> Execution Engine (interpreter + JIT)  -> native code
```

## Branch (expand)
- **[[JVM Architecture]]** — the hub: class loader, runtime data areas, execution engine, GC, JNI.
  - [[Class Loading]] — how classes are found, verified, initialized.
  - [[Runtime Data Areas]] — [[Program Counter Register]], [[Native Method Stack]] → [[JNI]].
  - [[Execution Engine]] — [[Interpreter vs JIT Compiler]].

## Learning Roadmap
1. [[JVM Architecture]]
2. [[Class Loading]] -> [[Runtime Data Areas]] -> [[Program Counter Register]] -> [[Native Method Stack]] -> [[JNI]]
3. [[Execution Engine]] -> [[Interpreter vs JIT Compiler]]

## Prerequisites
- [[Java Fundamentals Index|Java Fundamentals]]

## Next
- [[Memory Management Index|Memory Management]]

## Related Modules
- [[Java Index|Java]] · [[Memory Management Index|Memory Management]]

## Quick Revision
- Load -> link -> init classes; lay out runtime data areas; execute bytecode (interpret + JIT). Details in each note.
