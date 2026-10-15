# Tool Trial Report Template

```markdown
# Tool trial: <tool or feature list>

Date: <YYYY-MM-DD> · Tester: <human/agent> · Job: <one sentence>
Baseline: <current method or existing asset>

## Decision
<One line per tool: verdict and the reason in one sentence.>

## Frozen test plan
Written at <timestamp copied from plan.md>, before the first run. First evidence file: <path>, <mtime>. Changes after that are listed with their own timestamp.
| # | Input | Expected | Unacceptable | Human help allowed |
|---|---|---|---|---|

## Claims
| # | Claim | Category | State | Verdict | Runs | vs baseline | Evidence / next test |
|---|---|---|---|---|---|---|---|
| 1 | <single testable claim> | <one of six> | Used / Docs only / Blocked / Not tested / Inconclusive | Keep current method / Limited pilot / Adopt / Drop for now | <executions of the frozen input; 0 for a source read or a repo test suite> | <better, same, worse, not known> | <file that exists in the delivered evidence; for a source cite: commit plus the cited lines copied into the evidence; for every state except Used: the test that would move it to Used> |

A roll-up across several reports keeps one verdict label per cell. A pointer ("see round 1"), a state or prior evidence goes in the reason column; a row checked without a trial is marked "(docs screen)".

## Scores (Used claims only)
<rubric table or "none: no claim was used">

## Run record
Version, date, account/plan, environment, inputs, repetitions, failure type per failed run.

## Not checked
<What was skipped and why.>

## Left on the machine
<Apps, images, packages, preferences and files created outside the trial folder, and what was cleaned up.>
```
