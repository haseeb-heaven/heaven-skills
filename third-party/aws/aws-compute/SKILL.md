---
name: aws-compute
description: >-
  Provisions, scales, and manages AWS compute resources including EC2, Auto Scaling,
  AMIs, instance selection, Systems Manager, and provisioning workflows. Use when
  working with EC2 instances, auto-scaling policies, image management, capacity planning,
  or SSM automation. Covers both traditional VMs and modern managed compute services.
version: 1
---

# AWS Compute

Domain expertise for EC2 instance lifecycle management, auto-scaling configuration, AMI operations, instance right-sizing, Systems Manager automation, capacity planning, and compute troubleshooting.

## When NOT to Use

- Container orchestration (use `aws-containers` for ECS/EKS)
- Serverless functions (use `aws-serverless` for Lambda)
- High-performance computing (use AWS Batch or parallel cluster services)

## Critical Warnings

**Instance types change availability** — On-demand capacity can disappear regionally without warning. Always have fallback instance families and check `ec2:DescribeSpotPlacementScores` before committing.

**AMI rotation breaks launches** — Custom AMIs are account/region specific. Migrations require re-AMIfication. Use Parameter Store for current AMI IDs to avoid hardcoded references.

**Security group defaults are wrong** — Default SG allows all outbound; ingress depends on launch config. Explicitly define ingress rules — never use `0.0.0.0/0` in production without WAF.

## Common Workflows

| Task | Command/API | Details |
|------|-------------|---------|
| Launch instance | `ec2:RunInstances` | Specify AMI, type, SG, IAM role |
| Create AMI | `ec2:CreateImage` | Instance state: stopped recommended |
| Auto Scale | `autoscaling:createAutoScalingGroup` | Min/max/desired + scale policies |
| Right-size | CloudWatch CPU/Mem < 40% avg | [instance-selection.md](references/instance-selection.md) |
| SSM RunCommand | `ssm:SendCommand` | Execute remotely without SSH keys |
| Patch baseline | `ssm:CreatePatchBaseline` | Automated OS patching schedule |

## Troubleshooting Quick Reference

| Issue | Check |
|-------|-------|
| Instance won't start | EBS volume health, SG inbound rules, IAM instance profile |
| High CPU throttling | Check detailed monitoring; consider HPC/Compute Optimized families |
| Disk full after upgrade | `/var/log` growth, journal rotation, logrotate config |
| Connection refused | Security group, NACL, service status (`systemctl`) |
| Slow performance | EBS IO balance, network metrics, CPU credit balance (T-series) |

## References

- [AMI Management](references/ami-management.md)
- [Auto Scaling](references/auto-scaling.md)
- [Instance Selection](references/instance-selection.md)
- [Provisioning](references/provisioning.md)
- [Systems Manager](references/systems-manager.md)
- [Troubleshooting](references/troubleshooting.md)

**Author:** Amazon Web Services (AWS)
