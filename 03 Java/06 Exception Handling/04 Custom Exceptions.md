---
title: Custom Exceptions
aliases:
  - Custom Exceptions
domain: Java
module: Exception Handling
status: Learning
difficulty: Easy
priority: Medium
interview: 3
revision: Weekly
order: 4
tags:
  - java
  - exceptions
related:
  - "[[Checked vs Unchecked Exceptions]]"
  - "[[Exception Handling Best Practices]]"
---

# Custom Exceptions

## Overview
Domain-specific exceptions make failures explicit and let callers handle them precisely. Extend `RuntimeException` for unchecked (the common default) or `Exception` for checked.

## How It Works
- Provide a constructor that accepts a `cause` so the original stack trace is preserved.
- Add fields only when they help callers act (e.g., an error code or the offending id).

## Example
```java
public class OrderNotFoundException extends RuntimeException {
    private final String orderId;
    public OrderNotFoundException(String orderId) {
        super("Order not found: " + orderId);
        this.orderId = orderId;
    }
    public String getOrderId() { return orderId; }
}
```

## Best Practices
- Prefer unchecked for most domain errors.
- Always chain the cause: `super(message, cause)`.
- Name by the problem (`PaymentDeclinedException`), not the layer.
- Group related exceptions under a small base class for boundary handling.

## Common Mistakes
- Creating an exception per method with no added value — reuse standard ones (`IllegalArgumentException`, `IllegalStateException`) when they fit.
- Storing heavy objects in the exception.

## Interview Questions
- When do you create a custom exception vs use a standard one?
- Checked or unchecked for domain exceptions, and why?
- How do you preserve the cause chain?

## Related Topics
- [[Checked vs Unchecked Exceptions]]
- [[Exception Handling Best Practices]]

## Quick Revision
- Extend `RuntimeException` by default; chain the cause; name by problem; don't over-create.
