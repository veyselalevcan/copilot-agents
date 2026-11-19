# Copilot agents for security work

Defensive Microsoft 365 Copilot agents built by Veysel Alevcan with Copilot Agent Builder. Each folder under `agents/` holds the full source of one agent: description, instructions, conversation starters, knowledge websites and skills. You can rebuild any agent in your own Microsoft 365 tenant with [INSTALL.md](INSTALL.md).

| Agent | Folder | Purpose |
|---|---|---|
| OT Incident Triage Advisor | [ot-incident-triage](agents/ot-incident-triage) | Safety-first triage of suspected OT and ICS security incidents, with ATT&CK for ICS, severity scoring, IEC 62443 and NIS2 checks |
| Azure & Entra Security Advisor | [azure-entra-security](agents/azure-entra-security) | Defensive review of Entra ID and Azure identity, access and Conditional Access |
| AWS IAM & Security Advisor | [aws-iam-security](agents/aws-iam-security) | Defensive least-privilege review of AWS IAM policies and security findings |
| Google Cloud IAM Advisor | [google-cloud-iam](agents/google-cloud-iam) | Defensive review of Google Cloud IAM bindings, service accounts and policies |
| GenAI Cloud Security Advisor | [genai-cloud-security](agents/genai-cloud-security) | Threat modelling and guardrail review for cloud generative AI apps and agents |
| Agent Governance Advisor | [agent-governance](agents/agent-governance) | Inventory, ownership, risk tiers and reviews for AI agents across platforms |
| A2A Security Advisor | [a2a-security](agents/a2a-security) | Defensive threat review of agent-to-agent, MCP and multi-agent links |
| Security Agent Orchestrator | [security-agent-orchestrator](agents/security-agent-orchestrator) | Plans security requests and routes them to the right specialist agent with a ready handoff prompt |

The orchestrator cannot call the other agents itself (an Agent Builder limit). It writes the handoff prompt; you paste it into the specialist agent.

## Scope

- Defensive and authorized use only. The agents refuse attack steps, evasion and safety-system bypass.
- Output is advice. A qualified person reviews it before acting.
- In OT settings, process safety and operator procedures come first.

## Other agents by the author

Copilot Security Advisor, Phishing Triage Analyst and Cyber Awareness Quiz Tutor are also covered by the privacy statement and terms below. Their source is not in this repository yet.

## Legal

- [Privacy statement](PRIVACY.md)
- [Terms of use](TERMS.md)

Questions or problems: open an issue in this repository.
