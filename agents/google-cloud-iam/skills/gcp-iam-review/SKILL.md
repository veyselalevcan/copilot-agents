---
name: gcp-iam-review
description: Least-privilege review of Google Cloud IAM bindings, service accounts and organization policies, plus triage of Security Command Center findings. Use when the user pastes gcloud IAM policy output, asks about service account risk, or needs a GCP organization baseline.
---

# Google Cloud IAM review

## Ground rules
- Defensive review only. Describe impersonation and escalation risk abstractly.
- Use only the evidence given. Placeholders for project IDs and emails.
- Never request key files. If one appears, tell the user to delete and rotate it.

## Binding review workflow
1. Note the scope: organization, folder, project or resource. Remember inheritance downward.
2. For each binding record role, members and condition.
3. Run the risk checklist.
4. Propose the narrower role and scope. Use IAM Conditions for time or resource limits where they fit.
5. Verify with Policy Analyzer (who can access what), the IAM recommender (unused permissions) and Cloud Audit Logs (Admin Activity is always on; Data Access often needs enabling).

## Risk checklist
- Owner or Editor granted to people or service accounts in production.
- allUsers or allAuthenticatedUsers on buckets, functions, services or datasets.
- Members outside the organization's domains, or personal accounts.
- User-managed service account keys, especially old or unused ones.
- Broad grants of Service Account User or Service Account Token Creator at project level: they let the member act as every service account in the project.
- Default compute or App Engine service accounts used by workloads with broad roles.
- Custom roles that include setIamPolicy, or roles that allow creating keys or changing org policies.
- Project-level grants where a resource-level grant would do.
- No deny policies or org policies for sensitive guardrails.

## Organization Policy baseline (confirm impact first)
- Disable service account key creation and upload.
- Restrict domain sharing to the organization's customer IDs.
- Prevent automatic IAM grants to default service accounts.
- Enforce uniform bucket-level access and public access prevention on Cloud Storage.
- Restrict resource locations if data residency matters.
- Require OS Login and restrict external IPs on VMs where workloads allow.
Use dry-run where available and roll out per folder.

## Workload identity
- Prefer attached service accounts on Google Cloud and Workload Identity Federation for external workloads (other clouds, CI/CD) over keys.
- Restrict federation with attribute conditions (for example a specific repository or branch).

## Finding triage (Security Command Center)
1. Restate category, resource and severity.
2. Evidence from Cloud Audit Logs: principal, method name, caller IP, time window.
3. Benign causes to rule out.
4. Safe containment: remove the binding or disable the key, keep logs, snapshot disks before changes.

## Severity guide
- Critical: public access to sensitive data, owner-level access for an unintended principal, leaked key with broad role.
- High: basic roles in production, project-wide impersonation rights, external members.
- Medium: missing guardrail or logging.
- Low: hygiene.

## Output
Summary, findings table (Severity | Finding | Evidence | Fix | Verify), corrected binding or gcloud command, next steps, assumptions.
