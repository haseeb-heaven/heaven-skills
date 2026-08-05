---
name: launch-with-aws
description: >-
  Migrates vibe-coded web apps to production-ready AWS infrastructure. Handles project
  discovery, architecture design, IAM roles, VPC networking, service selection, CI/CD
  pipeline setup, monitoring configuration, and deployment execution. Use when planning
  or executing a migration from local development to AWS cloud hosting.
version: 1
---

# Launch with AWS

Domain expertise for migrating web applications from local development to production-ready AWS infrastructure.

## When NOT to Use

- Simple static sites — use S3 + CloudFront directly without this full workflow
- Apps that will stay local only — don't force cloud adoption unnecessarily
- Real-time requirements better served by edge computing — consider CloudFront functions instead

## Critical Warnings

**Default VPC has insecure security groups** — Default SG allows all outbound traffic. Create custom SGs with explicit inbound rules before launching any resources. Never open port 22 to 0.0.0.0/0.

**IAM role trust relationships are not auto-created** — When linking services (e.g., Lambda → DynamoDB), you must explicitly create the trust policy. The `sts:AssumeRole` permission must be granted in the target resource's policy document.

**Cost surprises with data transfer** — Cross-region data transfer costs 2-10x same-region costs. Keep related services (app, database, cache) in the same region. Only cross-region for DR or compliance.

## Workflow Steps

### Phase 1: Discovery & Planning
1. **Analyze the app** — Stack, dependencies, data needs, expected traffic, scaling requirements
2. **Choose compute** — App Runner (simple), ECS (containers), EC2 (custom), Lambda (event-driven)
3. **Design data layer** — RDS (relational), DynamoDB (NoSQL), S3 (static objects)
4. **Plan networking** — Public subnet (ALB/front-end), private subnet (back-end/db)

### Phase 2: Infrastructure Setup
1. **Create VPC** — Subnets, route tables, NAT gateway, security groups
2. **Set up IAM** — Roles with least-privilege policies
3. **Deploy core services** — Compute, database, storage, CDN
4. **Configure DNS** — Route 53 hosted zone, A/AAAA records, ALB alias

### Phase 3: Deployment
1. **Build artifacts** — Docker image, static assets, server bundle
2. **Deploy to chosen services** — App Runner deploy, ECR push, CodePipeline setup
3. **Run smoke tests** — Verify health endpoints, database connectivity, API responses
4. **Monitor initial traffic** — CloudWatch dashboards, X-Ray tracing, error rates

## References

- [Launch Configuration Reference](references/launchwithaws-2026-06-15.json)
- [Archive Script](scripts/archive.py) — Archive project state before migration
- [Auth Flow](scripts/auth.py) — OAuth integration for managed deployments

**Author:** Amazon Web Services (AWS)
