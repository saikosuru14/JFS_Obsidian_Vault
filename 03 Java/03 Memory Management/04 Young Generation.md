---
title: Young Generation
aliases:
  - Young Generation
domain: Java
module: Memory Management
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 4
tags:
  - java
related:
  - "[[Heap Memory]]"
  - "[[Old Generation]]"
---

# Young Generation

## Overview
The Young Generation holds newly allocated objects. It is split into **Eden** and two **Survivor** spaces (S0/S1). Because most objects die young, collecting this small region frequently (a **Minor GC**) reclaims most garbage cheaply.

## Why It Matters
Young GC frequency and copy cost dominate allocation-heavy service latency. Right-sizing the Young Gen reduces both Minor GC frequency and premature promotion.

## How It Works
1. New objects allocate in **Eden**.
2. Eden fills -> **Minor GC**: live objects copied to a Survivor space; Eden cleared.
3. Objects bounce between S0/S1 on each Minor GC; an **age** counter increments.
4. When age crosses the **tenuring threshold** (`-XX:MaxTenuringThreshold`), the object is **promoted** to the [[Old Generation]].

Minor GC is a **copying** collector: it copies survivors and leaves Eden empty, so allocation is a fast pointer bump.

## Gotchas
- **Premature promotion** — a too-small Young Gen or Survivor space pushes still-live objects to Old Gen, increasing costly Major GCs.
- Large objects may skip Eden and allocate directly in Old Gen.

## Interview Questions
- **Why two Survivor spaces?** Copying collection needs a clean target space; alternating S0/S1 compacts survivors and avoids fragmentation.
- **What is a Minor GC?** Collection of the Young Gen — frequent, short, stop-the-world (in most collectors).
- **When is an object promoted?** After surviving enough Minor GCs (age >= tenuring threshold) or if Survivor space overflows.

## Related Topics
- [[Old Generation]] · [[Heap Memory]] · [[Garbage Collection Overview]]

## Quick Revision
- Eden + S0/S1. New objects in Eden; Minor GC copies survivors, ages them, promotes to Old at the tenuring threshold. Most objects die here.
