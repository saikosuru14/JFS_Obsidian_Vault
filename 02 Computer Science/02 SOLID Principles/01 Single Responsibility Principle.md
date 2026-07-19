---
title: Single Responsibility Principle
aliases:
  - Single Responsibility Principle
  - SRP
domain: Computer Science
module: SOLID Principles
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 1
tags:
  - computer-science
  - solid
related:
  - "[[SOLID Principles]]"
---

# Single Responsibility Principle (SRP)

## Definition
A class should have **one, and only one, reason to change** — it should have a single responsibility.

## Violation
```java
class Report {
    String generate() { /* build report */ return ""; }
    void saveToDisk(String r) { /* file I/O */ }
    void email(String r) { /* SMTP */ }
}
```
This class changes for three unrelated reasons: report format, storage, and delivery.

## Fix — Separate Responsibilities
```java
class ReportBuilder { String generate() { return ""; } }
class ReportRepository { void save(String r) {} }
class ReportMailer { void email(String r) {} }
```

## Benefits
- Smaller, focused classes that are easy to understand and test.
- Changes stay localized.

## Interview Questions
- Give a real-world SRP violation and how you'd refactor it.
- How does SRP relate to cohesion?

## Related Notes
- [[SOLID Principles]]

## Revision Summary
- One class, one reason to change. Split mixed concerns (build/store/send).
