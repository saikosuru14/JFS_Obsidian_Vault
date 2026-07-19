---
title: Docker Index
aliases:
  - Docker
  - Docker Index
domain: Docker
module: Index
status: Learning
difficulty: Medium
priority: High
interview: 4
revision: Weekly
order: 0
tags:
  - docker
  - index
---

# Docker

> Domain hub — containerizing applications from image build to runtime.

## Overview
Docker packages applications and their dependencies into portable **containers** built from layered **images**. This domain covers the container model, image building, storage/networking, and distribution via registries and Compose.

## Learning Roadmap
1. [[Docker Fundamentals Index|Docker Fundamentals]] — architecture, containers, images, layers.
2. [[Building Images Index|Building Images]] — Dockerfile, multi-stage builds, best practices.
3. [[Storage and Networking Index|Storage & Networking]] — volumes and networks.
4. [[Registry and Compose Index|Registry & Compose]] — registries and multi-container apps.

## Suggested Study Order
Understand containers vs images first, then how to build efficient images, then how containers persist data and communicate, and finally how to distribute and orchestrate them locally.

## Prerequisites
- Basic [[Operating Systems]] concepts (processes, namespaces).

## Related Concepts
- [[Kubernetes]] — orchestrating containers at scale.
- [[CI-CD]] — building and shipping images in pipelines.

## Interview Focus
- Container vs virtual machine.
- Image layers and caching; multi-stage builds.
- Volumes vs bind mounts; Docker networking.

## Topic Tracker

> Live, auto-updating table of every note in this domain, grouped by module.

![[Docker.base]]
