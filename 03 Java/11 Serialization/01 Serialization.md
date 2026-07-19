---
title: Serialization
aliases:
  - Serialization
domain: Java
module: Serialization
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - java
related:
  - "[[Serialization Index|Serialization]]"
  - "[[NIO]]"
---

# Serialization

## Overview
Serialization converts an object graph into a byte stream (and deserialization reconstructs it). Native Java serialization works by implementing the **marker** interface `Serializable`; `ObjectOutputStream`/`ObjectInputStream` do the work.

## Why It Matters
It appears in caching, session replication, and RMI — but it's also a top source of security vulnerabilities and versioning pain. Knowing *why to avoid it* is as important as knowing how it works.

## How It Works
```java
class User implements Serializable {
    private static final long serialVersionUID = 1L;
    private String name;
    private transient String password;   // NOT serialized
}

try (var out = new ObjectOutputStream(new FileOutputStream("u.ser"))) {
    out.writeObject(user);
}
```

## Key Mechanics
- **`transient`** — field is skipped (secrets, caches, derived data); restored as default (null/0) on read.
- **`serialVersionUID`** — version stamp. If it mismatches on read, deserialization throws `InvalidClassException`. Always declare it explicitly; the auto-generated value changes with any class edit and breaks compatibility.
- **`static`** fields aren't serialized (they belong to the class, not the instance).
- **`Externalizable`** — full manual control via `writeExternal`/`readExternal`.
- Whole graph is serialized; every referenced object must also be `Serializable` (else `NotSerializableException`).

## Why Avoid Native Serialization
- **Security** — deserializing untrusted bytes can trigger gadget-chain RCE; it's the root of many CVEs. Never deserialize untrusted input.
- **Versioning brittleness** — schema evolution is painful.
- **Cross-language** — the format is Java-only.
Prefer **JSON** (Jackson/Gson), **Protobuf**, or **Avro** — explicit schemas, safer, interoperable.

## Interview Questions
- **Purpose of serialVersionUID?** Version compatibility check between the writer and reader class; mismatch -> `InvalidClassException`.
- **What does `transient` do?** Excludes a field from serialization (secrets, derived/cached values).
- **Serializable vs Externalizable?** Marker + automatic vs full manual control of the format.
- **Why avoid Java serialization?** Deserialization security risks, versioning fragility, Java-only format — prefer JSON/Protobuf.

## Related Topics
- [[NIO]] · [[Reflection]]

## Quick Revision
- Object <-> bytes via `Serializable` + ObjectStreams. `transient` skips fields; declare `serialVersionUID`; statics/transients not written. Native form is insecure/brittle -> prefer JSON/Protobuf; never deserialize untrusted data.
