---
name: aws-observability
description: >-
  Builds, configures, and debugs AWS observability across CloudWatch, X-Ray, Application
  Signals, CloudTrail, and Synthetics. Covers custom metrics, dashboards, alarms, log
  insights, distributed tracing, dynamic instrumentation, and troubleshooting production
  issues. Use when monitoring, alerting, or debugging AWS-hosted applications.
version: 1
---

# AWS Observability

Domain expertise for building comprehensive observability solutions on AWS — metrics, logs, traces, alerts, and dashboards.

## When NOT to Use

- Non-AWS observability tools (Datadog, New Relic, PagerDuty) — use their native patterns
- Custom log aggregation (ELK/EFK on EC2) — use CloudWatch Logs instead

## Critical Warnings

**CloudWatch metric granularity has cost implications** — Standard resolution is 1-minute data points. High resolution (10-second) costs ~10x more per metric. Only enable HR for critical infrastructure.

**X-Ray sampling drops 90%+ of requests by default** — The `DefaultTotalSegments` and `DefaultTargetedRequests` controls drop most traffic. Configure sampling rules based on your QPS to ensure adequate trace coverage.

**CloudWatch Logs retention is irreversible** — Setting `retentionInDays` to permanent is permanent — you can only reduce it, not increase back to unlimited once set via policy.

## Common Workflows

| Task | Command/API | Details |
|------|-------------|---------|
| Create alarm | `cloudwatch:set-alarm-state` | Threshold-based or metric math |
| Build dashboard | `cloudwatch:PutDashboard` | [alarms.md](references/alarms.md) |
| Query logs | `logs:FilterLogEvents` | [log-insights.md](references/log-insights.md) |
| Enable tracing | `xray:put-sampled-traces` | [tracing.md](references/tracing.md) |
| Create synthetics | `cloudwatch:create-canary` | [synthetics.md](references/synthetics.md) |
| Dynamic inst. | DI scripts enabled | [dynamic-instrumentation.md](references/dynamic-instrumentation.md) |

## Metrics Priority Matrix

| Service | Must-Monitor | Nice-to-Have |
|---------|-------------|--------------|
| EC2 | CPUUtilization, StatusCheckFailed, DiskReadOps | NetworkIn, ElasticIPUsage |
| RDS | CPUUtilization, DatabaseConnections, ReadLatency | BufferPoolUsage, SwapUsage |
| Lambda | Duration, Errors, Throttles, IteratorAge | ProvisionedConcurrentExecutions |
| API Gateway | 4XXError, 5XXError, IntegrationLatency | StageVariables, CacheHitRate |
| SQS | ApproximateNumberOfMessagesVisible | NumberOfMessagesSent, AgeOfOldestMessage |

## References

- [Alarms](references/alarms.md)
- [Dashboards](references/dashboards.md)
- [Log Insights](references/log-insights.md)
- [Metrics](references/metrics.md)
- [Tracing](references/tracing.md)
- [Synthetics](references/synthetics.md)
- [Dynamic Instrumentation](references/dynamic-instrumentation.md)
- [CloudTrail](references/cloudtrail.md)
- [Troubleshooting](references/troubleshooting.md)
- [Application Signals Onboarding](references/application-signals-onboarding.md)

**Author:** Amazon Web Services (AWS)
