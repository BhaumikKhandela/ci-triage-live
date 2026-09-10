# Problem

## The decision
At 02:47, an engineer responsible for the release must decide what to do about a red CI build before the 09:00 release deadline.

## The actions
The engineer can:
1. Isolate the failing test and move forward with the release.
2. Rerun the CI pipeline.
3. Stop the release altogether.

## The prediction
The system predicts one of the three possible release actions as its recommendation, or abstains when the available evidence is insufficient. The prediction is not the release decision: the engineer remains responsible for making the final decision.

## The output space
When the available evidence is insufficient to distinguish among the possible causes, the system abstains rather than pretending one action is supported. The engineer then manually investigates the failure, evaluates the findings and evidence, and makes the release decision.

## The cost
Currency is used as the cost unit because engineer time, CI compute, infrastructure, release delay, and user-facing consequences can all be expressed in monetary terms. The costs are asymmetric because different wrong recommendations produce different consequences.

| Ground-truth cause | Predicted cause | Recommendation | Consequence | Cost |
|---|---|---|---|---:|
| Genuine code/product failure | Flaky test | Isolate the test and release | A real defect may reach users, causing support tickets and user impact, followed by engineering remediation, CI, infrastructure, and redeployment costs. | $5,000 |
| Flaky test | Genuine code/product failure | Stop the release | The release is unnecessarily delayed and engineers spend time reviewing the code and rerunning tests/CI before redeployment. There is no user-facing bad release cost. | $2,500 |
| CI infrastructure/environment failure | Genuine code/product failure | Stop the release | The release is unnecessarily delayed and engineers incur code-review, test/CI rerun, and infrastructure/redeployment costs. | $2,500 |
| CI infrastructure/environment failure | Flaky test | Isolate the test and release | Conditional: if subsequent CI passes and the release is unaffected, the cost is limited to investigation/CI/infrastructure work; if the failure recurs or the isolation masks a real issue, additional remediation and potentially user-facing costs occur. | Conditional; not yet numerically estimated |
| Any ground-truth cause | Abstain | Manual investigation | The engineer must independently investigate the failure and then make the release decision, in addition to the work required by the eventual action. | $3,750 |

The abstention cost is non-zero but is not assumed to be more expensive than every wrong recommendation; its cost depends on the investigation and eventual action.

## Objective
Minimize expected monetary cost across recommendations and abstentions, using the explicit monetary cost of abstention rather than a separate coverage constraint.
