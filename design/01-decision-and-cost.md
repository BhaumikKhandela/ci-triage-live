# Slice 01 — decision and cost

## Responsibility
Define the external contract for the system's release-action recommendation or abstention and the cost model used to evaluate those outputs.

## Reads
- The Phase 00 system boundary and permitted inputs.
- The derived Phase 01 output space.
- The decision and cost assumptions established for the running CI incident.

## Emits
- Exactly one of three release-action recommendations or an abstention requiring manual investigation.
- For abstention, the caller must manually investigate the failure, evaluate the findings and evidence, and make the release decision.
- A cost model using currency as the unit because engineer time, CI compute, infrastructure, release delay, and user-facing consequences can all be expressed in monetary terms.
- Current estimated costs for wrong recommendations and abstention, including conditional costs where the downstream outcome is uncertain.
- Objective: minimize expected monetary cost across recommendations and abstentions.

## Refuses
The system abstains when the available evidence is insufficient to support one of the three release-action recommendations.

## Constraint
Abstention must have a non-zero explicit monetary cost so it cannot become a free escape from making recommendations.

## Cost model
The costs are asymmetric because different wrong recommendations produce different consequences. The working estimates are:

| Ground-truth cause | Predicted cause | Recommendation | Consequence | Cost |
|---|---|---|---|---:|
| Genuine code/product failure | Flaky test | Isolate the test and release | A real defect may reach users, causing support tickets and user impact, followed by engineering remediation, CI, infrastructure, and redeployment costs. | $5,000 |
| Flaky test | Genuine code/product failure | Stop the release | The release is unnecessarily delayed and engineers spend time reviewing the code and rerunning tests/CI before redeployment. There is no user-facing bad release cost. | $2,500 |
| CI infrastructure/environment failure | Genuine code/product failure | Stop the release | The release is unnecessarily delayed and engineers incur code-review, test/CI rerun, and infrastructure/redeployment costs. | $2,500 |
| CI infrastructure/environment failure | Flaky test | Isolate the test and release | Conditional: if subsequent CI passes and the release is unaffected, the cost is limited to investigation/CI/infrastructure work; if the failure recurs or the isolation masks a real issue, additional remediation and potentially user-facing costs occur. | Conditional; not yet numerically estimated |
| Any ground-truth cause | Abstain | Manual investigation | The engineer must independently investigate the failure and then make the release decision, in addition to the work required by the eventual action. | $3,750 |

Abstention is not free, but it is not assumed to be more expensive than every wrong recommendation; its cost depends on the investigation and eventual action.

## Objective
Minimize expected monetary cost across recommendations and abstentions, using the explicit monetary cost of abstention rather than a separate coverage constraint.

## Connects to
- Earlier slice: Phase 00 — system boundary.
- Later slice: Phase 02 — evaluation component.
