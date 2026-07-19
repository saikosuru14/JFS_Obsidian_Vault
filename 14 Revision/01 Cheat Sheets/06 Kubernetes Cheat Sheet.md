---
title: Kubernetes Cheat Sheet
aliases:
  - Kubernetes Cheat Sheet
domain: Revision
module: Cheat Sheets
status: Learning
difficulty: Medium
priority: Medium
interview: 4
revision: Weekly
order: 6
tags:
  - revision
  - kubernetes
---

# Kubernetes Cheat Sheet

> Fast recall for [[Kubernetes]]. See the [[Kubernetes Index|Kubernetes domain]] for depth.

## Core Objects
- Pod = smallest unit (one or more containers, shared network/storage).
- ReplicaSet keeps N pods; Deployment manages ReplicaSets (rolling updates/rollback).
- StatefulSet = stable identity/storage; DaemonSet = one pod per node; Job/CronJob = batch.

## Networking
- Service types: ClusterIP (internal), NodePort, LoadBalancer.
- Ingress routes HTTP(S) by host/path; NetworkPolicies restrict pod traffic.

## Config & Storage
- ConfigMaps (non-secret) and Secrets (base64, sensitive) injected as env/volumes.
- PV (cluster resource) bound by PVC (claim); StorageClass for dynamic provisioning.

## Scaling & Health
- HPA scales replicas on metrics; VPA adjusts requests/limits.
- Requests (scheduling) vs limits (cap); probes: liveness (restart), readiness (traffic), startup.

## Operations
- Helm = package manager (charts); RBAC = roles + bindings for least privilege.

## Common Commands
```
kubectl get pods / describe pod X / logs X
kubectl apply -f manifest.yaml
kubectl rollout status/undo deployment/app
kubectl scale deployment app --replicas=3
```

## Top Interview One-Liners
- Deployment vs StatefulSet: stateless/interchangeable vs stable identity.
- Readiness vs liveness: serve traffic vs restart-if-dead.
- Requests vs limits: guaranteed vs maximum resources.

## Revision Checklist
- [ ] Pod/ReplicaSet/Deployment
- [ ] Service types & Ingress
- [ ] ConfigMap vs Secret; PV/PVC
- [ ] Probes; requests vs limits
- [ ] HPA and rollouts
