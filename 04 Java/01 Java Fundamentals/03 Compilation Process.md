---
title: Compilation Process
aliases:
  - Compilation Process
domain: Java
module: Java Fundamentals
status: Learning
difficulty: Easy
priority: Medium
interview: 3
revision: Weekly
order: 3
tags:
  - java
related:
  - "[[Java Fundamentals Index|Java Fundamentals]]"
  - "[[Bytecode]]"
---

# Compilation Process

## Overview
Java compilation is **two-stage**: `javac` compiles source to portable bytecode ahead of time, and the JVM turns that bytecode into native code at run time (interpret + JIT). This split is what delivers portability *and* runtime performance.

## The Pipeline
```
Foo.java  --javac-->  Foo.class (bytecode)
                          |
                    Class Loader (load/link/init)
                          |
                    Execution Engine (interpret + JIT)
                          |
                    native machine code
```

- **`javac`** — checks types/syntax, produces `.class` bytecode. This is **ahead-of-time** compilation to bytecode, not native code.
- **JVM** — loads classes lazily and executes; the JIT compiles hot methods to native code at run time.

## Why Bytecode?
Portability: one compiled artifact runs on any platform that has a JVM. The platform-specific step (native codegen) is deferred to the JVM, which can also optimize using runtime profiling.

## Interview Questions
- **Is Java compiled or interpreted?** Both — compiled to bytecode by `javac`, then interpreted and JIT-compiled by the JVM.
- **What does `javac` produce?** Portable `.class` bytecode, not native machine code.
- **Where does platform-specific code get generated?** In the JVM at run time (JIT), not by the compiler.

## Related Topics
- [[Bytecode]] · [[JDK vs JRE vs JVM]] · [[Interpreter vs JIT Compiler]] · [[Class Loading]]

## Quick Revision
- Two stages: javac -> bytecode (AOT, portable); JVM -> native (interpret + JIT at runtime). Portability + runtime optimization.
