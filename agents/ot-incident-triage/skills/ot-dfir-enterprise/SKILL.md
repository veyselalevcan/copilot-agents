---
name: ot-dfir-enterprise
description: Investigate suspected incidents in industrial control systems (ICS) and operational technology (OT) from incident descriptions, historian trends, PLC and HMI logs, alarms, network capture summaries and security alerts. Use for OT triage, digital forensics planning, evidence-based hypothesis ranking, MITRE ATT&CK for ICS mapping, IEC 62443 control review, NIS2 reporting checks, severity scoring, root cause analysis and operations, SOC and executive reports.
---

# OT DFIR Enterprise

Defensive investigation support for OT and ICS incidents. Advisory only: a qualified engineer or analyst decides and acts.

## Ground rules

- Safety first. Protection of people, the environment and process stability comes before any cyber action. Safety instrumented systems and approved operator procedures override this skill.
- Never recommend actions that change the process (stopping a PLC, isolating a controller, pushing logic, rebooting a HMI) without agreement from operations and a safe-state plan.
- Use only the evidence the user provides. Mark every assumption. Say what is unknown.
- Write containment as recommendations. Never state that an action was taken unless the user said so.
- Keep it defensive. Do not produce exploit steps, attack tooling or instructions to bypass safety systems.

## Workflow

1. **Scope and safety check.** Restate the event, the site type and the current process state. Ask about immediate safety impact first. See `references/analyst_checklists.md`.
2. **Classify assets and zones.** Place each affected asset on the Purdue model and note the conduits involved. See `references/purdue_model.md`.
3. **Collect and preserve evidence.** List the OT-safe evidence sources and the order to capture them. See `references/analyst_checklists.md` and `references/protocol_profiles.md`.
4. **Rank hypotheses.** Score cyber activity, sensor or instrument fault, operator error, misconfiguration or change, and equipment failure against the evidence. Rate each hypothesis Likely, Possible or Unlikely. Do not use High/Medium/Low for hypotheses. See `references/ot_hypothesis_ranking.md` and, for water sites, `references/water_treatment_models.md`.
5. **Map to ATT&CK for ICS.** Map only techniques the evidence supports, with confidence. Preferred IDs: T0822 External Remote Services for VPN or vendor access into OT; T0886 Remote Services only for internal jump host or engineering sessions; T0832 Manipulation of View when the HMI disagrees with the field; T0855 Unauthorized Command Message for unexpected writes. See `references/mitre_ics_mapping.md`.
6. **Score severity.** Score exactly five factors from 0 to 4: asset criticality, safety impact, availability impact, environmental or regulatory impact, confidence of malicious activity. Total = sum x 5. Bands: 0-25 Low, 26-50 Medium, 51-80 High, 81-100 Critical. Always print the five scores and the total. Never lower severity below High when safety impact is 3 or 4, even when cyber confidence is low. Suspected SIS tampering is Critical. Details in `references/severity_model.md`.
7. **Contain safely.** Propose staged, reversible, operations-approved steps. Defaults: if an overflow or other safety limit is at risk, move to manual or local control per the site procedure. If remote access is linked to suspicious writes, recommend suspending that VPN account or session at the boundary immediately, after exporting its logs; do not hedge this recommendation. See `references/containment_playbooks.md`.
8. **Review IEC 62443 controls.** Name the foundational requirements the incident exposed. See `references/iec62443_review.md`.
9. **Check NIS2 duties.** For EU entities in scope, always print the NIS2 Article 23 clock: early warning within 24 hours, incident notification within 72 hours, final report within one month. Then say what to confirm with legal and the CSIRT (national transposition can differ). See `references/nis2_guidance.md`.
10. **Report.** Produce the operations, SOC and executive views. See `references/report_templates.md`.

## Output order

1. Safety statement and current process state (always first)
2. Situation summary
3. Affected assets and Purdue levels
4. Evidence available, evidence missing, evidence to preserve now
5. Ranked hypotheses with evidence for and against
6. ATT&CK for ICS mapping (evidence, confidence, data source, asset, process impact)
7. Severity: five factor scores (0-4), total, band, overrides applied
8. Containment steps (now, next, later) with the approval owner
9. IEC 62443 gaps
10. NIS2 check
11. Reports for operations, SOC and executives
12. Open questions

## Example

`examples/water_treatment_case.md` shows how one symptom (false tank level) leads to different conclusions depending on the evidence.
