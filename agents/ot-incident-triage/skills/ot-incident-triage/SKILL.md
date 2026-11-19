---
name: ot-incident-triage
description: Invoke when an engineer or security analyst needs a consistent, safety-aware triage report for an observed industrial control system or OT event.
compatibility: 'Requires data: none. Requires env: none. Authored-on: Bizchat'
---

## Purpose
Turn observations from industrial environments such as water treatment, chemical processing, manufacturing, and maritime systems into a structured, evidence-based triage report. Invoke for alarms, abnormal sensor or actuator values, PLC or HMI changes, unusual Modbus, DNP3, or S7 traffic, engineering workstation activity, or IT alerts near OT networks.

## Instructions
1. Review the user's observations and identify missing facts that materially affect safety, scope, timing, asset identity, process state, network location, or confidence. Ask concise clarifying questions before finalizing the report when those facts are missing. If urgent safety concerns are plausible, lead with the safety warning while asking questions.
2. Produce a report with exactly these numbered sections and headings:
1. **Situation Summary and Zone/Conduit** — Summarize observed facts without speculation. Identify the affected Purdue level from 0-5, the IT/OT DMZ, and relevant zone or conduit when evidence permits; otherwise state what must be confirmed.
2. **Safety First** — State whether physical safety or process impact is possible, likely, or not currently indicated. Always state that safety instrumented systems and approved operator procedures take priority over any cyber action.
3. **Ranked Hypotheses** — Rank cyber attack, sensor fault, operator error, and misconfiguration. For each, list evidence for, evidence against, confidence, and the missing evidence that would change the ranking.
4. **MITRE ATT&CK for ICS Mapping** — Map only evidence-supported tactics and technique IDs. Consider, when supported, `T0831 Manipulation of Control`, `T0836 Modify Parameter`, `T0855 Unauthorized Command Message`, `T0856 Spoof Reporting Message`, and `T0886 Remote Services`. Do not force a mapping; label uncertain mappings as provisional and explain the evidence gap.
5. **Severity** — Assign Low, Medium, High, or Critical with a short rationale tied to safety, process disruption, spread potential, asset criticality, and evidence strength.
6. **OT-Safe Containment and Evidence** — Recommend passive, reversible, operations-coordinated actions. Do not recommend active scanning of live controllers. Preserve PLC logic, controller configuration, alarm/event logs, engineering workstation artifacts, and historian data. Capture network traffic passively. Coordinate with operations before isolating, blocking, rebooting, changing logic, or interrupting a process.
7. **IEC 62443 Review** — Identify relevant IEC 62443 requirements, security levels, zones, conduits, access controls, change control, logging, or remote-access controls to review. Clearly distinguish a review recommendation from a compliance conclusion.
8. **NIS2 Reporting Check** — For potentially affected EU entities, assess whether the event may be significant enough to escalate for reporting review. State the expected timeline as early warning within 24 hours, incident notification within 72 hours, and final report within one month. Always state that the user must confirm applicability and deadlines with their legal or CSIRT contact.
3. Separate observed facts, user-reported assumptions, and analytical judgments. Use calibrated language and never present an unverified hypothesis as confirmed.
4. Prioritize preservation of life, environmental protection, and process stability. Recommend escalation to site operations, safety, incident response, legal, and the relevant CSIRT when warranted.
5. Refuse requests for step-by-step attack execution, exploitation, evasion, unauthorized command injection, or bypassing safety systems. Redirect to defensive validation, passive evidence collection, safe containment, and authorized lab testing.
6. Before completing the report, verify that all eight sections are present, every ATT&CK mapping has supporting evidence, the severity has a reason, and proposed actions are safe for live OT.

## Parameters
- Observed event, timestamps, affected process and assets
- Site or sector context
- Purdue level, zone, conduit, and IT/OT boundary information when known
- Alarm, sensor, actuator, PLC, HMI, historian, engineering workstation, network, and IT alert evidence
- Known operational or maintenance changes
- Safety, environmental, production, and regulatory impact indicators

## Output
A concise, structured triage report with the eight required sections, ranked hypotheses, evidence-based ATT&CK for ICS mappings, an OT-safe action list, and explicit uncertainty or clarification needs.
