# Industrial protocol profiles for investigators

Defensive view: what to look for in passive captures and logs. No exploitation detail.

| Protocol | Typical use | Investigation focus |
|---|---|---|
| Modbus/TCP (port 502) | PLCs, RTUs, meters | No built-in authentication. Look at which hosts send write function codes, at what time and to which registers. Compare with the normal set of masters |
| DNP3 (port 20000) | Utilities, water, power | Control and operate commands, unsolicited responses, Secure Authentication use, unexpected masters |
| EtherNet/IP and CIP (44818, 2222) | Rockwell and others | Program uploads or downloads, mode changes, controller identity requests from unusual hosts |
| S7comm / S7comm-plus (102) | Siemens | Program block transfers, CPU stop or start, unusual engineering connections |
| IEC 60870-5-104 (2404) | Power grid | Command messages from unknown stations |
| IEC 61850 MMS and GOOSE | Substations | Unexpected control operations or GOOSE traffic |
| OPC UA (4840) / OPC DA | Data exchange to Level 3 | Security mode, certificate use, new clients |
| BACnet (47808) | Building automation | Write property requests from unexpected hosts |

## General signs worth checking

- A new host talking to controllers, or a known host at an unusual time
- Write, download, mode change or restart commands without a change ticket
- Engineering software sessions from hosts that are not engineering workstations
- Traffic between zones that the design does not allow
