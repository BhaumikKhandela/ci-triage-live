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
- A cost model using currency as the unit.
- Current estimated costs for wrong recommendations and abstention, including conditional costs where the downstream outcome is uncertain.
- Objective: minimize expected monetary cost across recommendations and abstentions.

## Refuses
The system abstains when the available evidence is insufficient to support one of the three release-action recommendations.

## Constraint
Abstention must have a non-zero explicit monetary cost so it cannot become a free escape from making recommendations.

## Connects to
- Earlier slice: Phase 00 — system boundary.
- Later slice: Phase 02 — evaluation component.
