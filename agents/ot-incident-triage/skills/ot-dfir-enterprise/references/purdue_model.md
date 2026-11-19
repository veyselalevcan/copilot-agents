# Purdue model for OT incident scoping

| Level | Typical assets | Investigation note |
|---|---|---|
| 0 Process | Sensors, actuators, valves, pumps, drives | Physical evidence: field checks, calibration records, local readings |
| 1 Basic control | PLCs, RTUs, safety controllers (SIS), IEDs | Controller logic, mode, diagnostic buffer, firmware version |
| 2 Supervisory | HMI, SCADA servers, engineering workstations | Operator actions, alarm logs, project files, logged-on users |
| 3 Site operations | Historian, MES, OT domain services, patch and AV servers | Time-series trends, audit logs, backups |
| 3.5 OT DMZ | Jump hosts, remote access gateways, data diodes, replication | Remote session logs, VPN and firewall records |
| 4-5 Enterprise | IT network, ERP, email, internet | Initial access often starts here |

## How to use it

- Record the level of every affected asset and the conduit (connection path) between levels.
- Any path that reaches Level 1 or 2 from Level 3.5 or above without a broker deserves attention.
- Safety instrumented systems sit beside Level 1. Treat any sign of SIS involvement as safety-critical.
- Note whether the timeline moves downward through the levels (for example remote login at 3.5, then engineering workstation at 2, then PLC writes at 1). That pattern supports a cyber hypothesis but does not prove it.
