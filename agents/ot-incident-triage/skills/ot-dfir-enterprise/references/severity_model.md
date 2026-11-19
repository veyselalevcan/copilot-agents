# Severity model

Score five factors from 0 to 4. Total = sum x 5 (range 0-100).

| Factor | 0 | 2 | 4 |
|---|---|---|---|
| Asset criticality | Non-essential | Supports production | Essential service or safety-related asset |
| Safety impact | None | Possible with further failures | Credible harm to people or environment |
| Availability impact | None | Degraded operation | Process stopped or service to customers lost |
| Environmental or regulatory impact | None | Limited, contained | Release, permit breach or reportable event |
| Confidence of malicious activity | No indicators | Some indicators | Confirmed malicious activity |

Use 1 and 3 for in-between cases.

| Total | Severity |
|---|---|
| 0-25 | Low |
| 26-50 | Medium |
| 51-80 | High |
| 81-100 | Critical |

## Overrides

- Credible safety impact (score 3 or 4) sets a floor of High, whatever the total.
- SIS tampering or bypass, suspected or confirmed, is Critical.
- State the factor scores and one sentence for each, so a reviewer can disagree with a specific score.
- Re-score when new evidence arrives and record the change.
