---
title: Spring Index
aliases:
  - Spring
  - Spring Index
domain: Spring
module: Index
status: Learning
difficulty: Medium
priority: High
interview: 5
revision: Weekly
order: 0
tags:
  - spring
  - index
---

# Spring

> Domain hub — from the IoC container to production-ready secure web services.

## Overview
Spring is the dominant Java application framework. It centers on **Inversion of Control** and **dependency injection**, then layers on Boot (auto-configuration), MVC (web), Data JPA (persistence), and Security.

## Learning Roadmap
1. [[Spring Core Index|Spring Core]] — IoC container, beans, DI, scopes, lifecycle.
2. [[Spring Boot Index|Spring Boot]] — auto-configuration, starters, external config, Actuator.
3. [[Spring MVC Index|Spring MVC]] — DispatcherServlet, controllers, request handling, validation.
4. [[Spring Data JPA Index|Spring Data JPA]] — entities, repositories, mappings, caching, locking.
5. [[Spring Security Index|Spring Security]] — authentication, authorization, JWT, OAuth2.

## Suggested Study Order
Start with Core (the mental model for everything Spring), then Boot (how real apps bootstrap), then MVC and Data JPA (the web + persistence workhorses), and finish with Security.

## Prerequisites
- [[Java]] — especially [[Core Java Index|Core Java]] and annotations.
- [[Object-Oriented Programming]] and [[SOLID Principles]] (Spring is DIP in practice).

## Related Concepts
- [[Microservices]] — Spring Cloud builds on Spring Boot.
- [[Database Fundamentals]] — underpins Spring Data JPA.

## Interview Focus
- IoC/DI, bean scopes and lifecycle.
- Auto-configuration and starters.
- Request lifecycle through the DispatcherServlet.
- JPA mappings, N+1 problem, caching, locking.
- Security filter chain, JWT vs OAuth2.

## Topic Tracker

> Live, auto-updating table of every note in this domain, grouped by module.

![[Spring.base]]
