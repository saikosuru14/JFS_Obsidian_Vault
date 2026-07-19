---
title: JDK vs JRE vs JVM
aliases:
  - JDK vs JRE vs JVM
domain: Java
module: Java Fundamentals
status: Learning
difficulty: Easy
priority: High
interview: 4
revision: Weekly
order: 2
tags:
  - java
related:
  - "[[Java Fundamentals Index|Java Fundamentals]]"
---

# JDK vs JRE vs JVM

## Overview
Three nested things people confuse: the **JVM** runs bytecode, the **JRE** adds the standard libraries needed to run apps, and the **JDK** adds the tools needed to build them.

## The Layers
```
+------------------------------------------+
| JDK  (build + run)                       |
|  javac, jar, javadoc, jdb, jstack ...    |
|  +------------------------------------+  |
|  | JRE  (run only)                    |  |
|  |  standard libraries (java.*)       |  |
|  |  +------------------------------+  |  |
|  |  | JVM  (execute bytecode)      |  |  |
|  |  |  class loader, GC, JIT       |  |  |
|  |  +------------------------------+  |  |
|  +------------------------------------+  |
+------------------------------------------+
```

| | Contains | Purpose |
|--|----------|---------|
| **JVM** | class loader, execution engine, GC | executes `.class` bytecode |
| **JRE** | JVM + core libraries | run Java apps |
| **JDK** | JRE + compiler & dev tools | develop + run Java apps |

## Notes
- Since Java 11, standalone JREs aren't shipped separately by Oracle — you get a JDK and can build a trimmed runtime with `jlink`.
- The JVM is implementation-specific (HotSpot, OpenJ9); bytecode is portable across all of them.

## Interview Questions
- **Difference between JDK, JRE, JVM?** JDK = JRE + dev tools; JRE = JVM + libraries; JVM = the bytecode execution engine.
- **Which do you need to run vs build?** Run: JRE (or JDK). Build: JDK.
- **Is the JVM platform-independent?** No — it's platform-specific; the bytecode it runs is portable.

## Related Topics
- [[JVM Architecture]] · [[Compilation Process]] · [[Bytecode]]

## Quick Revision
- JVM runs bytecode; JRE = JVM + libs (run); JDK = JRE + tools (build). Bytecode portable, JVM platform-specific.
