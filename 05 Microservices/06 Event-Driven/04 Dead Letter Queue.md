---
title: Dead Letter Queue
aliases:
  - Dead Letter Queue
  - DLQ
domain: Microservices
module: Event-Driven
status: Learning
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 4
tags:
  - microservices
related:
  - "[[Event-Driven Architecture]]"
---

# Dead Letter Queue (DLQ)

## Overview
A dead letter queue is a separate topic/queue where messages are sent after they repeatedly fail processing. It prevents a single bad ("poison") message from blocking a partition/queue forever while preserving it for investigation and replay.

## Why It Matters
Without a DLQ, a poison message either blocks the consumer (Kafka: stuck offset) or is silently dropped. The DLQ is the standard escape hatch for un-processable messages.

## How It Works
1. Consumer fails to process a message.
2. Retry with backoff up to a limit (sometimes via a **retry topic**).
3. On exhausting retries, publish to the **DLQ** (with metadata: original topic, error, stack, attempt count) and commit the offset so processing continues.
4. Operators inspect, fix the cause, and **replay** from the DLQ.

## Poison Message Causes
- Malformed payload / deserialization failure (schema mismatch — see [[Event Versioning]]).
- A persistent bug or a downstream that's permanently rejecting.
- Non-idempotent logic failing mid-way.

## Best Practices
- Include rich context on the DLQ message for diagnosis.
- Alert on DLQ growth (it means something is broken).
- Separate **transient** (retry) from **permanent** (DLQ immediately) failures.
- Support controlled replay after a fix.

## Interview Questions
- **What is a DLQ for?** Isolating messages that fail after retries so they don't block the stream, keeping them for analysis/replay.
- **What's a poison message?** One that can never be processed successfully (bad payload, schema mismatch, persistent bug).
- **Retry vs DLQ?** Retry transient failures with backoff; route permanent failures to the DLQ.

## Related Topics
- [[Event-Driven Architecture]] · [[Event Versioning]] · [[Retry]] · [[Idempotency]]

## Quick Revision
- Parked queue for messages failing after retries (poison messages). Retry transient, DLQ permanent; attach context, alert on growth, support replay. Unblocks the stream.
