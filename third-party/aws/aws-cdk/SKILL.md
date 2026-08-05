---
name: aws-cdk
description: >-
  Authors, deploys, and troubleshoots AWS infrastructure using CDK with TypeScript
  or Python. Covers best practices, stack architecture, construct patterns, bootstrapping,
  drift detection, resource import, safe refactoring, and CLI error resolution. Use when
  writing CDK constructs, deploying stacks, fixing CloudFormation errors, or planning stacks.
version: 1
---

# AWS CDK

Domain expertise for CDK construct authoring, deployment workflows, compliance, drift, importing resources, safe refactoring, and troubleshooting CDK CLI / CloudFormation errors.

## When NOT to Use

Raw CloudFormation YAML/JSON. SAM. Terraform/Pulumi. CI/CD beyond CDK Pipelines. Use builtin knowledge or specialized skills for these.

## Critical Warnings

**Deadly embrace**: Removing a cross-stack reference deadlocks deployment (`Export ... cannot be deleted as it is in use by ...`). Preferred fix: weaken the reference first — `CrossStackReferences.of($RESOURCE).produce(ReferenceStrength.BOTH)` then `WEAK`, then remove (three deploys). Legacy fallback: two-deploy `this.exportValue()` recipe.

**Construct ID changes cause replacement**: Renaming/moving a construct changes its logical ID → CloudFormation replaces the resource (data loss for stateful resources). Always `cdk diff` before deploy.

**UPDATE_ROLLBACK_FAILED**: Stack is stuck. Fix with `cdk rollback $STACK` or `cdk rollback $STACK --orphan <LogicalId>`.

**Non-empty S3 buckets persist after destroy**: You MUST set both `removalPolicy: DESTROY` and `autoDeleteObjects: true`. Versioned buckets are worse — delete markers persist even after apparent deletion.

## Common Workflows

| Task | Quick Command | Details |
|------|--------------|---------|
| Bootstrap | `cdk bootstrap aws://$ACCOUNT/$REGION` | Required once per account/region |
| New TS project | `cdk init app --language typescript` | Use `tsx`, `eslint-plugin-awscdk` |
| New Python project | `cdk init app --language python` | Pin deps, use virtualenv |
| Deploy | `cdk synth --strict` → `cdk diff` → `cdk deploy` | Always diff before deploy to prod |
| cdk-nag | `Aspects.of(app).add(new AwsSolutionsChecks())` | Compliance checks |
| Drift | `cdk drift $STACK` (use `--fail` in CI) | Detect manual changes |
| Import resource | `cdk import` (interactive or `--resource-mapping`) | [import-and-migrate](references/import-and-migrate.md) |
| Refactor safely | `cdk refactor --unstable=refactor` | No property changes in same deploy |

## Troubleshooting

| Error | Cause → Fix |
|-------|------------|
| **DeployFailed / DeploymentError** | CDK error isn't root cause. `cdk deploy $STACK --verbose`, then diagnose. First `_FAILED` event is the cause. |
| **NoCredentials / ExpiredToken** | `aws sts get-caller-identity` + `cdk doctor`. Expired SSO, missing `env`, missing `sts:AssumeRole`. |
| **Asset errors** | Path wrong, Docker not running, or bootstrap bucket perms. |
| **AppRequired** | Add `"app": "npx tsx bin/my-app.ts"` to `cdk.json`. |
| **BootstrapVersionValidation** | Re-bootstrap. Match `--qualifier` everywhere. |
| **DependencyCycle** | Extract shared resource into third stack or use SSM for late-binding. |
| **UnresolvedAccount** | Set explicit `env: { account, region }` on stack. Commit `cdk.context.json`. |
| **NoStacksMatched** | CDK uses logical ID (2nd constructor arg), not CFN name. `cdk list` to find IDs. |
| **Cannot find module** | Run `npx tsc --noEmit`, check `cdk.json` app path matches `tsconfig.json`. |

## References

- [Bootstrap & Project Setup](references/bootstrap-and-project-setup.md)
- [Construct Patterns](references/construct-patterns.md)
- [Compliance & Drift](references/compliance-and-drift.md)
- [Import & Migrate](references/import-and-migrate.md)
- [Refactor & Prevent Replacement](references/refactor-and-prevent-replacement.md)
- [Troubleshooting Credentials](references/troubleshooting-credentials.md)
- [Troubleshooting Deployment](references/troubleshooting-deployment.md)
- [Troubleshooting Synth](references/troubleshooting-synth.md)
- [V1 to V2 Migration](references/v1-to-v2-migration.md)

**Author:** Amazon Web Services (AWS)
