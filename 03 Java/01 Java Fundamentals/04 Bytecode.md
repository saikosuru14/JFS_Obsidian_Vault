---
title: Bytecode
aliases:
  - Bytecode
domain: Java
module: Java Fundamentals
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 4
tags:
  - java
related:
  - "[[Compilation Process]]"
---

# Bytecode

## Overview
Bytecode is the platform-independent instruction set `javac` emits into `.class` files. The JVM is a **stack-based** virtual machine that executes these opcodes (`iload`, `iadd`, `invokevirtual`, ...).

## Why It Matters
Bytecode is the contract between compiler and JVM. It enables portability, JVM-level verification for safety, and JIT optimization. It's also why languages like Kotlin, Scala, and Groovy run on the JVM — they compile to the same bytecode.

## Inspecting It
```bash
javac Foo.java        # produces Foo.class
javap -c Foo          # disassemble bytecode
javap -p -v Foo       # verbose: constant pool, flags, stack map
```
Example: `a + b` on ints compiles to `iload`, `iload`, `iadd`, `ireturn` — operands pushed/popped on the operand stack.

## Key Properties
- **Portable** — same `.class` runs on any JVM.
- **Verified** — the bytecode verifier rejects unsafe/malformed code before execution.
- **Optimizable** — the JIT compiles hot bytecode to native code using runtime profiling.
- **Language-neutral** — any language that emits valid bytecode runs on the JVM.

## Interview Questions
- **What is bytecode?** The JVM's portable, verified intermediate instruction set produced by `javac`.
- **Is the JVM stack- or register-based?** Stack-based — instructions operate on an operand stack.
- **How do you view bytecode?** `javap -c` (disassemble) / `javap -v` (verbose).
- **Why can Kotlin/Scala run on the JVM?** They compile to the same bytecode format.

## Related Topics
- [[Compilation Process]] · [[Interpreter vs JIT Compiler]] · [[Class Loading]]

## Quick Revision
- Portable, verified, stack-based instruction set in `.class` files. Inspect with `javap -c`. Enables portability, safety, JIT, and polyglot JVM languages.
