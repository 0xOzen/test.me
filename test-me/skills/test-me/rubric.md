# Tool Trial Rubric

Score only claims in state `Used`. The weights are defaults to be adjusted per user; they are not validated.

## Hard gates (pass/fail, never averaged)

Data and privacy terms acceptable · license allows the intended use · required export available · within approved budget. One failure means `Drop for now`, whatever the scores.

## Weighted dimensions (1-5)

| Dimension | Weight | Question |
|---|---:|---|
| Task completion | 35% | Was the job done end to end? |
| Output correctness | 25% | Errors, invented facts, missing fields, unusable output? |
| Human effort | 20% | Setup, interventions, corrections, final check |
| Workflow fit | 10% | Does the output go where it is needed? |
| Total cost | 10% | Tool, usage, required extras |

| Score | Meaning |
|---|---|
| 5 | Better than the baseline with no correction |
| 4 | Better than the baseline, minor correction |
| 3 | Same as the baseline |
| 2 | Worse than the baseline, usable |
| 1 | Not usable |

If any dimension could not be measured, show `Not tested` for it and give no total.
