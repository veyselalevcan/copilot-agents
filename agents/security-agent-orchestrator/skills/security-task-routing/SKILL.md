---
name: security-task-routing
description: Split a security request into tasks, route each to the right specialist security agent with a handoff prompt, and merge returned answers into one plan. Use when the user brings a broad or mixed security request, asks which agent to use, or pastes answers from several agents.
---

# Security task routing

## Routing table
| Signal in the request | Agent |
|---|---|
| PLC, SCADA, HMI, historian, Modbus, DNP3, plant, process safety | OT Incident Triage Advisor |
| Suspicious email, link, attachment, sender | Phishing Triage Analyst |
| Microsoft 365 Copilot, Copilot prompt injection, Copilot data exposure | Copilot Security Advisor |
| Entra ID, Conditional Access, Azure subscription, Sentinel, KQL | Azure & Entra Security Advisor |
| AWS account, IAM policy, S3, GuardDuty, CloudTrail | AWS IAM & Security Advisor |
| GCP project, gcloud, service account, SCC | Google Cloud IAM Advisor |
| Bedrock, Azure OpenAI, AI Foundry, Vertex AI, RAG, LLM app | GenAI Cloud Security Advisor |
| Agents calling agents, MCP, A2A, tool permissions of agents | A2A Security Advisor |
| Agent inventory, owners, approval, lifecycle, policy | Agent Governance Advisor |
| Training, awareness, quiz | Cyber Awareness Quiz Tutor |

If two agents fit, pick the one closest to the asset at risk and mention the second as a follow-up.

## Ordering rule
1. Safety and containment (OT first when people or the process are at risk).
2. Investigation and evidence.
3. Hardening and fixes.
4. Governance, reporting and awareness.

## Handoff prompt template
"Context: <two or three facts>. Task: <one task>. Constraints: <time, platform, licence, what must not change>. Output: <format, for example findings table with severity, fix, verify>." No secrets, no personal data beyond what is needed.

## Merge rules
- Keep each specialist's findings with its source agent named.
- Resolve conflicts by stating both views and the deciding fact or check.
- Produce one prioritised action list with owner and due date placeholders.
- List what is still unknown.

## Limits
Agent Builder agents cannot call each other. The user runs each handoff. For automatic orchestration suggest Copilot Studio or another framework and a threat review by the A2A Security Advisor.
