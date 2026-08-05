---
name: aws-containers
description: >-
  Deploys and operates containerized workloads on AWS using ECS, EKS, and App Runner.
  Covers task definitions, service deployment, Fargate capacity, logging with FireLens,
  debug exec, scaling strategies, ECR management, and infrastructure patterns. Use when
  building, deploying, or troubleshooting container applications on AWS.
version: 1
---

# AWS Containers

Domain expertise for managing containerized applications on AWS across ECS, EKS, and App Runner.

## When NOT to Use

- Local-only development without AWS targeting
- Non-container orchestration (use EC2/autoscaling for VMs)
- Serverless functions (use `aws-serverless` for Lambda)

## Critical Warnings

**ECS execution role missing policy** — Task definitions reference an IAM role that needs `AmazonECSTaskExecutionRolePolicy`. Without it, the agent can't pull images from ECR or write logs to CloudWatch.

**Fargate spot interruptions are instant** — Spot capacity can be reclaimed with 2-minute warning. Set appropriate `healthCheckGracePeriodSeconds` and use mixed-strategy placement.

**EKS kubeconfig stale tokens** — `eks:update-kubeconfig` must run before each session if using SSO. Old credentials cause silent auth failures.

## Common Workflows

| Task | Command/API | Details |
|------|-------------|---------|
| Create cluster | `ecs:create-cluster` or `eks:create-cluster` | Managed control plane |
| Deploy service | `ecs:describe-services` + update desired count | Rolling updates |
| Push image | `ecr:get-login-password` → docker login → push | [ecr-repository-management.md](references/ecr-repository-management.md) |
| Execute into container | `ecs:execute-command` | Requires Fargate Agent v1.1.0+ |
| Configure FireLens | Add firelens sidecar to task def | Structured log shipping |
| Scale service | Target tracking or step scaling policies | [service-scaling-and-updates.md](references/service-scaling-and-updates.md) |

## Platform Selection

| Platform | Best For | Compute Type |
|----------|----------|-------------|
| ECS Fargate | Simple deployments, no server management | Serverless |
| ECS EC2 | Cost optimization, custom instance types | Provisioned |
| EKS | Kubernetes ecosystem, multi-cloud portability | Both |
| App Runner | Quick web app deployment, auto HTTPS | Fully managed |

## References

- [App Runner Guide](references/app-runner-guide.md)
- [ECR Repository Management](references/ecr-repository-management.md)
- [ECS Exec Debugging](references/ecs-exec-debugging.md)
- [ECS Infrastructure Patterns](references/ecs-infrastructure-patterns.md)
- [ECS Logging & FireLens](references/ecs-logging-and-firelens.md)
- [ECS Troubleshooting Guide](references/ecs-troubleshooting-guide.md)
- [Fargate Service Deployment](references/fargate-service-deployment.md)
- [Fargate Spot](references/fargate-spot.md)
- [Service Scaling](references/service-scaling-and-updates.md)
- [Task Definition Authoring](references/task-definition-authoring.md)

**Author:** Amazon Web Services (AWS)
