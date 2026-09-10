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
| Genuine code/product failure | CI infrastructure/environment failure | Rerun the CI pipeline | The real bug is caught when the rerun fails, so the release is contained, but the pipeline wastes another cycle, developer feedback is delayed, and engineering time is spent waiting on a rerun that cannot resolve the underlying code failure. | $3,500 |
| Flaky test | Genuine code/product failure | Stop the release | The release is unnecessarily delayed and engineers spend time reviewing the code and rerunning tests/CI before redeployment. There is no user-facing bad release cost. | $2,500 |
| Flaky test | CI infrastructure/environment failure | Rerun the CI pipeline | The flaky failure may disappear on rerun, so the code ships without a product defect, but CI compute and engineer time are wasted and the pipeline is delayed. | $1,500 |
| CI infrastructure/environment failure | Genuine code/product failure | Stop the release | The release is unnecessarily delayed and engineers incur code-review, test/CI rerun, and infrastructure/redeployment costs. | $2,500 |
| CI infrastructure/environment failure | Flaky test | Isolate the test and release | The test result is inconclusive, so isolating it can become a blind release. If the code is buggy, a real defect may ship; if the code is clean, the valid infrastructure failure is still left unresolved. The working expected cost of this wrong action is estimated at $4,000. | $4,000 |
| Any ground-truth cause | Abstain | Manual investigation | The engineer must independently investigate the failure and then make the release decision, in addition to the work required by the eventual action. | $3,750 |

The abstention cost is non-zero but is not assumed to be more expensive than every wrong recommendation; its cost reflects the manual investigation burden.

## Objective
Minimize expected monetary cost across recommendations and abstentions, using the explicit monetary cost of abstention rather than a separate coverage constraint.
