---
title: Kubernetes Index
aliases:
  - Kubernetes
  - Kubernetes Index
domain: Kubernetes
module: Index
status: Learning
difficulty: Hard
priority: High
interview: 5
revision: Weekly
order: 0
tags:
  - kubernetes
  - index
---

# Kubernetes

> Domain hub — orchestrating containers from pods to production operations.

## Overview
Kubernetes is a container orchestration platform that schedules, scales, and heals workloads across a cluster. This domain moves from the core objects (pods, namespaces) through workloads, networking, config, storage, scaling, and operations.

## Learning Roadmap
1. [[Kubernetes Fundamentals Index|Kubernetes Fundamentals]] — architecture, namespaces, pods.
2. [[Workloads Index|Workloads]] — ReplicaSets, Deployments, StatefulSets, Jobs.
3. [[Networking Index|Networking]] — Services, Ingress, Network Policies.
4. [[Configuration and Secrets Index|Configuration & Secrets]] — ConfigMaps and Secrets.
5. [[Storage Index|Storage]] — Persistent Volumes and Claims.
6. [[Scaling and Health Index|Scaling & Health]] — autoscalers, resource limits, probes.
7. [[Operations and Security Index|Operations & Security]] — Helm, RBAC, best practices.

## Suggested Study Order
Start with the object model (pods, namespaces), then how workloads are declared and scaled, then networking and configuration, then storage, autoscaling/health, and finally packaging and security.

## Prerequisites
- [[Docker]] — containers and images.
- Basic [[Computer Networks]].

## Related Concepts
- [[CI-CD]] — deploying to clusters.
- [[AWS]] — managed Kubernetes (EKS).

## Interview Focus
- Pod scheduling and the control plane.
- Deployments vs StatefulSets; rolling updates.
- Services vs Ingress; ConfigMaps vs Secrets.
- Probes, resource requests/limits, and autoscaling.

## Topic Tracker

> Live, auto-updating table of every note in this domain, grouped by module.

![[Kubernetes.base]]
