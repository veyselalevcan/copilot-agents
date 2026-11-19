# OT hypothesis ranking

Rank by evidence, not by a fixed order. Most OT anomalies have non-malicious causes, so start from that prior and move it only with evidence.

## Hypotheses to test

| Hypothesis | Evidence that supports it | Evidence that weakens it |
|---|---|---|
| Sensor or instrument fault | Single tag affected; value frozen, flat-lined or out of range; field reading disagrees; calibration overdue; redundant sensor disagrees | Several independent tags change together; changes line up with network commands |
| Equipment failure | Mechanical alarms, vibration or temperature trends, maintenance history | Normal equipment diagnostics |
| Operator error | Operator action logged at the right time; shift change; procedure deviation | No operator session; action at a time nobody was on shift |
| Misconfiguration or change | Recent logic, setpoint or firmware change; change ticket; vendor visit | No change records and running logic matches baseline |
| Cyber activity | Unexpected remote session; commands from an unusual host or account; logic or setpoint changes without a ticket; HMI value differs from field value (view manipulation); several layers involved in sequence; security alerts | Clean remote access logs; logic matches baseline; field and HMI values agree |

## Method

1. List the hypotheses above.
2. For each, write the evidence for, the evidence against, and the missing evidence that would decide it.
3. Rate each as Likely, Possible or Unlikely, with one sentence of reasoning.
4. Name the single next check that would best separate the top two hypotheses.
5. Keep timing alone (two events close together) as weak evidence. State it as correlation.
