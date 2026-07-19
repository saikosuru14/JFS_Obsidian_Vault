---
title: JNI
aliases:
  - JNI
  - Java Native Interface
domain: Java
module: JVM Internals
status: Learning
difficulty: Medium
priority: Low
interview: 2
revision: Monthly
order: 8
tags:
  - java
related:
  - "[[Native Method Stack]]"
---

# Java Native Interface (JNI)

## Overview
JNI is the bridge that lets Java code call into (and be called from) native libraries written in C/C++. Native methods are declared `native` in Java and implemented in a shared library loaded via `System.loadLibrary`.

## Why It Matters
It unlocks capabilities the JVM alone can't reach — OS-specific APIs, hardware, and mature C/C++ code — but at a real cost to safety and portability. Knowing the trade-offs is the interview point.

## How It Works
```java
public class NativeDemo {
    static { System.loadLibrary("demo"); }   // loads libdemo.so / demo.dll
    public native int compute(int x);        // implemented in C/C++
}
```
Calls cross the JVM/native boundary using the [[Native Method Stack]]; the JNI runtime maps Java types to native types.

## Use Cases
- Hardware / device access.
- Reusing legacy or performance-critical C/C++ libraries.
- OS-specific features not exposed by the standard library.

## Trade-offs
- **Reduced portability** — you now ship platform-specific binaries.
- **Safety** — native code can corrupt memory and crash the whole JVM (segfault, not an exception).
- **Debugging** — harder; spans two runtimes.
- **Overhead** — boundary crossings aren't free.

## Modern Alternative
Java 21+ offers the **Foreign Function & Memory (FFM) API** (Project Panama, `java.lang.foreign`) as a safer, simpler replacement for most JNI use cases.

## Interview Questions
- **What is JNI for?** Calling native C/C++ code from Java (and vice versa).
- **Main downsides?** Lost portability, memory-safety risks (can crash the JVM), harder debugging.
- **Modern alternative?** The Foreign Function & Memory API (Project Panama).

## Related Topics
- [[Native Method Stack]] · [[JVM Architecture]]

## Quick Revision
- Bridge to native C/C++ via `native` methods + `loadLibrary`. Powerful but hurts portability/safety and can crash the JVM. Prefer the FFM API (Java 21+) where possible.
