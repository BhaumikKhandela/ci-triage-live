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
- Current estimated costs for wrong recommendations and abstention.
- Objective: minimize expected monetary cost across recommendations and abstentions.

## Refuses
The system abstains when the available evidence is insufficient to support one of the three release-action recommendations.

## Constraint
Abstention must have a non-zero explicit monetary cost so it cannot become a free escape from making recommendations.

## Cost model
The costs are asymmetric because different wrong recommendations produce different consequences. The table only assigns prediction-error cost to wrong recommendation/cause pairs; correct predictions have no prediction-error cost assigned.

| Ground-truth cause | Predicted cause | Recommendation | Consequence | Cost |
|---|---|---|---|---:|
| Genuine code/product failure | Flaky test | Isolate the test and release | A real defect may reach users, causing support tickets and user impact, followed by engineering remediation, CI, infrastructure, and redeployment costs. | $5,000 |
| Genuine code/product failure | CI infrastructure/environment failure | Rerun the CI pipeline | The real bug is caught when the rerun fails, so the release is contained, but the pipeline wastes another cycle, developer feedback is delayed, and engineering time is spent waiting on a rerun that cannot resolve the underlying code failure. | $3,500 |
| Flaky test | Genuine code/product failure | Stop the release | The release is unnecessarily delayed and engineers spend time reviewing the code and rerunning tests/CI before redeployment. There is no user-facing bad release cost. | $2,500 |
| Flaky test | CI infrastructure/environment failure | Rerun the CI pipeline | The flaky failure may disappear on rerun, so the code ships without a product defect, but CI compute and engineer time are wasted and the pipeline is delayed. | $1,500 |
| CI infrastructure/environment failure | Genuine code/product failure | Stop the release | The release is unnecessarily delayed and engineers incur code-review, test/CI rerun, and infrastructure/redeployment costs. | $2,500 |
| CI infrastructure/environment failure | Flaky test | Isolate the test and release | The test result is inconclusive, so isolating it can become a blind release. If the code is buggy, a real defect may ship; if the code is clean, the valid infrastructure failure is still left unresolved. The working expected cost of this wrong action is estimated at $4,000. | $4,000 |
| Any ground-truth cause | Abstain | Manual investigation | The engineer must independently investigate the failure and then make the release decision, in addition to the work required by the eventual action. | $3,750 |

Abstention is not free, but it is not assumed to be more expensive than every wrong recommendation; its cost reflects the manual investigation burden.

## Objective
Minimize expected monetary cost across recommendations and abstentions, using the explicit monetary cost of abstention rather than a separate coverage constraint.

## Connects to
- Earlier slice: Phase 00 — system boundary.
- Later slice: Phase 02 — evaluation component.
