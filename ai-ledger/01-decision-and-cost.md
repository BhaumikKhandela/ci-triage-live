# Phase 01 — AI ledger

## Proposed
Optimize accuracy of the predicted underlying cause rather than monetary cost.

## Rejected / narrowed to
Use expected monetary cost across recommendations and abstentions as the objective.

## Because
The consequences of different prediction errors are asymmetric. Predicting a wrong cause can lead to materially different release actions and financial consequences. Optimizing cause-prediction accuracy alone would treat all errors as equally costly and would not reflect the actual purpose of the system.

Abstention is assigned an explicit non-zero monetary cost so that it remains a useful safety mechanism rather than a free escape from making recommendations.

## Review
1. slice fit — The output contract is derived from the three Phase 00 actions plus the ambiguous case that forced abstention.
2. correctness — The engineer remains the final decision-maker; abstention requires manual investigation and a decision based on findings and evidence.
3. ML validity — No model or experiment is introduced in this phase.
4. necessity — The cost model is necessary because the system's errors have asymmetric consequences.

## Ponytail pass
Not applicable; no code in Phase 01.
