# Slice 00 — system boundary

## Responsibility
Help the on-call engineer respond to a red CI build by predicting one appropriate release action or abstaining when the available evidence is insufficient.

## Reads
- Test logs from the failing CI run.
- The failing test.
- The codebase.

## Emits
- Exactly one recommendation: isolate the test and move forward with the release; rerun the CI pipeline; or stop the release.
- Or an abstention when the system does not have sufficient evidence to make a recommendation.
- Supporting evidence/explanation for the recommendation.
- The engineer remains responsible for the final release decision; the system does not execute the recommended action.

## Refuses
Abstain rather than recommend when the available evidence is insufficient to support one of the three actions.

## Constraint
The system must never merge, create, or delete a branch, and must never change code or tests.

## Connects to
- Earlier slice: none; this is the system boundary.
- Later slice: the external contract defines the precise output space and downstream handling of recommendations and abstention.
