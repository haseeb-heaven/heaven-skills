---
name: aws-billing-and-cost-management
description: >-
  Analyze AWS costs, identify savings opportunities, and optimize spending.
  Covers Cost Explorer, budgets, savings plans, reserved instances, RI optimization,
  EBS/EC2/RDS rightsizing, Lambda optimization, and cost allocation tags. Use when
  investigating high bills or optimizing AWS infrastructure costs.
version: 1
---

# AWS Billing & Cost Management

Domain expertise for analyzing AWS costs, finding optimization opportunities, and implementing cost-saving strategies.

## When to Use

- Investigating unexpected AWS bill spikes
- Regular cost optimization audits
- Setting up budgets and alerts
- Evaluating Savings Plans vs Reserved Instances
- Rightsizing EC2, RDS, EBS, Lambda resources

## Critical Warnings

**Cost Explorer has 2-day lag** — Recent charges may not appear in Cost Explorer immediately. Always check the billing dashboard for real-time spend estimates.

**Savings Plans are commitments** — Once purchased, they're non-refundable and lock you into committed usage. Never commit before validating patterns over 30+ days.

**Data transfer is invisible** — Egress costs between services/regions often go unnoticed. They can exceed compute costs in data-heavy workloads.

## Common Workflows

| Task | Command/API | Details |
|------|-------------|---------|
| Analyze spend | `ce:GetCostAndUsage` | [cost-explorer.md](references/cost-explorer.md) |
| Set budgets | `budgets:CreateBudget` | [budgets.md](references/budgets.md) |
| Evaluate SPs | Compare on/off-peak usage | [savings-plans.md](references/savings-plans.md) |
| RI optimization | `ec2:DescribeReservedInstances` | [reserved-instances.md](references/reserved-instances.md) |
| Rightsize EC2 | `compute-optimization/ec2` | [ec2-rightsizing.md](references/ec2-rightsizing.md) |
| Optimize RDS | `rds:describe-orderable-db-instances` | [rds-optimization.md](references/rds-optimization.md) |
| Optimize Lambda | Check duration/memory | [lambda-optimization.md](references/lambda-optimization.md) |
| Audit costs | CUR + Athena queries | [cur-athena.md](references/cur-athena.md) |

## Quick Optimization Checklist

1. **Unattached EBS volumes** — Delete or snapshot, then delete
2. **Idle load balancers** — Remove if no targets for 7+ days
3. **Over-provisioned instances** — Check CloudWatch CPU/mem < 40% average
4. **Old snapshots** — Automate lifecycle policies
5. **No cost allocation tags** — Tag everything for visibility
6. **Free tier ineligible** — Verify eligibility on new accounts

## References

- [Cost Explorer](references/cost-explorer.md)
- [Budgets](references/budgets.md)
- [Savings Plans](references/savings-plans.md)
- [Reserved Instances](references/reserved-instances.md)
- [EC2 Rightsizing](references/ec2-rightsizing.md)
- [RDS Optimization](references/rds-optimization.md)
- [Lambda Optimization](references/lambda-optimization.md)
- [EBS Optimization](references/ebs-optimization.md)
- [CUR + Athena](references/cur-athena.md)

**Author:** Amazon Web Services (AWS)
