---
name: aws-cloudformation
description: >-
  Authors, validates, and troubleshoots AWS CloudFormation templates (YAML/JSON).
  Covers best practices for template authoring, pre-deploy validation, compliance checks,
  express mode deployments, resource property lookups, drift detection, and common deployment
  error resolution. Use when writing CloudFormation stacks, debugging deployment failures,
  or validating infrastructure-as-code templates.
version: 1
---

# AWS CloudFormation

Domain expertise for authoring, validating, deploying, and troubleshooting CloudFormation templates.

## When NOT to Use

- IaC using CDK, Terraform, Pulumi. These have their own specialized patterns.

## Critical Warnings

**No rollback on partial failure** — CloudFormation rolls back automatically by default, but `DisableRollback` parameter will leave resources in a broken state. Always verify before disabling.

**Nested stack circular dependencies** — Stacks cannot form dependency cycles. If Stack A references an output from Stack B and vice versa, use SSM parameters or Lambda triggers to break the cycle.

**Drift doesn't auto-detect manual changes** — Resources modified outside CFN won't cause failures unless you explicitly run `detect-stack-drift`. Manual changes may silently diverge from your template.

## Common Workflows

| Task | Command/API | Details |
|------|-------------|---------|
| Validate template | `cfndiff validate-template` | Syntax & logical checks |
| Pre-deploy check | `cfndiff pre-deploy-validation.script.md` | Dry-run simulation |
| Deploy (Express) | `cdk deploy --express-mode` | Faster single-resource deploys |
| Lookup properties | `cfndiff lookup-resource-properties.script.md` | Read existing resource attributes |
| Check compliance | `cfndiff check-compliance.script.md` | Validate against best practices |
| Validate script | `cfndiff validate-cloudformation-template.script.md` | Run template through linting |
| Deploy script | `cfndiff deploy-with-express-mode.script.md` | Automated safe deployment |
| Troubleshoot | `cfndiff troubleshoot-deployment.script.md` | Diagnose failed deployments |

## Template Best Practices

1. **Use intrinsic functions sparingly** — Prefer conditions over complex Fn::If nesting
2. **Tag everything** — `AWS::CloudFormation::Stack` tags propagate to all child resources
3. **RemoveOnDeletion policies** — Set `DeletionPolicy: Retain` for stateful resources (RDS, S3) to prevent accidental data loss
4. **Parameter constraints** — Always add `AllowedPattern`, `MinLength`, `MaxLength` to string params
5. **ChangeSets** — Preview changes with `create-change-set` before deploying to production

## References

- [Author Best Practices](references/author-cloudformation-best-practices.script.md)
- [Pre-Deploy Validation](references/cloudformation-pre-deploy-validation.script.md)
- [Deploy with Express Mode](references/deploy-with-express-mode.script.md)
- [Lookup Resource Properties](references/lookup-resource-properties.script.md)
- [Troubleshoot Deployment](references/troubleshoot-deployment.script.md)
- [Validate Template](references/validate-cloudformation-template.script.md)

**Author:** Amazon Web Services (AWS)
