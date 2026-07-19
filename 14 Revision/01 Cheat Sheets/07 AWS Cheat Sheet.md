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

> Fast recall for [[AWS]]. See the [[AWS Index|AWS domain]] for depth.

## Compute
- EC2 (VMs), Lambda (serverless functions), ECS/Fargate (containers), EKS (Kubernetes).
- Auto Scaling groups + launch templates; scale on metrics.

## Storage & Databases
- S3 (object storage, 11 nines durability, lifecycle/versioning), EBS (block), EFS (file).
- RDS (managed relational), DynamoDB (managed NoSQL, single-digit ms), ElastiCache (Redis/Memcached).

## Networking
- VPC = private network; subnets (public/private), route tables, IGW/NAT.
- Security Groups (stateful, instance-level) vs NACLs (stateless, subnet-level).
- Route 53 (DNS), ELB (ALB L7 / NLB L4), API Gateway, CloudFront (CDN).

## Messaging & Events
- SQS (queue, decoupling), SNS (pub/sub fan-out), EventBridge (event bus/routing).

## Security & Identity
- IAM users/roles/policies; least privilege; roles for service-to-service.
- Secrets Manager / SSM Parameter Store for secrets.

## Management & Monitoring
- CloudWatch (metrics/logs/alarms), CloudFormation (IaC), Systems Manager, AWS CLI.

## Top Interview One-Liners
- SG vs NACL: stateful/instance vs stateless/subnet.
- SQS vs SNS: queue (one consumer group) vs pub/sub fan-out.
- S3 vs EBS vs EFS: object vs block vs shared file.

## Revision Checklist
- [ ] Compute options and when to use each
- [ ] S3/RDS/DynamoDB selection
- [ ] VPC, SG vs NACL
- [ ] SQS vs SNS vs EventBridge
- [ ] IAM roles and least privilege
