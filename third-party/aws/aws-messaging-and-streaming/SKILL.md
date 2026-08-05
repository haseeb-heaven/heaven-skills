---
name: aws-messaging-and-streaming
description: >-
  Guides use of AWS messaging and streaming services including SQS, SNS, Kinesis,
  EventBridge, and MSK. Covers message queuing patterns, pub/sub architectures,
  event-driven design, stream processing, dead letter queues, and ordering guarantees.
  Use when building decoupled, event-driven applications on AWS.
version: 1
---

# AWS Messaging & Streaming

Domain expertise for building event-driven architectures using AWS messaging and streaming services.

## When NOT to Use

- Synchronous request/response patterns — use API Gateway + Lambda instead
- File/big object transfer — use S3 with presigned URLs
- Transactional database operations — use RDS/DynamoDB with proper ACID patterns

## Critical Warnings

**SQS message visibility timeout < process time** — If your consumer takes longer than the visibility timeout to process a message, the message becomes visible again and may be processed twice. Set `VisibilityTimeout` to at least 2x your max processing time, or use `ChangeMessageVisibility` to extend it mid-processing.

**SNS doesn't persist messages** — Unlike SQS, SNS is fire-and-forget. If a subscriber is down, messages are lost. Always pair SNS topics with SQS queues as subscribers for reliability.

**Kinesis shard throughput limits** — Each shard supports 1 MB/s input and 2 MB/s output. Exceeding this causes `ProvisionedThroughputExceeded` errors. Monitor `IncomingBytes` and `WriteBytes` metrics and scale shards accordingly.

## Common Workflows

| Task | Service | Details |
|------|---------|---------|
| Create queue | `sqs:create-queue` | Set FIFO for ordering, set DLQ for retries |
| Publish topic | `sns:publish` | Fan-out to multiple subscribers |
| Stream data | `kinesis:put-record` | Partition by shard key for ordering |
| Route events | `events:put-events` | EventBridge rule targets |
| Connect systems | EventBridge integration rules | Cross-service event handling |

## Architecture Patterns

| Pattern | Services | When to Use |
|---------|----------|-------------|
| **Queue-based load leveling** | SQS | Decouple producers from consumers |
| **Pub/Sub fan-out** | SNS → SQS | Distribute events to many subscribers |
| **Event sourcing** | Kinesis + DynamoDB | Track complete state history |
| **CQRS** | EventBridge → multiple consumers | Separate read/write workloads |
| **Saga pattern** | Step Functions + SNS/SQS | Distributed transactions across services |

## References

- [SQS Deep Dive](references/sqs-deep-dive.md)
- [SNS Configuration](references/sns-configuration.md)
- [Kinesis Streams](references/kinesis-streams.md)
- [EventBridge Routing](references/eventbridge-routing.md)
- [MSK Setup](references/msk-setup.md)
- [Messaging Best Practices](references/messaging-best-practices.md)

**Author:** Amazon Web Services (AWS)
