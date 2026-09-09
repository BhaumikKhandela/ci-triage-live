# Problem

## The decision
At 02:47, an engineer responsible for the release must decide what to do about a red CI build before the 09:00 release deadline.

## The actions
The engineer can:
1. Isolate the failing test and move forward with the release.
2. Rerun the CI pipeline.
3. Stop the release altogether.

## The prediction
The system predicts which of those three actions is appropriate, or abstains when the available evidence is insufficient. The prediction is not the release decision: the engineer remains responsible for making the final decision.

## The cost
The costs are asymmetric and depend on the action recommended versus the action that was appropriate.

| System recommends | Appropriate action | Cost |
|---|---|---|
| Isolate | Stop release | Potentially severe; a bad release may reach users. |
| Stop | Isolate | Unnecessary release delay. |
| Rerun | Isolate | Depends on the rerun: if CI fails, the system is activated again and another human intervention is required; if it passes, the app is released and there is no identified cost from this error. |
| Rerun | Stop | CI fails again and the system is activated again, causing another human intervention during decision making. |
| Abstain | Any action | Manual review cost. |

These costs are qualitative at this stage; no numerical cost has been established by an experiment or command yet.
