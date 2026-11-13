# Labeling Guide

Used to hand-label the evaluation set (`data/labeled-eval-set.csv`). The labels you assign here are the ground truth the classifier is measured against, so follow these rules consistently.

## Fields to label

| Field | Allowed values |
|---|---|
| primary_category | Technical / Infrastructure, Process / Workflow, Scope & Product Direction, External Dependencies, No blocker, Uncategorized |
| sub_issue_tag | see taxonomy below, plus None and Uncategorized |
| severity | High, Medium, Low, N/A |

## Taxonomy

| Primary category | Sub-type | Use when the comment is about... |
|---|---|---|
| Technical / Infrastructure | Environment down | Dev, test or staging environment, local setup, VPN or database unavailable or broken |
| | Tooling/API limits | Quotas, rate limits, licenses, credits or plan limits exhausted |
| | CI/CD failures | Pipeline failing, flaky tests in CI, slow or stuck builds and runners |
| | Access & permissions | Missing or revoked access to systems, data, accounts |
| Process / Workflow | Meeting overhead | Too many, too long or unproductive meetings |
| | Unclear acceptance criteria | Missing, vague, conflicting or buried requirements or definition of done |
| | Delayed code reviews | PRs waiting too long for review or approval |
| | Late handoff to QA | Work reaching QA late in the sprint, QA crunch or idle time |
| Scope & Product Direction | Mid-sprint scope creep | New or changed requirements added after the sprint started |
| | Sudden priority shifts | Sprint goal or priorities reshuffled mid-sprint |
| External Dependencies | Blocked on cross-team work | Waiting on another internal team (platform, data, design, mobile, business) |
| | Vendor clarification | Waiting on an outside vendor for answers, credentials or fixes |
| No blocker | None | Praise, thanks, neutral or purely positive comments |
| Uncategorized | Uncategorized | A real issue that does not fit any sub-type above |

## Severity rules

- **High:** complete work stoppage, or multiple people blocked (environment fully down, core tooling unavailable).
- **Medium:** work continues but efficiency drops significantly while waiting (waiting on clarification, sign-offs, reviews, handoffs).
- **Low:** annoyance or minor friction that did not stop delivery (meetings running over).
- **N/A:** used only for No blocker comments. Uncategorized issues still get a severity if you can judge one.

If a comment gives no clear impact, choose the level the stated words support, not the one you imagine. A comment with a duration or a "couldn't do X" statement usually supports a higher severity than one that only expresses annoyance.

## Decision rules

1. **One label per comment.** If a comment has two issues, label the one that most blocks work. If they are equal, label the first one mentioned.
2. **Label what the comment says, not what you know.** Do not use your knowledge of how the data was generated.
3. **Positive or neutral comments** get No blocker / None / N/A.
4. **Vague comments with no issue** ("meh", "busy sprint", "idk") get No blocker / None / N/A. If a vague comment clearly signals a problem but not which, use Uncategorized.
5. **Real problems outside the taxonomy** (burnout, workload balance, hardware, on-call, feature ideas, support interruptions) get Uncategorized.
6. **Severity follows the comment's impact, not its topic.** The same sub-type can be High in one comment and Low in another.
7. **Choose the cause, not the symptom.** "PR stuck because CI is red" is CI/CD failures, not Delayed code reviews.

## Final tie-break rules (used while labeling)

These rules were applied consistently to the whole evaluation set.

**Scope and requirements**
- New or changed requirement after work started (including a design change after build, or a client change before deployment): **Mid-sprint scope creep**.
- Requirement existed but was missing, vague, conflicting or buried in a ticket: **Unclear acceptance criteria**.
- The whole sprint direction or goal changed: **Sudden priority shifts**.
- Waiting on a product decision with no requirement written: **Unclear acceptance criteria**.

**Reviews and handoffs**
- Late or rework-causing reviewer feedback on finished work: **Delayed code reviews**. Changed requirements from product or stakeholders: **Mid-sprint scope creep**.
- No review happening at all (not a slow one): **Uncategorized**.
- Work reaching QA late because it was stuck in review: **Delayed code reviews** (root cause over symptom).

**Technical and access**
- Waiting on IT or another team for access or permissions: **Access & permissions**, even though another team fixes it.
- Staging or test database or disk full or unavailable: **Environment down**.
- Slow or stuck builds, including data build jobs, and tests failing only in CI: **CI/CD failures**.
- Quotas, rate limits, credits or license seats exhausted: **Tooling/API limits**.

**External**
- Waiting on an outside vendor for answers, credentials, renewals or fixes (including asking a vendor about their limits): **Vendor clarification**. A vendor-caused outage is Vendor, not Environment down.
- Waiting on another internal team for a deliverable (platform, data, design, business): **Blocked on cross-team work**.

**Two issues in one comment**
- Label the issue that most blocks work. If equal, label the first one mentioned. If one is clearly the root cause of the other, label the root cause.

**Non-blockers and out-of-taxonomy**
- Praise, neutral or purely positive comments, and mood-only or vague comments with no cause ("meh", "felt slow", "kinda stressful"): **No blocker / None / N/A**.
- Real issues outside the taxonomy (burnout, on-call fairness, hardware, support interruptions, outdated runbook, feature ideas, time logging): **Uncategorized**. Interruptions from outside the sprint are Uncategorized, not scope creep.

**Severity**
- The word "blocked" alone does not make a comment High. High needs a complete stoppage or several people blocked.
- A comment that gives no stated impact gets the lowest level its words support (often Low).
- Long waits with reduced efficiency but continued work are Medium.

## Process rules

- Label in one sitting or two, with the model's output closed.
- Do not change a label after seeing model results. If you realize a rule was wrong, fix the rule, relabel all affected rows, and log the change.
- The 20 rows marked `holdout` are used once, at the end. Never tune the prompt on them.
