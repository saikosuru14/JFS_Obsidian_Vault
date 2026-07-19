---
title: HashMap
aliases:
  - HashMap
domain: Java
module: Collections Framework
status: Completed
difficulty: Medium
priority: Medium
interview: 5
revision: Weekly
order: 13
tags:
  - java
related:
  - "[[Map]]"
  - "[[ConcurrentHashMap]]"
  - "[[Hashtable]]"
---

## Definition

`HashMap` is a hash table–based implementation of the `Map<K, V>` interface in Java. It stores data as **key-value pairs** and provides **average O(1)** time complexity for insertion, lookup, and deletion.

Unlike arrays, a HashMap allows retrieval using a **key** instead of an index.

```java
Map<Integer, String> map = new HashMap<>();

map.put(1, "Alice");
map.put(2, "Bob");

System.out.println(map.get(1));
```

Output

```
Alice
```

---

# Why HashMap?

Suppose we store one million users.

Searching inside an ArrayList:

```
Alice
Bob
Charlie
David
...
```

requires scanning elements one by one.

Time Complexity

```
O(n)
```

HashMap calculates where data should be stored using a hash function.

```
Key
 ↓
Hash Function
 ↓
Bucket
 ↓
Value
```

Hence lookup is approximately

```
O(1)
```

---

# Internal Architecture

```
HashMap

 ┌──────────────────────┐
 │ Bucket Array         │
 └──────────────────────┘

Index 0 → Node

Index 1 → Node → Node

Index 2 → Empty

Index 3 → TreeNode

Index 4 → Node
```

Each bucket contains

- nothing
- linked list
- red-black tree

---

# Internal Node Structure

Java internally stores entries like

```java
static class Node<K,V>{

    final int hash;

    final K key;

    V value;

    Node<K,V> next;

}
```

Each node stores

- hash
- key
- value
- pointer to next node

---

# How put() Works

Example

```java
map.put("Apple",100);
```

Steps

1. Calculate hash

```
hash("Apple")
```

↓

2. Calculate bucket index

```
index = hash % capacity
```

↓

3. Bucket empty?

YES

↓

Insert Node

If NO

↓

Collision occurs

↓

Linked list or Tree

---

# Example

Capacity

```
16
```

Hash

```
Apple -> 52

52 % 16 = 4
```

Store

```
Bucket 4

Apple
```

---

# Collision

Suppose

```
Apple

Banana
```

produce same bucket.

```
Bucket 5

Apple
   ↓

Banana
```

Both are stored.

---

# Collision Resolution

Java uses

Before Java 8

```
Linked List
```

After Java 8

If bucket size > 8

↓

Convert into

```
Red Black Tree
```

Search becomes

```
O(log n)
```

instead of

```
O(n)
```

---

# Load Factor

Default

```
0.75
```

Formula

```
Threshold

=

Capacity

×

Load Factor
```

Default capacity

```
16
```

Threshold

```
16 × 0.75

=

12
```

After 12 entries

↓

Resize

---

# Resize Process

Old Capacity

```
16
```

↓

New Capacity

```
32
```

↓

Recalculate bucket positions

↓

Move every node

This operation is expensive.

---

# Time Complexity

| Operation | Average | Worst |
|-----------|---------|-------|
| put | O(1) | O(n) |
| get | O(1) | O(n) |
| remove | O(1) | O(n) |
| containsKey | O(1) | O(n) |

After Java 8

Worst case

```
O(log n)
```

when bucket becomes tree.

---

# Null Keys

HashMap allows

```
One null key
```

```java
map.put(null,"Admin");
```

Valid.

---

# Null Values

Unlimited

```java
map.put(1,null);
map.put(2,null);
```

Perfectly valid.

---

# Duplicate Keys

```java
map.put(1,"Alice");

map.put(1,"Bob");
```

Result

```
1

↓

Bob
```

Old value overwritten.

---

# Iteration

```java
for(Map.Entry<Integer,String> e:map.entrySet()){

System.out.println(e.getKey());

}
```

---

# equals() and hashCode()

HashMap depends heavily on

```
hashCode()

equals()
```

Rule

Equal objects

↓

Must have

Same hashCode

---

Bad Example

```java
class Employee{

String name;

}
```

Without overriding

```
equals()

hashCode()
```

lookup may fail.

---

Good Example

```java
@Override

public int hashCode(){

return Objects.hash(id);

}
```

---

# Fail Fast Iterator

```java
Iterator<String> it=map.values().iterator();

map.put(5,"ABC");

it.next();
```

Throws

```
ConcurrentModificationException
```

---

# Java 7 vs Java 8

Java 7

```
Collision

↓

Linked List
```

Worst

```
O(n)
```

Java 8

```
Collision

↓

Tree

↓

O(log n)
```

---

# HashMap vs Hashtable

| Feature | HashMap | Hashtable |
|----------|----------|------------|
| Thread Safe | ❌ | ✅ |
| Null Key | ✅ | ❌ |
| Null Value | ✅ | ❌ |
| Performance | Faster | Slower |

---

# HashMap vs ConcurrentHashMap

HashMap

```
Not Thread Safe
```

ConcurrentHashMap

```
Thread Safe

High Performance
```

Uses finer-grained concurrency instead of synchronizing the entire map.

---

# Memory Diagram

```
Bucket Array

0

1

2

3

↓

Node

↓

Node

↓

TreeNode

↓

null
```

---

# Common Interview Questions

### Why is HashMap O(1)?

Because it computes the bucket index directly from the key's hash value, avoiding linear searches in the average case.

### Why is hashCode() important?

It determines the bucket where the key is stored.

### What happens if hashCode() is poor?

Many collisions occur, degrading performance.

### Why does Java 8 use Red Black Trees?

To improve worst-case lookup performance from O(n) to O(log n).

### Why is HashMap not synchronized?

To maximize performance. Use `ConcurrentHashMap` when concurrent access is required.

---

# Best Practices

✅ Use immutable keys whenever possible.

✅ Override both `equals()` and `hashCode()` consistently.

✅ Choose an appropriate initial capacity for large maps to reduce resizing.

✅ Avoid mutable objects as keys.

✅ Prefer `ConcurrentHashMap` in multithreaded applications.

---

# Summary

- HashMap stores key-value pairs.
- Average operations are O(1).
- Uses hashing to determine bucket location.
- Handles collisions with linked lists and, in Java 8+, red-black trees.
- Supports one `null` key and multiple `null` values.
- Not thread-safe.
- Depends on correctly implemented `equals()` and `hashCode()`.

# Revision Checklist

- [ ] Explain hashing
- [ ] Explain bucket indexing
- [ ] Explain collisions
- [ ] Explain load factor
- [ ] Explain resizing
- [ ] Explain treeification
- [ ] Compare HashMap vs Hashtable
- [ ] Compare HashMap vs ConcurrentHashMap
- [ ] Practice interview questions