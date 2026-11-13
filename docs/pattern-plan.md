# Pattern Plan (hidden ground truth)

Do not paste this into the classifier prompt. It is only for checking the pattern detector.

Rule: a sub-type is **flagged** if it appears in 3 or more of the last 5 sprints (S4 to S8).
Counts are approximate and include a few multi-issue comments.

| Sub-type | Sprints present | ~Count | Detector should flag? |
|---|---|---|---|
| CI/CD failures | S1, S2, S4, S5, S6 | 22 | Yes (S4, S5, S6) |
| Unclear acceptance criteria | S2, S3, S4, S5, S6, S7 | 20 | Yes (4 of 5) |
| Delayed code reviews | S3 to S8, rising | 24 | Yes (5 of 5) |
| Late handoff to QA (new) | S4, S5, S6, S7 | 8 | Yes (4 of 5) |
| Meeting overhead | S1 to S8 | 16 | Yes, but mostly Low severity |
| Blocked on cross-team work | S4, S5, S6, S8 | 12 | Yes (4 of 5) |
| Environment down | S3, S7 | 10 | No (one-off spikes) |
| Access and permissions (new) | S2, S3, S5 | 7 | No (1 of 5) |
| Tooling/API limits | S4, S6 | 7 | No (2 of 5) |
| Scope creep | S1, S2, S6, S8 | 14 | No (2 of 5) |
| Sudden priority shifts | S1, S4, S8 | 9 | No (2 of 5) |
| Vendor clarification | S1, S2 only | 8 | No (resolved early) |

## Not blockers (the detector should ignore these)

- Positive comments (~23)
- Vague comments (~14)
- Out-of-taxonomy items (~11): morale, burnout, workload, feature ideas, time logging, hardware, on-call fairness, support interruptions, a production runbook, a coffee machine. These should land in "Uncategorized / needs human review".

## Ambiguous boundary cases (about 8)

Comments where scope creep vs. priority shift, unclear AC vs. scope, review delay vs. changing requirements, or CI vs. test problem is honestly debatable. Decide these in your labeling guide and note the decision.

## Taxonomy changes made after reviewing a real retro dataset's themes

- Added **Access and permissions** under Technical / Infrastructure.
- Added **Late handoff to QA** under Process / Workflow.
- Added a **No blocker / Not applicable** label for positives and vague comments.
- Out-of-taxonomy items go to **Uncategorized, needs human review**.
