---
title: JVM Architecture
aliases:
  - JVM Architecture
domain: Java
module: JVM Internals
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - java
related:
  - "[[JVM Internals Index|JVM Internals]]"
  - "[[Class Loading]]"
  - "[[Runtime Data Areas]]"
  - "[[Execution Engine]]"
---

# JVM Architecture

## Overview
The JVM is a specification with many implementations (HotSpot, OpenJ9, GraalVM). Its job: load bytecode, manage memory, and execute code portably across platforms. This note is the module hub — expand each subsystem.

## Why It Matters
"Write once, run anywhere" and Java's runtime performance both come from this architecture. Knowing the subsystems lets you reason about class-loading errors, memory layout, and JIT behavior.

## Core Subsystems
```
        +---------------------------+
        |   Class Loader Subsystem  |  load -> link -> init
        +---------------------------+
                     |
        +---------------------------+
        |    Runtime Data Areas     |  heap, stacks, PC, Metaspace
        +---------------------------+
                     |
        +---------------------------+
        |     Execution Engine      |  interpreter + JIT + GC
        +---------------------------+
                     |
        +---------------------------+
        |   JNI / Native Libraries  |
        +---------------------------+
```
- **[[Class Loading|Class Loader]]** — finds, verifies, and initializes classes with parent delegation.
- **[[Runtime Data Areas]]** — memory regions: heap (shared), per-thread stacks, [[Program Counter Register|PC]], Metaspace.
- **[[Execution Engine]]** — interprets bytecode and JIT-compiles hot paths; includes the garbage collector.
- **[[JNI]]** — bridge to native C/C++ libraries.

## JVM vs JRE vs JDK
- **JVM** — the runtime that executes bytecode.
- **JRE** — JVM + standard libraries (run apps).
- **JDK** — JRE + dev tools (`javac`, `jar`, `jstack`) (build apps).

## Interview Questions
- **What are the JVM's main subsystems?** Class loader, runtime data areas, execution engine (+ GC), JNI.
- **JVM vs JRE vs JDK?** Runtime engine vs runtime + libs vs full dev kit.
- **Is the JVM platform-independent?** The bytecode is; the JVM itself is platform-specific — that's what abstracts the OS away.

## Related Topics
- [[Class Loading]] · [[Runtime Data Areas]] · [[Execution Engine]] · [[Garbage Collection Overview]]

## Quick Revision
- Subsystems: class loader -> runtime data areas -> execution engine (+GC) -> JNI. Bytecode is portable; the JVM is not. JDK > JRE > JVM.
