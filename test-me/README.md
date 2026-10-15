# test-me

An agent skill for deciding whether a tool, or a feature you plan to borrow from one, actually does the job. The decision rests on evidence from using it, not on its README.

## Install

In Claude Code:

```
/plugin marketplace add 0xOzen/test.me
/plugin install test-me@aequai-skills
```

Other agents that read `SKILL.md` files can use the skill folder `skills/test-me/` directly.

## What it does

- Splits each tool into single, testable claims. Each claim gets one category: code/architecture, UI/UX, security/privacy, reliability/ops, integration, or licence/cost.
- Freezes the test (input, expected result, unacceptable result) before the first run.
- Records one evidence state per claim: Used, Docs only, Blocked, Not tested, Inconclusive. Only Used claims are scored.
- Ends each claim in one of four verdicts: Keep current method, Limited pilot, Adopt, Drop for now.
- For a decision that rests on several tools, adds a round guide with a shared brief, a roll-up, and an independent audit.

## Files

| File | Purpose |
|---|---|
| `skills/test-me/SKILL.md` | The method, its rules and its safety boundary |
| `skills/test-me/rubric.md` | Hard gates, and weighted scoring for Used claims only |
| `skills/test-me/report.md` | The report template |
| `skills/test-me/round.md` | Several tools at once: shared brief, roll-up, audit |
| `evals/` | Trigger tests for the skill (`claude plugin eval`) |

## Why

The author used this method on more than a dozen agent tools. Several claims that sounded solid in the docs did not hold up once the tool was run:
- a security setting that the tool accepted but never enforced;
- an approver list that still let an unlisted approver through;
- an audit chain that did not notice its last entries being deleted;
- a "single egress path" that a launched component could bypass.

The skill is built so that gaps like these show up before you build on the tool.

## Safety

Use synthetic data only, and run each trial in a sandbox or as a separate OS user. If a test hits a login, a sign-up, a CAPTCHA, a paid plan or a permission prompt, stop and ask a human. Never put secrets in a report.

## Licence

MIT, see [LICENSE](LICENSE).
