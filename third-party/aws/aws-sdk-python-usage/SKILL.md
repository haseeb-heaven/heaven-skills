---
name: aws-sdk-python-usage
description: >-
  AWS SDK for Python (boto3) reference guide. Covers client configuration, credentials,
  S3 operations, DynamoDB patterns, error handling, pagination, waiters, and effective
  programming practices. Use when writing Python code that interacts with AWS services.
version: 1
---

# AWS SDK for Python (boto3)

Reference guide for using boto3 — the official AWS SDK for Python.

## When NOT to Use

- Async-only applications — use `aioboto3` or the async-native `boto3` alternatives
- Performance-critical tight loops — consider the lower-level `botocore` directly or AWS CLI
- Non-Python environments — use language-specific SDKs

## Critical Warnings

**boto3 clients are thread-safe but not async-safe** — Share a single client across threads, but don't share across asyncio tasks without protection. Create per-task clients if needed.

**S3 upload_part returns nothing on success** — You must collect ETags from each part response and combine them with `CompleteMultipartUpload`. Missing an ETag causes data corruption.

**DynamoDB conditional expressions fail silently on wrong types** — Type mismatches between your data and table schema cause `ValidationException`, not type coercion. Explicitly cast values.

## Common Workflows

| Task | Code Pattern | Details |
|------|-------------|---------|
| Configure client | `boto3.client("s3", region_name="us-east-1")` | [configuration.md](references/configuration.md) |
| Read credentials | Environment, ~/.aws/credentials, IAM roles | [credentials.md](references/credentials.md) |
| Upload file | `s3.upload_file(filename, bucket, key)` | [s3.md](references/s3.md) |
| Query table | `dynamodb.query(KeyConditionExpression=...)` | [dynamodb.md](references/dynamodb.md) |
| Handle errors | Check `err.response["Error"]["Code"]` | [error-handling.md](references/error-handling.md) |
| Pagination | `client.get_paginator("list_buckets")` | Iterate pages automatically |
| Wait for state | `ec2.waiter.instance_running.wait(InstanceIds=[...])` | [waiters.md](references/waiters.md) |

## Best Practices

1. **Use resource interface for high-level ops** — `s3.Bucket("mybucket").objects.all()` is cleaner than command objects
2. **Use client interface for fine control** — `s3.put_object(Body=data)` gives you all parameters
3. **Configure retry strategy** — Default retries may be insufficient for production: `config=Config(retries={"max_attempts": 5})`
4. **Use waiters for synchronization** — Don't poll manually; use built-in waiters (`instance_running`, `bucket_exists`)
5. **Paginate large results** — Never call list/scan methods expecting all results at once; always use `get_paginator()`

## References

- [Configuration](references/configuration.md)
- [Credentials](references/credentials.md)
- [DynamoDB](references/dynamodb.md)
- [Error Handling](references/error-handling.md)
- [Pagination](references/pagination.md)
- [S3](references/s3.md)
- [Waiters](references/waiters.md)

**Author:** Amazon Web Services (AWS)
