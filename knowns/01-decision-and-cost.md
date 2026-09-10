# Phase 01

| Was | Now | Statement | Evidence |
|---|---|---|---|
| unknown | known | The system has four outputs: isolate and release, rerun CI, stop release, or abstain. | decisions/01-output-space.md |
| unknown | known | Abstention requires the engineer to manually investigate, evaluate findings and evidence, and make the release decision. | decisions/01-output-space.md |
| unknown | known | Currency is the chosen cost unit. | Builder decision in phase 01 conversation |
| unknown | known | Wrong recommendations have asymmetric monetary consequences. | design/01-decision-and-cost.md |
| unknown | known | The estimated cost of a genuine code failure predicted as flaky, leading to isolation and release, is $5,000. | Builder estimate in phase 01 conversation |
| unknown | known | The estimated cost of an unnecessary stop for a flaky test or CI infrastructure failure is $2,500. | Builder estimate in phase 01 conversation |
| unknown | known | The estimated cost of abstention and manual investigation is $3,750. | Builder estimate in phase 01 conversation |
| unknown | known | A CI infrastructure failure predicted as a flaky test and followed by isolation/release has a conditional cost because downstream outcomes vary. | Builder decision in phase 01 conversation |
| unknown | known | The objective is to minimize expected monetary cost across recommendations and abstentions, with abstention represented by its explicit monetary cost rather than a separate coverage constraint. | Builder decision in phase 01 conversation |
| unknown | known | Accuracy of predicted cause is not the objective because different errors have different monetary consequences. | ai-ledger/01-decision-and-cost.md |
| unknown | known-unknown | The numerical value/probability model for the conditional CI-infrastructure-to-flaky-test cost has not yet been established. | — |
