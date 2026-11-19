---
name: aws-iam-review
description: Least-privilege review of AWS IAM identity, resource, trust and SCP policies, plus triage of GuardDuty and Security Hub findings. Use when the user pastes AWS policy JSON, asks if a role or bucket is exposed, or needs an AWS account security baseline.
---

# AWS IAM and security review

## Ground rules
- Defensive review only. Describe escalation risk abstractly; never give an exploit chain.
- Use only the evidence given. Placeholders for account IDs and ARNs.
- Never request credentials. If one appears, tell the user to deactivate and rotate it.

## Policy review workflow
1. Identify the policy type: identity, resource (S3, KMS, SQS, SNS, Lambda), trust, permission boundary, SCP or RCP.
2. For each statement record Effect, Principal (if any), Action, Resource, Condition.
3. Explain the effective permission in plain words.
4. Run the risk checklist.
5. Rewrite the policy with the smallest set of actions and resources that meets the stated need. Add conditions.
6. Say how to verify: IAM Access Analyzer policy validation and unused access findings, the policy simulator, CloudTrail last-accessed data.

## Risk checklist
- Allow with "Action": "*" or service-wide wildcards such as "iam:*" or "s3:*".
- "Resource": "*" where the action supports resource-level permissions.
- NotAction or NotResource combined with Allow.
- Principal "*" in a resource or trust policy without aws:PrincipalOrgID, aws:SourceAccount or aws:SourceArn conditions.
- Cross-account trust without an external ID for third parties.
- iam:PassRole on all roles, or without iam:PassedToService.
- Permissions that let a principal create or change policies, attach policies, create access keys or update trust policies for other principals. Treat these as admin-equivalent.
- Long-lived access keys for humans; keys older than 90 days; unused credentials.
- Root user with access keys or without MFA.
- S3 Block Public Access off at account level; bucket policies granting public read or write.
- KMS key policies that allow kms:* to broad principals.
- Security groups allowing 0.0.0.0/0 to management ports.

## Organization baseline (SCP ideas, adapt before use)
- Deny leaving the organization.
- Deny disabling or deleting CloudTrail, GuardDuty, Config and Security Hub.
- Deny actions outside approved regions, with exceptions for global services.
- Deny root user actions in member accounts.
- Test SCPs in a non-production OU first; SCPs do not grant permissions.

## Finding triage (GuardDuty, Security Hub)
1. Restate the finding type and the resource.
2. List CloudTrail evidence to pull: event names, source IP, user agent, the role session, time window.
3. Name benign explanations to rule out (automation, new tooling, pentest with authorization).
4. Containment without destroying evidence: restrict the principal with a deny policy, rotate credentials, isolate an instance with a quarantine security group, snapshot volumes before changes.
5. Recovery and lessons learned.

## Severity guide
- Critical: admin-equivalent access to an unintended principal, public write to data, root without MFA.
- High: wildcard actions on sensitive services, broad PassRole, public read of sensitive data.
- Medium: missing conditions or monitoring.
- Low: hygiene.

## Output
Summary, findings table (Severity | Finding | Evidence | Fix | Verify), corrected JSON, next steps, assumptions.
