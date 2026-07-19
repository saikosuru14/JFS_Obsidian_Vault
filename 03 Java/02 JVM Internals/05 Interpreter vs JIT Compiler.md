---
title: Interpreter vs JIT Compiler
aliases:
  - Interpreter vs JIT Compiler
domain: Java
module: JVM Internals
status: Not Started
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 5
tags:
  - java
---

# Interpreter vs JIT Compiler

Interpreter:
- Executes bytecode instruction-by-instruction.
- Faster startup.

JIT Compiler:
- Compiles frequently executed ("hot") code into native machine code.
- Better long-running performance.

Interview:
Why does Java become faster after warm-up?
