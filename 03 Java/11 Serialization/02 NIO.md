---
title: NIO
aliases:
  - NIO
  - New IO
domain: Java
module: Serialization
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 2
tags:
  - java
related:
  - "[[Serialization Index|Serialization]]"
  - "[[Serialization]]"
---

# NIO (New I/O)

## Overview
NIO (Java 4+, extended as NIO.2 in Java 7) is a buffer- and channel-oriented I/O model that supports **non-blocking** operations and multiplexing via selectors. It complements the older stream-based `java.io`.

## Why It Matters
Classic blocking I/O needs one thread per connection, which caps scalability. NIO lets one thread manage thousands of connections — the foundation of high-performance servers (Netty, the Spring WebFlux stack).

## Core Concepts
| Concept | Role |
|---------|------|
| **Buffer** | fixed-size container (`ByteBuffer`) you read/write; has position/limit/capacity |
| **Channel** | bidirectional connection to a file/socket (`FileChannel`, `SocketChannel`) |
| **Selector** | one thread monitors many channels for readiness (multiplexing) |

## Blocking vs Non-Blocking
```
Blocking I/O:      1 thread per connection  -> thread-per-request, simple, limited scale
NIO (selectors):   1 thread, many channels  -> event-driven, scalable, more complex
```
A `Selector` blocks in `select()` until one of its registered channels is ready, then processes only those — avoiding idle threads.

## NIO.2 (java.nio.file)
Modern file API: `Path`, `Files`, `WatchService`.
```java
Path p = Path.of("data.txt");
List<String> lines = Files.readAllLines(p);
Files.write(p, bytes, StandardOpenOption.CREATE);
```

## Note on Virtual Threads
[[Virtual Threads]] (Java 21) make the simple blocking-per-request style scale again, reducing the need to write complex selector-based NIO by hand for many applications.

## Interview Questions
- **NIO vs classic IO?** Buffer/channel-based, non-blocking, selector multiplexing vs stream-based blocking, thread-per-connection.
- **What is a selector?** A component that lets one thread monitor many channels for I/O readiness.
- **Three core abstractions?** Buffers, channels, selectors.
- **How do virtual threads change this?** They let blocking-style code scale, easing the need for manual non-blocking NIO.

## Related Topics
- [[Serialization]] · [[Virtual Threads]]

## Quick Revision
- Buffer/channel/selector model; non-blocking, one thread for many connections. NIO.2 = Path/Files. Virtual threads reduce the need for hand-written selectors.
