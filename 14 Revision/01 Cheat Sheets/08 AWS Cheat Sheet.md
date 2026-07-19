---
title: AWS Cheat Sheet
aliases:
  - AWS Cheat Sheet
domain: Revision
module: Cheat Sheets
status: Learning
difficulty: Medium
priority: Medium
interview: 4
revision: Weekly
order: 8
tags:
  - revision
  - aws
---

# AWS Cheat Sheet

> Interview-ready revision for [[AWS]] (4–5 YOE). Service selection, trade-offs, and Q&A with answers.

---

## 1. Compute
| Service | Use | Watch out |
|---------|-----|-----------|
| EC2 | full control VMs | you patch/scale/manage |
| Lambda | event-driven, short tasks | 15-min max, cold starts, /tmp, concurrency limits |
| ECS/Fargate | containers, no node mgmt | AWS-native orchestration |
| EKS | managed Kubernetes | portable, more ops |
- Auto Scaling Groups + target tracking; scale on the metric reflecting real load (CPU, queue depth, RPS).

## 2. Storage & Databases
| Service | Type | Notes |
|---------|------|-------|
| S3 | object | 11 nines durability, versioning/lifecycle, event notifications; not a filesystem |
| EBS | block | single-AZ, one EC2 at a time |
| EFS | file (NFS) | multi-AZ shared |
| RDS | managed relational | Multi-AZ = HA standby; read replicas = read scaling |
| Aurora | cloud-native relational | faster failover, up to 15 replicas, storage auto-grows |
| DynamoDB | managed NoSQL | single-digit-ms; **partition-key design is everything**; on-demand vs provisioned + auto scaling; GSIs |
| ElastiCache | Redis/Memcached | caching, sessions, rate limiting, leaderboards |

## 3. Networking
- **VPC** = isolated network; public/private **subnets**, route tables, **IGW** (public egress), **NAT** (private egress).
- **Security Group** (stateful, instance-level, allow-only) vs **NACL** (stateless, subnet-level, allow + deny).
- **ALB** (L7: path/host routing, WebSocket) vs **NLB** (L4: ultra-low latency, static IP, TCP). **Route 53** (DNS + latency/health routing). **CloudFront** (CDN/edge + TLS).

## 4. Messaging (know the differences)
| Service | Model |
|---------|-------|
| SQS | queue; decouple; at-least-once; one consumer group; FIFO variant |
| SNS | pub/sub fan-out to many subscribers |
| Kinesis | ordered streaming, shards, replay window |
| EventBridge | event bus with content-based routing/filtering + schemas |
Pattern: SNS→SQS fan-out; SQS + Lambda for buffered async processing.

## 5. Security & Identity
- **IAM**: prefer **roles** (temporary creds) over long-lived keys; least privilege; identity vs resource policies; use roles for service-to-service and EC2/EKS (IRSA).
- **Secrets Manager** (rotation) / **SSM Parameter Store**; **KMS** for encryption at rest.

## 6. Observability & Well-Architected
- **CloudWatch** (metrics, logs, alarms, dashboards), **X-Ray** (tracing). Centralize logs; alarm on SLOs.
- **Well-Architected pillars:** Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization, Sustainability.

---

## 7. Interview Q&A (with answers)

**Q: EC2 vs Lambda vs Fargate — how do you choose?**
A: Lambda for spiky, short, event-driven work (pay per invocation, but cold starts + 15-min limit). Fargate for containerized services without managing nodes. EC2 when you need full control, special hardware, or long-running/stateful workloads.

**Q: S3 vs EBS vs EFS?**
A: S3 = object store (web assets, backups, data lake), accessed via API. EBS = block volume attached to one EC2 (like a disk). EFS = shared NFS across many instances/AZs.

**Q: RDS vs Aurora vs DynamoDB?**
A: RDS = managed standard engines (MySQL/Postgres). Aurora = AWS-optimized MySQL/Postgres with faster failover, more replicas, auto-scaling storage. DynamoDB = serverless NoSQL for predictable single-digit-ms at scale — model around the partition key/access patterns.

**Q: Security Group vs NACL?**
A: SG is stateful (return traffic auto-allowed), instance-level, allow-rules only. NACL is stateless (must allow both directions), subnet-level, supports allow **and** deny — used for coarse subnet guardrails.

**Q: ALB vs NLB?**
A: ALB is L7 — HTTP routing by path/host, TLS, WebSockets. NLB is L4 — extreme performance, static IPs, TCP/UDP, preserves source IP.

**Q: SQS vs SNS vs Kinesis vs EventBridge?**
A: SQS = point-to-point queue (buffering, one consumer group). SNS = pub/sub fan-out. Kinesis = ordered, replayable streaming with shards. EventBridge = event bus with rich routing/filtering and schema registry.

**Q: How do you handle secrets and access on AWS?**
A: IAM roles with least privilege (no hard-coded keys), instance/pod roles for service auth, Secrets Manager/Parameter Store for secrets (with rotation), KMS for encryption.

**Q: How do you reduce Lambda cold starts?**
A: Provisioned concurrency, smaller packages, avoid heavy init, keep runtimes warm, and prefer lightweight runtimes; for the JVM, use SnapStart (where available).

---

## Revision Checklist
- [ ] Compute selection (EC2/Lambda/Fargate/EKS) + Lambda limits
- [ ] S3/EBS/EFS + RDS/Aurora/DynamoDB
- [ ] VPC, SG vs NACL, ALB vs NLB, Route 53/CloudFront
- [ ] SQS/SNS/Kinesis/EventBridge
- [ ] IAM roles/least privilege + Secrets Manager + KMS
- [ ] CloudWatch/X-Ray + Well-Architected pillars
