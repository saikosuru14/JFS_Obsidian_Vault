---
title: Native Method Stack
aliases:
  - Native Method Stack
domain: Java
module: JVM Internals
status: Learning
difficulty: Easy
priority: Low
interview: 2
revision: Monthly
order: 7
tags:
  - java
related:
  - "[[Runtime Data Areas]]"
  - "[[JNI]]"
---

# Native Method Stack

## Overview
The native method stack is a per-thread stack that holds frames for **native (non-Java) method calls** made through [[JNI]]. It mirrors the JVM stack but for C/C++ code executing outside the bytecode world.

## Why It Matters
When Java calls into native libraries (OS APIs, hardware, legacy code), those calls need their own stack. Deep native recursion can also throw `StackOverflowError`.

## How It Works
- Created per thread alongside the JVM stack and PC register.
- Used only when a thread invokes a native method; otherwise idle.
- Its size and behavior are implementation-dependent (some JVMs merge it with the C stack).

## Interview Questions
- **What is the native method stack for?** Frames of native (JNI) method calls executing outside the JVM.
- **How does it differ from the JVM stack?** The JVM stack holds Java bytecode frames; the native stack holds native (C/C++) call frames.

## Related Topics
- [[JNI]] · [[Runtime Data Areas]] · [[Stack Memory]]

## Quick Revision
- Per-thread stack for native (JNI) calls. Separate from the Java stack. Implementation-dependent; deep native recursion can SOE.
