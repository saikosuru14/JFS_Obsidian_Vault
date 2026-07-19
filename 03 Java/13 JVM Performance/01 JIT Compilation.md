---
title: JIT Compilation
aliases:
  - JIT Compilation
domain: Java
module: JVM Performance
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - java
  - performance
related:
  - "[[Escape Analysis]]"
  - "[[Interpreter vs JIT Compiler]]"
---

# JIT Compilation

## Overview
The JVM starts by interpreting bytecode, then the Just-In-Time compiler compiles "hot" methods to native code at runtime using profiling data. This is why the JVM gets faster after warmup.

## Why It Matters
Explains warmup behavior, why microbenchmarks need warmup, and why peak throughput arrives only after the JIT kicks in.

## How It Works
- **Tiered compilation** (default): C1 (fast, lightly optimized) → C2 (slower to compile, highly optimized) based on invocation/loop counts.
- Profiling drives optimizations: **inlining**, loop unrolling, dead-code elimination, [[Escape Analysis]], branch prediction.
- **Deoptimization**: speculative optimizations are undone if assumptions break (e.g., a new subclass loaded).

## Performance
- Warmup matters: measure steady-state, not the first iterations.
- Inlining is the highest-leverage optimization; huge methods may exceed inlining thresholds.
- `-XX:+PrintCompilation` shows JIT activity; JITWatch helps analyze.

## Best Practices
- Let the JIT work — don't hand-optimize prematurely.
- Keep hot methods small enough to inline.
- Benchmark with JMH (handles warmup and dead-code elimination).

## Common Mistakes
- Benchmarking cold JVM runs.
- Assuming interpreted-time behavior reflects production throughput.

## Interview Questions
- What is tiered compilation (C1 vs C2)?
- Why does the JVM need warmup?
- What is deoptimization?

## Related Topics
- [[Interpreter vs JIT Compiler]]
- [[Escape Analysis]]

## Quick Revision
- Interpret → profile → JIT-compile hot methods (C1→C2); inlining is key; measure steady-state with JMH.
