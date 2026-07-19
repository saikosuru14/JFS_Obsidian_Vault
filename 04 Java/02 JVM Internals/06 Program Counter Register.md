---
title: Program Counter Register
aliases:
  - Program Counter Register
  - PC Register
domain: Java
module: JVM Internals
status: Learning
difficulty: Easy
priority: Low
interview: 2
revision: Monthly
order: 6
tags:
  - java
related:
  - "[[Runtime Data Areas]]"
---

# Program Counter (PC) Register

## Overview
Each thread has its own PC register holding the address of the **current JVM instruction** being executed. It's tiny and per-thread, which is exactly what lets the JVM suspend and resume threads correctly.

## Why It Matters
It's the mechanism that makes context switching and multithreading work: when a thread is rescheduled, the PC tells the JVM where to resume.

## How It Works
- For Java methods: holds the address/offset of the current bytecode instruction.
- For native methods: value is **undefined** (execution is outside the JVM's bytecode, tracked by the [[Native Method Stack]]).
- Updated as each instruction executes; never throws `OutOfMemoryError`.

## Interview Questions
- **Why is the PC register per-thread?** So each thread independently tracks its own execution point across context switches.
- **What does the PC register hold during a native call?** Undefined — native execution isn't bytecode.

## Related Topics
- [[Runtime Data Areas]] · [[Native Method Stack]] · [[Thread Lifecycle]]

## Quick Revision
- Per-thread pointer to the current bytecode instruction. Enables context switching. Undefined during native calls; never OOMs.
