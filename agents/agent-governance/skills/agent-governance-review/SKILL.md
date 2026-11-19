---
name: agent-governance-review
description: Inventory, risk-tier and review AI agents and agent-to-agent chains, and draft governance artefacts (policy, RACI, intake form, review checklist, KPIs). Use when the user lists agents, asks who owns or approves agents, or needs an agent governance process.
---

# Agent governance review

## Ground rules
- Work only from the information the user gives. Mark gaps as unknown.
- Platform settings change; point to vendor documentation when unsure.
- Regulatory notes are general information, not legal advice.

## Inventory fields
Agent | Owner (person) | Business purpose | Platform | Data sources | Tools and actions | Called agents | Identity used | Users or audience | Publication scope (personal, shared, catalog) | Risk tier | Last review | Next review

## Risk tiers
- Low: read-only, public or non-sensitive data, no actions.
- Medium: internal data, no actions on behalf of users.
- High: sensitive or personal data, or actions on behalf of users (email, files, tickets).
- Critical: actions with financial, safety, legal or tenant-wide impact; autonomous chains of agents; external parties.

## Controls per tier
| Control | Low | Medium | High | Critical |
|---|---|---|---|---|
| Named owner | Yes | Yes | Yes | Yes plus deputy |
| Design review | No | Light | Security and privacy | Security, privacy, legal |
| Test evidence before publishing | Basic | Test prompts | Test set plus misuse tests | Red-team in non-production |
| Human approval for actions | n/a | n/a | For high-impact actions | For all external or irreversible actions |
| Logging and audit | Platform default | Enabled | Enabled and reviewed | Enabled, alerting |
| Review frequency | Yearly | Six-monthly | Quarterly | Quarterly plus after each change |

## Agent-to-agent checks
- Every call from one agent to another is documented with purpose and data passed.
- Each agent in a chain has its own identity and least-privilege permissions; no shared credentials.
- The caller cannot gain permissions it does not have by asking another agent (no permission laundering).
- One human is accountable for the whole chain, and each agent has an owner.
- Chains can be stopped quickly (a kill switch or disable procedure is known).
- Logs allow tracing a user request across all agents.

## Lifecycle
Request, intake form, risk tier, design review, build, test, approval, publish, monitor, periodic review, change review, retirement (disable, remove sharing, archive configuration, revoke identities).

## Artefacts on request
- Policy: purpose, scope, roles, tiers, controls, exceptions, review.
- RACI: requester, owner, security, privacy, IT admin, approver.
- Intake form questions: purpose, data, actions, audience, called agents, identity, expected volume.
- KPIs: number of agents by tier, agents without owner, overdue reviews, agents with actions, incidents, retired agents.

## Output
Summary, inventory table, risk table with reasons, actions with owner and due date placeholders, assumptions.
