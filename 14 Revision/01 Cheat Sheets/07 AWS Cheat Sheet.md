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
order: 7
tags:
  - revision
  - aws
---

# AWS Cheat Sheet

> Mid-level recall for [[AWS]] — service selection and the trade-offs interviewers probe.

## Compute (pick by workload)
- **EC2** (full control), **Lambda** (event-driven, 15-min max, cold starts, /tmp, concurrency limits), **ECS/Fargate** (containers, no node mgmt), **EKS** (managed k8s).
- Auto Scaling groups + target tracking; scale on the metric that reflects load.

## Storage & Databases
- **S3**: object store, 11 nines durability, lifecycle/versioning, event notifications; not a filesystem.
- EBS (block, single-AZ, attach to one EC2) vs EFS (NFS, multi-AZ shared).
- **RDS** (managed relational) vs **Aurora** (cloud-native, faster failover/replicas) vs **DynamoDB** (managed NoSQL, single-digit-ms, partition-key design is everything, on-demand vs provisioned).
- ElastiCache (Redis) for caching/sessions/rate-limits.

## Networking
- VPC = private network; public/private subnets, route tables, IGW (public), NAT (private egress).
- **Security Groups** (stateful, instance-level, allow-only) vs **NACLs** (stateless, subnet-level, allow+deny).
- ALB (L7, path/host routing) vs NLB (L4, ultra-low latency, static IP). Route 53 (DNS + health-based routing), CloudFront (CDN/edge).

## Messaging (know the differences)
- **SQS** (queue, decouple, at-least-once, one consumer group), **SNS** (pub/sub fan-out), **Kinesis** (ordered streaming, shards, replay), **EventBridge** (event bus + routing/filtering).

## Security & Ops
- IAM: roles > long-lived keys; least privilege; policies (identity vs resource); use roles for service-to-service.
- Secrets Manager / SSM Parameter Store; KMS for encryption.
- Observability: CloudWatch (metrics/logs/alarms), X-Ray (tracing). Well-Architected pillars: ops, security, reliability, performance, cost, sustainability.

## Sharp Interview Answers
- EC2 vs Lambda vs Fargate; Lambda cold-start/limits.
- S3 vs EBS vs EFS; RDS vs Aurora vs DynamoDB.
- SG vs NACL; ALB vs NLB.
- SQS vs SNS vs Kinesis vs EventBridge.

## Revision Checklist
- [ ] Compute options + when each
- [ ] S3/EBS/EFS + RDS/Aurora/DynamoDB
- [ ] VPC, SG vs NACL, ALB vs NLB
- [ ] SQS/SNS/Kinesis/EventBridge
- [ ] IAM least privilege + observability
