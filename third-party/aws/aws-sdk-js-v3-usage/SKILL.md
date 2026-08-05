---
name: aws-sdk-js-v3-usage
description: >-
  AWS SDK for JavaScript v3 reference guide. Covers client configuration, credentials
  management, S3 operations, DynamoDB patterns, Lambda integration, error handling,
  performance optimization, TypeScript usage, and effective programming practices.
  Use when writing JavaScript/TypeScript code that interacts with AWS services.
version: 1
---

# AWS SDK for JavaScript v3

Reference guide for using the modular AWS SDK for JavaScript v3 (clients only, not legacy `@aws-sdk/client-*` monolith).

## When NOT to Use

- Node.js 12 or earlier — use v2 (`aws-sdk`)
- Browser applications without a proxy — SDK secrets don't belong in client-side code
- Server-side Python/Go/Rust apps — use language-specific SDKs

## Critical Warnings

**Tree shaking doesn't work at runtime** — ES module imports like `import { S3Client } from "@aws-sdk/client-s3"` reduce bundle size but every imported client still makes metadata requests on startup. Cold starts increase if you import many clients.

**Credential resolution order is complex** — The SDK checks: ① `process.env.AWS_ACCESS_KEY_ID`, ② `~/.aws/credentials`, ③ IAM role, ④ ECS container credentials, ⑤ EKS webhook. Explicitly set via `fromEnv()` or `fromIni()` when unsure.

**Retry logic defaults are conservative** — Default max retries is 3 with exponential backoff. For high-throughput workloads, configure `retryStrategy: RetryStrategyV2.standard()` to increase resilience.

## Common Workflows

| Task | Code Pattern | Details |
|------|-------------|---------|
| Configure client | `new S3Client({ region: "us-east-1" })` | [clients.md](references/clients.md) |
| Read credentials | `fromEnv()`, `fromIni()`, `fromProcess()` | [credentials.md](references/credentials.md) |
| Upload file | `s3.send(new PutObjectCommand(params))` | [s3.md](references/s3.md) |
| Query table | `dynamoDb.send(new ScanCommand(params))` | [dynamodb.md](references/dynamodb.md) |
| Handle errors | Check `err.name` for specific error types | [error-handling.md](references/error-handling.md) |
| Optimize perf | Reuse client instances, configure timeout | [performance.md](references/performance.md) |
| TS typing | Full type inference on commands | [typescript.md](references/typescript.md) |

## Best Practices

1. **Reuse client instances** — Client constructors are expensive; create once and reuse across invocations
2. **Use pagination correctly** — `Paginator` utilities handle page iteration automatically for list/scan operations
3. **Configure timeouts explicitly** — Don't rely on defaults, especially for network-bound operations
4. **Use Command objects** — v3 uses command-based API; each operation is a separate Command object sent to the client
5. **Error handling by name** — SDK errors have specific `.name` properties (`NoSuchKey`, `ConditionalCheckFailedException`) for precise matching

## References

- [Clients](references/clients.md)
- [Credentials](references/credentials.md)
- [DynamoDB](references/dynamodb.md)
- [Effective Practices](references/effective-practices.md)
- [Error Handling](references/error-handling.md)
- [Lambda Integration](references/lambda.md)
- [Performance](references/performance.md)
- [S3](references/s3.md)
- [Schemas](references/schemas.md)
- [Sigv4a](references/sigv4a.md)
- [TypeScript](references/typescript.md)

**Author:** Amazon Web Services (AWS)
