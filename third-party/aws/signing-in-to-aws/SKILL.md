---
name: signing-in-to-aws
description: >-
  Gets AWS credentials for CLI access across different authentication methods.
  Covers SSO login, IAM user credentials, assumed roles, temporary tokens,
  multi-factor authentication, and credential file management. Use when needing
  to authenticate to AWS services from the command line or scripts.
version: 1
---

# Signing Into AWS

Domain expertise for obtaining and managing AWS credentials across all authentication methods.

## When NOT to Use

- Non-CLI programs — use SDK default credential chain
- Service accounts running on EC2/Lambda/ECS — use instance roles or task roles
- Long-running background processes — use short-lived STS tokens instead of long-term keys

## Critical Warnings

**Never commit credentials** — Access keys in source control are immediately exploitable. Rotate via IAM console and delete old keys within minutes of detection.

**SSO sessions expire silently** — After SSO token expiry, `aws sts get-caller-identity` returns empty or error. Run `aws sso login --profile <name>` before each session that may have expired.

**Assumed roles lose scope** — `sts:assume-role` gives temporary credentials valid for up to 36 hours. Code using assumed role credentials will fail when they expire unless refreshed.

## Authentication Methods

| Method | Best For | Token Duration | Setup Complexity |
|--------|----------|---------------|-----------------|
| **IAM User Keys** | Scripts, CI/CD (legacy) | Permanent | Low |
| **SSO Login** | Daily developer work | 8 hours (renewable) | Medium |
| **STS AssumeRole** | Cross-account access | Up to 36 hours | High |
| **Instance Profile** | EC2, Lambda, ECS | Automatic refresh | Medium |
| **Web Identity** | Mobile/web apps | Short-lived | High |

## Common Workflows

| Task | Command | Details |
|------|---------|---------|
| SSO login | `aws sso login --profile myprofile` | Opens browser for auth |
| Verify identity | `aws sts get-caller-identity` | Confirm active credentials |
| Assume role | `aws sts assume-role --role-arn <arn> --session-name <name>` | Get temp creds |
| List profiles | `cat ~/.aws/credentials` | View configured accounts |
| Set env vars | `eval $(aws configure export-credentials --format env)` | Shell credential injection |
| MFA prompt | Include in profile config | Force MFA on role assumption |

## Credential File Structure (~/.aws/)

```
~/.aws/
├── credentials          # Saved access keys (encrypted recommended)
├── config               # Profiles, regions, output formats
└── sso/cache/           # SSO session tokens (auto-managed)
```

## Best Practices

1. **Use SSO over static keys** — Always prefer SSO for interactive use; it supports MFA natively
2. **One key pair per purpose** — Different IAM users for CI/CD vs development vs automation
3. **Enable MFA everywhere** — Virtual MFA device (Google Authenticator, Authy) on all root and IAM accounts
4. **Rotate keys regularly** — 90-day rotation policy for any static access key

**Author:** Amazon Web Services (AWS)
