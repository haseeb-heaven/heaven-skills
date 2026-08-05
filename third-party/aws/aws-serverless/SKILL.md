---
name: aws-serverless
description: >-
  Builds, deploys, and manages serverless applications on AWS using Lambda, API Gateway,
  Step Functions, EventBridge, and DynamoDB. Covers architecture patterns, concurrency
  controls, event sources, production hardening, deployment strategies, and troubleshooting.
  Use when designing or debugging serverless architectures on AWS.
version: 1
---

# AWS Serverless

Domain expertise for building production serverless applications on AWS.

## When NOT to Use

- Long-running processes (>15 min Lambda timeout) — use ECS/Fargate or SQS workers
- Stateful applications requiring persistent memory between requests — use Redis/ElastiCache
- Real-time WebSocket apps needing constant connections — consider App Runner or Fargate

## Critical Warnings

**Lambda cold starts are non-deterministic** — After idle periods, Lambda containers spin up fresh. Provisioned Concurrency eliminates this but costs money. For APIs, always test with provisioned concurrency enabled.

**Concurrent execution limits are account-wide** — Default is 1000 concurrent executions per region across ALL functions. If one function hogs the limit, others fail with `TooManyRequestsException`. Request increases proactively.

**API Gateway + Lambda integration has payload limits** — 10 MB (REST) or 20 MB (HTTP) request/response payload. Larger payloads must go through S3 with presigned URLs.

## Common Workflows

| Task | Command/API | Details |
|------|-------------|---------|
| Create function | `lambda:create-function` | Runtime, handler, role, layers |
| Deploy API | `apigateway:create-rest-api` → create resource → method → lambda integration | [api-gateway.md](references/api-gateway.md) |
| Orchestrate | Step Functions state machine definition JSON | [orchestration.md](references/orchestration.md) |
| Set concurrency | `lambda:update-function-concurrency` | Reserve for critical paths |
| Handle events | EventBridge rules → Lambda targets | [event-sources.md](references/event-sources.md) |
| Harden prod | Error handling, logging, monitoring | [production.md](references/production.md) |

## Architecture Patterns

| Pattern | Components | When to Use |
|---------|------------|-------------|
| **API backend** | API Gateway + Lambda + DynamoDB | REST/GraphQL APIs |
| **Event pipeline** | SNS/SQS → Lambda → DynamoDB | Asynchronous data processing |
| **Workflow** | Step Functions → Lambda → SQS | Multi-step business logic |
| **Scheduled job** | CloudWatch Events → Lambda | Cron-like tasks |
| **Real-time** | Kinesis/DynamoDB Streams → Lambda | Stream processing |

## References

- [API Gateway](references/api-gateway.md)
- [Architecture Patterns](references/architecture.md)
- [Concurrency Controls](references/concurrency.md)
- [Deployment Strategies](references/deployment.md)
- [Event Sources](references/event-sources.md)
- [Lambda Best Practices](references/lambda.md)
- [Orchestration](references/orchestration.md)
- [Production Hardening](references/production.md)
- [Troubleshooting](references/troubleshooting.md)

**Author:** Amazon Web Services (AWS)
