---
title: Security Filter Chain
aliases:
  - Security Filter Chain
domain: Spring
module: Spring Security
status: Not Started
difficulty: Medium
priority: Medium
interview: 3
revision: Weekly
order: 5
tags:
  - spring
---

# Security Filter Chain

Every incoming HTTP request passes through a chain of security filters.

Common filters:
- UsernamePasswordAuthenticationFilter
- BasicAuthenticationFilter
- ExceptionTranslationFilter
- AuthorizationFilter

Interview:
Why is filter order important?
