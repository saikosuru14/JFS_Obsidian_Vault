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

> Mid-level recall for [[Kubernetes]] — scheduling, health, and debugging real failures.

## Objects
- Pod (smallest unit) ← ReplicaSet ← **Deployment** (rolling updates/rollback). StatefulSet (stable identity/storage), DaemonSet (per node), Job/CronJob (batch).
- Service types: ClusterIP (internal), NodePort, LoadBalancer; **Ingress** routes HTTP by host/path.

## Health & Resources (interview-heavy)
- Probes: **liveness** (restart if dead), **readiness** (remove from Service until ready), **startup** (slow starters). Bad liveness probe → restart loops.
- Requests (scheduling guarantee) vs limits (hard cap). **QoS**: Guaranteed (req==limit) > Burstable > BestEffort — affects eviction order.
- CPU limit → throttling; memory limit exceeded → **OOMKilled**. For JVM set `MaxRAMPercentage` under the memory limit.
- HPA scales on CPU/custom metrics; PodDisruptionBudget protects availability during drains.

## Config & Scheduling
- ConfigMap (non-secret) / Secret (base64, not encrypted at rest by default — enable encryption + RBAC). Mount as env or volume.
- Affinity/anti-affinity (spread replicas across nodes/zones), taints + tolerations (dedicated nodes), nodeSelector.
- NetworkPolicies restrict pod traffic (default is all-open).

## Debugging (know the failure modes)
```bash
kubectl get pods; kubectl describe pod X   # events: scheduling, image, probes
kubectl logs X [-p]                         # -p = previous (crash)
kubectl rollout status/undo deploy/app
kubectl top pod; kubectl get events --sort-by=.lastTimestamp
```
- **CrashLoopBackOff** (app exits / bad probe), **OOMKilled** (raise memory / fix leak), **ImagePullBackOff** (tag/creds), **Pending** (no resources / unschedulable).

## Ops
- Helm (templated charts) for packaging; RBAC (roles + bindings, least privilege).
- Rolling update: `maxSurge`/`maxUnavailable`; ensure readiness probe gates traffic.

## Sharp Interview Answers
- Deployment vs StatefulSet; liveness vs readiness.
- Requests vs limits + QoS + eviction; why a pod is OOMKilled.
- How a rolling update stays zero-downtime.
- Diagnosing CrashLoopBackOff / Pending.

## Revision Checklist
- [ ] Workloads + Service/Ingress
- [ ] Probes + requests/limits + QoS
- [ ] ConfigMap/Secret, affinity, taints, NetworkPolicy
- [ ] Debugging: describe/logs/events + failure modes
- [ ] Rolling updates, HPA, PDB, RBAC
