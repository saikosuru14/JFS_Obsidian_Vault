---
title: Class Loading
aliases:
  - Class Loading
domain: Java
module: JVM Internals
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 2
tags:
  - java
related:
  - "[[JVM Architecture]]"
---

# Class Loading

## Overview
Class loading is how the JVM finds a `.class`, brings it into memory, verifies it, and prepares it for use — lazily, on first active use. It runs in three phases: **Loading -> Linking -> Initialization**.

## Why It Matters
It explains `ClassNotFoundException` vs `NoClassDefFoundError`, static-initializer timing, and framework tricks (hot reload, plugin isolation) built on custom class loaders.

## Phases
1. **Loading** — a `ClassLoader` reads the bytecode and creates a `Class` object in Metaspace.
2. **Linking**
   - *Verification* — bytecode is well-formed and safe.
   - *Preparation* — static fields get default values (0/null).
   - *Resolution* — symbolic references resolved to direct references.
3. **Initialization** — static initializers and static field assignments run (top to bottom).

## Class Loader Hierarchy + Parent Delegation
```
Bootstrap (core JDK)  ->  Platform/Extension  ->  Application (classpath)  ->  custom
```
A loader **delegates to its parent first**; only if the parent can't find the class does it load it itself. This prevents core classes from being spoofed (you can't replace `java.lang.String`) and avoids duplicate loading.

## Common Errors
- **`ClassNotFoundException`** — checked; class missing at load time (e.g., `Class.forName`).
- **`NoClassDefFoundError`** — class was present at compile time but missing/failed to init at runtime.
- **`ExceptionInInitializerError`** — a static initializer threw.

## Interview Questions
- **Three phases of class loading?** Loading, Linking (verify/prepare/resolve), Initialization.
- **What is parent delegation and why?** Ask the parent loader first — security (no spoofing core classes) and uniqueness.
- **ClassNotFoundException vs NoClassDefFoundError?** Missing at explicit load time vs missing/failed at runtime after being known at compile time.
- **When is a class initialized?** On first active use — `new`, static access, reflection — not merely when referenced.

## Related Topics
- [[JVM Architecture]] · [[Runtime Data Areas]] · [[Metaspace]]

## Quick Revision
- Load -> Link (verify/prepare/resolve) -> Init. Parent delegation for security + uniqueness. CNFE (load time) vs NoClassDefFoundError (runtime). Lazy init on first use.
