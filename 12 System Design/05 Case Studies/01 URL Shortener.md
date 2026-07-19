---
title: URL Shortener
aliases:
  - URL Shortener
domain: System Design
module: Case Studies
status: Not Started
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 1
tags:
  - system-design
---

# URL Shortener

## Requirements
- Shorten URLs
- Redirect quickly
- Analytics (optional)

## Design
- Hash/Base62 encoding
- Cache with Redis
- Store mappings in a database
- Use CDN for static assets

## Challenges
- Unique key generation
- High read traffic