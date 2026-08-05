---
name: aws-deployment
description: >-
  Configures CI/CD pipelines on AWS using CodePipeline, CodeBuild, CodeDeploy,
  CodeArtifact, and CodeConnections. Covers pipeline authoring, deployment strategies
  (blue/green, canary, rolling), artifact management, and troubleshooting pipeline failures.
  Use when setting up or debugging AWS-based CI/CD infrastructure.
version: 1
---

# AWS Deployment

Domain expertise for building CI/CD pipelines and deployment automation using AWS developer tools services.

## When NOT to Use

- GitHub Actions, GitLab CI, CircleCI, Jenkins — use native patterns for those platforms
- Air-gapped/on-prem deployments without AWS targeting
- Simple file sync/deploy (use S3 deploy or CodeDeploy agent instead)

## Critical Warnings

**CodePipeline actions are stateful** — Removing a stage from an active pipeline doesn't automatically remove associated resources (build projects, deploy actions). Clean up manually via console or CLI.

**CodeDeploy blue/green requires careful routing** — The traffic shifting script (`AppSpec.hooks.BeforeTraffic`) must succeed within timeout or the entire deployment rolls back. Test with manual step first.

**Cross-account artifacts need explicit cross-region replication** — S3 buckets used for pipeline artifacts don't replicate across regions by default. Set up `replicationConfiguration` before deploying cross-region.

## Common Workflows

| Task | Command/API | Details |
|------|-------------|---------|
| Create pipeline | `codepipeline:create-pipeline` | Define stages, actions, role |
| Build project | `codebuild:create-project` | Specify source + build spec |
| Deploy app | `codedeploy:create-application` | App Spec YAML defines lifecycle hooks |
| Artifact registry | `codeartifact:create-domain/repository` | Private npm/maven/pip packages |
| Connect repos | `codeconnections:create-connection` | GitHub/GitLab integration |
| Troubleshoot | `codepipeline:get-pipeline-state` | Find failing stage/action |

## Deployment Strategies

| Strategy | Best For | Duration | Rollback |
|----------|----------|----------|----------|
| **All at once** | Dev/staging only | Minutes | Full revert |
| **Rolling** | EC2/ECS services | Tens of min | Per-instance |
| **Blue/Green** | Zero-downtime prod | Varies | Swap container |
| **Canary** | Low-risk gradual rollout | Hours | Traffic shift back |

## References

- [CodePipeline](references/codepipeline.md)
- [CodeBuild](references/codebuild.md)
- [CodeDeploy](references/codedeploy.md)
- [CodeArtifact](references/codeartifact.md)
- [CodeConnections](references/codeconnections.md)
- [Troubleshooting](references/troubleshooting.md)

**Author:** Amazon Web Services (AWS)
