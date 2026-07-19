---
title: Execution Engine
aliases:
  - Execution Engine
domain: Java
module: JVM Internals
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 4
tags:
  - java
related:
  - "[[JVM Architecture]]"
  - "[[Interpreter vs JIT Compiler]]"
---

# Execution Engine

## Overview
The execution engine runs the bytecode held in the runtime data areas. It combines an **interpreter** (immediate execution) with a **JIT compiler** (native compilation of hot code), plus the **garbage collector** that reclaims memory.

## Why It Matters
This is where Java's "slow to start, fast once warm" behavior comes from, and where profiling/JIT flags take effect.

## Components
- **[[Interpreter vs JIT Compiler|Interpreter]]** — decodes and executes bytecode one instruction at a time; fast startup, slower steady-state.
- **JIT Compiler** — compiles frequently executed ("hot") methods to native code, applying optimizations (inlining, escape analysis, loop unrolling).
- **Garbage Collector** — reclaims unreachable heap objects (see [[Garbage Collection Overview]]).

## How It Flows
```
Bytecode --interpret--> execute now
   |
   +--hot method detected--> JIT compile --> native code cache --> run fast
```
HotSpot uses **tiered compilation**: start interpreted, then C1 (fast, lightly optimized), then C2 (slower to compile, heavily optimized) for the hottest code. Profiling data gathered while interpreting guides these optimizations.

## Interview Questions
- **What does the execution engine contain?** Interpreter, JIT compiler, and garbage collector.
- **What is tiered compilation?** Progressive compilation from interpreted -> C1 -> C2 based on how hot the code is.
- **How does profiling help the JIT?** Runtime data (branch frequencies, receiver types) enables speculative optimizations like inlining and monomorphic dispatch.

## Related Topics
- [[Interpreter vs JIT Compiler]] · [[JVM Architecture]] · [[Garbage Collection Overview]]

## Quick Revision
- Runs bytecode via interpreter + JIT (+ GC). Tiered: interpret -> C1 -> C2 for hot code. Profiling drives optimizations. Explains warm-up.
