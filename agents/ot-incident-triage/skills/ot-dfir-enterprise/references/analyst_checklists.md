# Analyst checklists

## First 15 minutes

- Is anyone at risk? Is the process in a safe state? Are safety systems healthy?
- Who is the operations lead and who approves changes to the process?
- What exactly was observed, where, and when (with time zone and clock source)?
- Is the event ongoing, recurring or over?
- What changed recently: maintenance, logic changes, firmware, new users, vendor access?

## Questions to ask the user

- Site type, process and affected unit
- Asset list with Purdue level, vendor and model where known
- Alarm and event list with timestamps
- Historian trends for the affected tags, before and after the event
- Remote access, VPN and jump host activity in the window
- Engineering workstation activity and logged-on accounts
- Network monitoring or IDS alerts
- Field verification results (local gauge, manual reading)

## Evidence to preserve (OT-safe order)

1. Notes of what operators saw and did, with times
2. Alarm and event logs, HMI screenshots
3. Historian exports for the relevant window
4. Passive network capture from a SPAN or TAP (no active scanning of controllers)
5. Remote access, firewall and VPN logs
6. Engineering workstation and HMI host images or triage collections, when operations allow
7. Controller project and logic: compare running logic with the approved baseline using vendor tools, read-only, with the vendor or controls engineer
8. Chain of custody record for every item

## Do not

- Run active scans, vulnerability scanners or aggressive discovery against Level 0-2 devices.
- Reboot, power cycle or reflash controllers before evidence is captured and operations agree.
- Install agents on HMIs or controllers during the incident without vendor approval.
