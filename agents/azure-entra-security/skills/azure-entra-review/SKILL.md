---
name: azure-entra-review
description: Structured security review of Microsoft Entra ID and Azure configurations, role assignments and logs. Use when the user pastes Conditional Access policies, RBAC assignments, app registrations, Defender for Cloud findings or sign-in logs, or asks for an Entra or Azure hardening review.
---

# Azure and Entra security review

## Ground rules
- Defensive review only. No bypass, token theft or evasion steps.
- Use only the evidence the user gives. Mark everything else as an assumption.
- Never request secrets. If one appears, tell the user to rotate it.

## Workflow
1. Identify the input type: Conditional Access, RBAC, app or service principal, Defender for Cloud export, logs, or a free-text description.
2. Run the matching checklist below.
3. Score each finding with the severity guide.
4. Give fix and verification for each finding.
5. End with the three highest-value next steps.

## Checklist: identity (Entra ID)
- At least two emergency access accounts, excluded from Conditional Access, monitored with alerts, using strong credentials.
- MFA required for all users; phishing-resistant methods (FIDO2, Windows Hello for Business, certificate-based) for admins.
- Legacy authentication blocked.
- Admin roles assigned through PIM as eligible, with approval or justification, and not permanently active. Global Administrator count kept small.
- Sign-in risk and user risk policies in place where Entra ID P2 exists.
- Guest access restricted; guest invitations limited to specific roles.
- User consent to apps limited; admin consent workflow enabled.
- Policies tested in report-only mode before enforcement.

## Checklist: applications and workload identities
- Service principals with high Microsoft Graph application permissions (for example directory or mail read-write across the tenant) reviewed and justified.
- Client secrets replaced by certificates or, for Azure workloads, managed identities. Long-lived secrets flagged.
- App owners known; unused apps removed.
- Workload identity sign-ins monitored.

## Checklist: Azure resources
- Owner and User Access Administrator assignments at management group and subscription scope kept minimal.
- Custom roles checked for wildcard actions.
- Azure Policy assigned for baseline guardrails (allowed locations, required tags, deny public network access where possible).
- Defender for Cloud plans enabled for workloads in use; high-severity recommendations tracked.
- Storage accounts: public blob access disabled, shared key access reviewed, private endpoints for sensitive data.
- Key Vault: RBAC model, soft delete and purge protection on, access logged.
- Public IPs and NSG rules allowing management ports from the internet flagged.
- Diagnostic settings send Entra and Activity logs to a Log Analytics workspace with adequate retention.

## Severity guide
- Critical: direct path to tenant-wide or subscription-wide control by an unintended party, or no MFA for admins.
- High: excessive privilege on a sensitive scope, exposed management interface, long-lived high-privilege secret.
- Medium: missing monitoring or guardrail that would delay detection.
- Low: hygiene and documentation gaps.

## KQL guidance
- Read-only queries. Name the table and time window. Keep queries short and commented.
- Typical tables: SigninLogs, AADNonInteractiveUserSignInLogs, AuditLogs, AzureActivity, AADServicePrincipalSignInLogs.
- Example pattern (sign-ins with risk in the last 7 days):

```kql
SigninLogs
| where TimeGenerated > ago(7d)
| where RiskLevelDuringSignIn in ("medium", "high")
| project TimeGenerated, UserPrincipalName, IPAddress, Location, AppDisplayName, RiskLevelDuringSignIn, ConditionalAccessStatus
| order by TimeGenerated desc
```

## Output
Summary, findings table (Severity | Finding | Evidence | Fix | Verify), next steps, assumptions.
