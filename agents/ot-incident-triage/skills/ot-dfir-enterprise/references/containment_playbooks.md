# Containment playbooks (OT-safe)

Every step needs an owner and operations approval. Prefer reversible steps. Keep the process safe before keeping it running.

## Now (minutes)

- Put the process in a safe state per operating procedures if safety is at risk; switch to local or manual control where procedures allow.
- Verify key values in the field (local gauges, manual readings).
- Disable or suspend suspicious remote access at the boundary (VPN account, jump host session) rather than inside the control network.
- Start passive capture and preserve logs.

## Next (hours)

- Tighten boundary firewall rules between Level 3.5 and Level 3, and between Level 3 and Level 2, with operations agreement.
- Reset credentials used in the suspicious activity, starting with remote access and engineering accounts.
- Compare controller logic and setpoints with the approved baseline, read-only.
- Increase monitoring on affected conduits.

## Later (days)

- Restore changed logic or setpoints from a verified baseline, through change control.
- Rebuild compromised Level 2-3 hosts from known-good images.
- Review vendor and contractor access model.
- Run a lessons-learned review with operations, engineering and security.

## Avoid during the incident

- Pulling cables or isolating controllers without a safe-state plan.
- Mass password resets that lock operators out of HMIs.
- Patching or reflashing controllers before evidence capture.
