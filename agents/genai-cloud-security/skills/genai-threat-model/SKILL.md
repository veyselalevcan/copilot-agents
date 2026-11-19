---
name: genai-threat-model
description: Threat modelling and control review for LLM applications, RAG and agents on Amazon Bedrock, Azure AI Foundry or Azure OpenAI, and Google Vertex AI, mapped to the OWASP Top 10 for LLM Applications 2025. Use when the user describes a GenAI architecture or pastes guardrail, content filter or model access settings.
---

# GenAI platform threat model

## Ground rules
- Defensive only. No jailbreak prompts, injection payloads or bypass steps.
- Use only the evidence given; list assumptions.
- Never request keys. If one appears, tell the user to rotate it.

## Workflow
1. Draw the data flow in text: user, application, model endpoint, retrieval store, tools, downstream systems, logs.
2. Mark trust boundaries: user input, retrieved content, tool output, model output used by code or people.
3. For each boundary run the checklist and map to OWASP LLM IDs.
4. Record existing controls and gaps.
5. Prioritise fixes: platform guardrail, identity and network, application logic, monitoring, process.
6. Propose defensive verification in a non-production environment.

## Checklist by OWASP LLM 2025 category
- LLM01 Prompt Injection: direct and indirect (through documents, web pages, emails, tool output). Controls: platform prompt-attack filters (Bedrock Guardrails prompt attack filter, Azure Prompt Shields, Vertex Model Armor where available), separating instructions from data, least-privilege tools, human approval for high-impact actions.
- LLM02 Sensitive Information Disclosure: PII or secrets in prompts, retrieval or output. Controls: sensitive information filters, document-level access control in retrieval, data classification, no secrets in system prompts.
- LLM03 Supply Chain: third-party models, plugins, datasets. Controls: approved model list, provenance, version pinning.
- LLM04 Data and Model Poisoning: untrusted training or retrieval content. Controls: content review, source allow-lists, integrity checks.
- LLM05 Improper Output Handling: model output passed to browsers, shells, SQL or APIs. Controls: treat output as untrusted input, encoding, validation, parameterised calls.
- LLM06 Excessive Agency: tools with broad permissions or autonomy. Controls: narrow IAM roles per tool, read-only by default, approval steps, rate limits.
- LLM07 System Prompt Leakage: secrets or security logic in prompts. Controls: keep secrets and authorization outside the prompt.
- LLM08 Vector and Embedding Weaknesses: cross-tenant retrieval, unauthorised documents, embedding store exposure. Controls: per-user filtering, tenant isolation, access control on the store.
- LLM09 Misinformation: ungrounded answers. Controls: grounding checks (for example Bedrock contextual grounding, Azure groundedness detection), citations, human review for high-stakes use.
- LLM10 Unbounded Consumption: cost and denial of service. Controls: quotas, token limits, rate limiting, budget alerts.

## Platform control checklist
Amazon Bedrock
- Model access granted only to required models; IAM restricts bedrock:InvokeModel to specific model ARNs.
- Guardrails attached to applications and agents; configuration reviewed.
- Model invocation logging enabled with protected storage and retention policy.
- VPC interface endpoints (PrivateLink) for private access where needed.
- Agents: action group Lambda functions with least-privilege roles.

Azure AI Foundry / Azure OpenAI
- Entra ID authentication with managed identities; local key authentication disabled where possible.
- Content filters and Prompt Shields configured per deployment.
- Private endpoints and restricted public network access.
- Diagnostic logging enabled.

Google Vertex AI
- IAM roles scoped to the needed resources; service accounts per workload.
- Safety settings and Model Armor reviewed where available.
- VPC Service Controls perimeter around AI and data projects.
- CMEK where policy requires it; audit logs enabled.

## Severity guide
- Critical: agent can take high-impact actions from untrusted content without approval; sensitive data exposed to unauthorised users.
- High: no guardrails on a public app, broad model or data access, no logging.
- Medium: partial controls, missing monitoring.
- Low: documentation and hygiene.

## Output
Summary, threat model table (Boundary | Threat | OWASP ID | Current control | Gap | Fix), findings, next steps, assumptions.
