# MITRE ATT&CK for ICS mapping

Map only what the evidence supports. For each mapping record: technique ID and name, evidence, confidence (High, Medium, Low), data source, affected asset, process impact.

Verify technique IDs and names against https://attack.mitre.org/matrices/ics/ before a final report. If unsure of an ID, give the name and mark the ID unverified.

## Techniques often relevant to OT triage

| ID | Name | Typical evidence |
|---|---|---|
| T0822 | External Remote Services | VPN or remote access session into OT |
| T0886 | Remote Services | Remote desktop or similar from jump host into Level 2 |
| T0859 | Valid Accounts | Legitimate account used at an unusual time or from an unusual host |
| T0801 | Monitor Process State | Unusual reads or polling of process values |
| T0861 | Point & Tag Identification | Enumeration of tags or points |
| T0855 | Unauthorized Command Message | Write or control commands from an unexpected source |
| T0836 | Modify Parameter | Setpoint or parameter changed without a change record |
| T0831 | Manipulation of Control | Process driven to an abnormal state by commands |
| T0832 | Manipulation of View | HMI shows values that do not match the field |
| T0856 | Spoof Reporting Message | Forged values reported to supervisory systems |
| T0815 | Denial of View | Operators lose visibility of the process |
| T0813 | Denial of Control | Operators cannot control the process |
| T0843 | Program Download | Logic download to a controller |
| T0889 | Modify Program | Controller logic differs from baseline |
| T0878 | Alarm Suppression | Alarms disabled or missing during the event |

## Impact techniques

Loss of View, Loss of Control, Loss of Safety, Loss of Availability and Damage to Property describe consequences. Use them only when the consequence occurred or was close to occurring, and say which.
