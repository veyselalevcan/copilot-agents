# IEC 62443 review

IEC 62443-3-3 groups system requirements under seven foundational requirements (FR). After an incident, name the FRs the evidence shows were weak, and the zone or conduit where it happened.

| FR | Name | Questions after an incident |
|---|---|---|
| FR 1 | Identification and authentication control | Were shared or default accounts used? Was MFA in place for remote access? |
| FR 2 | Use control | Did the account have more rights than its role needed? Could it write to controllers? |
| FR 3 | System integrity | Were logic and firmware changes detected? Is there a verified baseline? |
| FR 4 | Data confidentiality | Were credentials or project files exposed? |
| FR 5 | Restricted data flow | Did traffic cross zones without a conduit control? Was there a direct path from IT or remote access to Level 1-2? |
| FR 6 | Timely response to events | Were events logged, monitored and alerted on time? |
| FR 7 | Resource availability | Did the process keep running safely? Were backups and manual operation available? |

Also note: zone and conduit design (62443-3-2), the target security level for the affected zone if known, and supplier or integrator duties (62443-2-4) when vendor access was involved. Mark security level claims unverified unless the user provides them.
