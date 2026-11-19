# Example: false tank level at a water treatment plant

## Symptom

The HMI shows the raw water tank at a normal level, but operators see water near the overflow.

## Case A: evidence points to a sensor fault

- Only the level tag is wrong; flows, pump status and valve positions match operator actions.
- The level value has been flat for six hours.
- The transmitter calibration is overdue.
- No remote sessions, no writes from unusual hosts, running logic matches baseline.

Ranking: sensor fault Likely; misconfiguration Possible; cyber activity Unlikely. Severity driven by safety and availability, not by malicious activity. Containment: manual level control, field verification, replace or recalibrate the transmitter.

## Case B: evidence points to cyber activity

- The pump and inlet valve start without operator action.
- The historian shows Modbus writes from an engineering workstation that is normally off at night.
- A contractor VPN login happened 24 minutes earlier.
- The HMI level differs from the field reading while the raw historian value shows the rise.

Ranking: cyber activity Likely; misconfiguration Possible; sensor fault Unlikely. Relevant techniques: External Remote Services, Unauthorized Command Message, Manipulation of View. Severity at least High because of overflow risk. Containment: safe state and manual control, suspend the contractor VPN account at the boundary, preserve logs and capture, compare logic with baseline read-only. Timing alone does not prove the chain; confirm with remote access logs and workstation evidence.

## Lesson

The same symptom leads to different conclusions. Rank by evidence and name the check that separates the top hypotheses.
