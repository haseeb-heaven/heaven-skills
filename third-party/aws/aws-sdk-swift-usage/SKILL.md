---
name: aws-sdk-swift-usage
description: >-
  AWS SDK for Swift development reference. Covers client initialization, credential
  management, S3 operations, error handling patterns, concurrency with async/await,
  and best practices for iOS/macOS/Linux deployment. Use when building Swift applications
  that interact with AWS services.
version: 1
---

# AWS SDK for Swift

Reference guide for using the AWS SDK for Swift on iOS, macOS, Linux, and other platforms.

## When NOT to Use

- JavaScript/Python/Go environments — use language-native SDKs
- Platform-universal libraries needing a single codebase — each platform needs its own AWS config

## Critical Warnings

**iOS background tasks have time limits** — Background URLSession sessions are limited; long-running uploads/download may be suspended by the OS. Implement `URLSessionDelegate.backgroundSessions` handlers properly.

**Credential storage on iOS** — Never store access keys in source code or plist files. Use Keychain Services via `AWSCognitoAuth` or IAM instance roles for EC2/Lambda targets.

**Linux support requires additional dependencies** — libcurl and OpenSSL must be installed on Linux. On Ubuntu: `apt-get install -y libcurl4-openssl-dev libssl-dev`.

## Common Workflows

| Task | Code Pattern | Details |
|------|-------------|---------|
| Configure client | `S3Client(region: "us-east-1", from: .default)` | Client initialization |
| Read credentials | `.default`, environment vars, shared file | [credentials.md](references/credentials.md) |
| Upload data | `client.putObject(...)` | S3 object upload |
| Download data | `client.getObject(...)` | S3 object retrieval |
| Handle errors | Check `SdkError` types | [error-handling.md](references/error-handling.md) |

## Best Practices

1. **Use async/await** — All SDK operations support Swift async/await natively; don't wrap in dispatch queues
2. **Reuse clients across requests** — Client construction is expensive; keep as singleton property
3. **Configure timeout explicitly** — Especially important for mobile networks with variable latency
4. **Handle offline gracefully** — Queue requests locally when network unavailable; sync when back online
5. **Use request signing properly** — SigV4 signatures expire; refresh credentials before sending

## References

- [Configuration & Initialization](references/configuration.md)
- [Credentials Management](references/credentials.md)
- [S3 Operations](references/s3-operations.md)
- [Error Handling](references/error-handling.md)
- [Concurrency Patterns](references/concurrency-patterns.md)

**Author:** Amazon Web Services (AWS)
