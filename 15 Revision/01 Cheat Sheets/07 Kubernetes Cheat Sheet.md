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
order: 7
tags:
  - revision
  - kubernetes
---

# Kubernetes Cheat Sheet

> Interview-ready revision for [[Kubernetes]] (4–5 YOE). Concepts, YAML, tables, and Q&A with answers.

---

## 1. Architecture
- **Control plane:** API server (front door), etcd (state store), scheduler (places pods), controller-manager (reconciles desired vs actual).
- **Node:** kubelet (runs pods), kube-proxy (Service networking), container runtime (containerd).
- Everything is declarative: you post desired state; controllers reconcile toward it.

## 2. Workloads
| Object | Use |
|--------|-----|
| Pod | smallest unit (1+ containers, shared net/volume) |
| ReplicaSet | keeps N pod replicas |
| **Deployment** | manages ReplicaSets → rolling update/rollback (stateless) |
| StatefulSet | stable identity + storage (ordered, e.g. DBs) |
| DaemonSet | one pod per node (agents) |
| Job / CronJob | run-to-completion / scheduled |

## 3. Health & Resources (interview-heavy)
```yaml
resources:
  requests: { cpu: "250m", memory: "256Mi" }   # scheduling guarantee
  limits:   { cpu: "500m", memory: "512Mi" }   # hard cap
livenessProbe:  { httpGet: { path: /health/live,  port: 8080 }, initialDelaySeconds: 30 }
readinessProbe: { httpGet: { path: /health/ready, port: 8080 } }
```
- **Liveness** → restart if dead; **readiness** → remove from Service endpoints until ready; **startup** → for slow starters (guards liveness during boot).
- **QoS classes:** Guaranteed (requests==limits) > Burstable > BestEffort — decides **eviction order** under node pressure.
- CPU over limit → **throttled**; memory over limit → **OOMKilled**. For the JVM, set `-XX:MaxRAMPercentage` below the memory limit.

## 4. Config, Networking, Scheduling
- **ConfigMap** (non-secret) / **Secret** (base64, *not* encrypted at rest by default → enable encryption + RBAC). Mount as env or file.
- **Service** types: ClusterIP (internal), NodePort, LoadBalancer. **Ingress** = L7 HTTP routing by host/path. **NetworkPolicy** restricts pod traffic (default: all-allowed).
- Scheduling: nodeSelector, **affinity/anti-affinity** (spread replicas across nodes/zones), **taints + tolerations** (dedicated/again special nodes), topology spread.
- **PodDisruptionBudget** keeps min replicas available during voluntary disruptions (drains/upgrades).

## 5. Debugging (know the failure modes)
```bash
kubectl get pods -o wide
kubectl describe pod <p>          # Events: scheduling, image pull, probe failures
kubectl logs <p> [-c cont] [-p]   # -p = previous (crashed) container
kubectl get events --sort-by=.lastTimestamp
kubectl top pod ; kubectl rollout status/undo deploy/<d>
```
| Symptom | Likely cause |
|---------|-------------|
| CrashLoopBackOff | app exits / failing liveness / bad config |
| OOMKilled | memory limit too low / leak |
| ImagePullBackOff | wrong tag / registry creds |
| Pending | no schedulable node (resources/taints/affinity) |
| 503 via Service | readiness failing → no endpoints |

## 6. Rollouts & Scaling
- Rolling update: `maxSurge`/`maxUnavailable`; readiness gates traffic → zero-downtime. `kubectl rollout undo` to roll back.
- **HPA** scales replicas on CPU/custom metrics; **VPA** adjusts requests/limits; **Cluster Autoscaler** adds nodes.
- **Helm** = templated packaging (charts/values); **RBAC** = roles + bindings, least privilege.

---

## 7. Interview Q&A (with answers)

**Q: Deployment vs StatefulSet?**
A: Deployment manages interchangeable, stateless pods with fast rolling updates. StatefulSet gives stable network identity and per-pod persistent storage with ordered, controlled rollout — for stateful apps (DBs, brokers).

**Q: Liveness vs readiness vs startup probe?**
A: Liveness restarts a stuck container; readiness controls whether the pod receives traffic (removed from the Service until ready); startup protects slow-booting apps so liveness doesn't kill them prematurely.

**Q: Requests vs limits, and QoS?**
A: Requests are guaranteed for scheduling; limits are hard caps. QoS (Guaranteed/Burstable/BestEffort) is derived from them and determines eviction priority under pressure. CPU limit throttles; memory limit exceeded → OOMKilled.

**Q: How is a rolling update zero-downtime?**
A: New pods must pass readiness before old ones are terminated (`maxUnavailable`/`maxSurge`), so the Service always has healthy endpoints.

**Q: How do you debug CrashLoopBackOff / Pending?**
A: `kubectl describe pod` (Events) + `kubectl logs -p`. CrashLoop = app exits or bad probe/config; Pending = unschedulable (insufficient resources, taints, affinity, no matching node).

**Q: ConfigMap vs Secret — are Secrets secure?**
A: Both inject config; Secrets are only base64-encoded and not encrypted at rest by default. Enable etcd encryption, restrict with RBAC, and consider an external secrets manager.

**Q: How does a Service route to pods?**
A: A Service selects pods by label; kube-proxy programs routing to the ready endpoints. Only pods passing readiness are in the endpoint set.

---

## Revision Checklist
- [ ] Control-plane vs node components
- [ ] Deployment/StatefulSet/DaemonSet/Job
- [ ] Probes + requests/limits + QoS + eviction
- [ ] ConfigMap/Secret, Service/Ingress/NetworkPolicy, affinity/taints, PDB
- [ ] Debugging: describe/logs/events + failure-mode table
- [ ] Rolling updates + HPA/VPA/Cluster Autoscaler + Helm/RBAC
