---
title: Interpreter vs JIT Compiler
aliases:
  - Interpreter vs JIT Compiler
domain: Java
module: JVM Internals
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 5
tags:
  - java
related:
  - "[[Execution Engine]]"
---

# Interpreter vs JIT Compiler

## Overview
The JVM uses both: the **interpreter** executes bytecode immediately for fast startup, while the **JIT compiler** compiles hot methods to native code for fast steady-state performance. They work together, not as alternatives.

## Why It Matters
This is why Java is slower on the first requests and speeds up after warm-up — a frequent interview question and a real concern for short-lived processes (serverless, CLIs).

## Comparison
| | Interpreter | JIT Compiler |
|--|-------------|--------------|
| Unit | one bytecode at a time | whole hot method |
| Startup | fast | slower (compilation cost) |
| Steady-state | slower | fast (native code) |
| Optimizations | none | inlining, escape analysis, loop unrolling |

## How Hot Code Is Detected
The JVM counts method invocations and loop back-edges. When a counter crosses a threshold, the method is queued for JIT compilation. HotSpot **tiered compilation** ramps interpreted -> C1 -> C2.

## Key Optimizations
- **Inlining** — replace a call with the callee body (enables further optimization).
- **Escape analysis** — objects that don't escape a method can be scalar-replaced/stack-allocated, avoiding heap allocation.
- **Deoptimization** — if a speculative assumption breaks (e.g., a new subclass loads), the JIT falls back to the interpreter.

## Warm-up & AOT
Short-lived apps may never warm up. Options: `-XX:+TieredCompilation` tuning, GraalVM native image (AOT), or CDS/AppCDS to cut startup.

## Interview Questions
- **Why does Java get faster after warm-up?** Hot methods get JIT-compiled to optimized native code after enough executions.
- **Interpreter vs JIT — which does the JVM use?** Both — interpret first, compile hot paths.
- **What is deoptimization?** Reverting JIT-compiled code to interpreted when a speculative optimization becomes invalid.
- **What is escape analysis?** Proving an object doesn't escape a scope so it can skip heap allocation.

## Related Topics
- [[Execution Engine]] · [[JVM Performance Index|JVM Performance]]

## Quick Revision
- Interpret for startup, JIT-compile hot methods for speed. Tiered C1/C2. Optimizations: inlining, escape analysis; deopt on broken assumptions. Explains warm-up.
