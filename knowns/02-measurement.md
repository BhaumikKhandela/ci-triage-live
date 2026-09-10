# Phase 02 — measurement

| Was | Now | Statement | Evidence |
|---|---|---|---|
| unknown | known | The Phase 02 hypothesis is that accuracy alone will make a constant “not flaky” predictor look deceptively strong because flaky tests are rare, while recall and cost-sensitive measurements will expose that it is useless for detecting flaky failures. | Builder-approved hypothesis in Phase 02 conversation |
| unknown | known | The constant baseline predicts “not flaky” for every input. | Phase 02 baseline experiment |
| unknown | known | On a hand-written toy array with 100 examples and 3 flaky positives (3%), the constant predictor achieved 97% accuracy. | Phase 02 baseline experiment |
| unknown | known | On the same array, the constant predictor achieved 0% recall. | Phase 02 baseline experiment |
| unknown | known | The baseline supports the hypothesis: accuracy can look strong under class imbalance while recall reveals that the constant predictor catches none of the flaky cases. | Phase 02 baseline experiment |
| unknown | known | Accuracy alone is therefore inadequate as the primary measurement for this problem. | Phase 02 baseline experiment |
