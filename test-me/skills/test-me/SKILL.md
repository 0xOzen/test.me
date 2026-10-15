---
name: test-me
description: Use when deciding whether to adopt a tool, app, library or a feature borrowed from one, when a "what to take from X" list rests on READMEs or product pages, or when someone asks "is this new tool worth switching to?"
---

# Tool Trial

## Overview

Decide whether a tool or borrowed feature does a specific job better than the current method, using evidence from actually using it. "Keep the current method" is a valid, often correct, result.

**Core rule: a claim nobody has used gets no score.** Reading the docs tells you what to test, not what works.

## When to Use

- A list of features to take from external tools, built from docs or demos
- "Should we switch to X?" / "Is X worth trying?"
- Re-checking an earlier adoption after a tool changed
- Several tools feeding one decision: also follow [round.md](round.md)

Not for: bug-hunting your own app (use a QA/dogfood skill), benchmarking models (use an eval harness).

## Process

1. **Job and baseline.** Write the concrete job, the current method (or existing asset that already covers it), hard constraints (data, license, budget, platform) and the effort allowed. If the user has `ade inventory` output or a similar setup listing, use it as the current-method inventory.
2. **Identify the exact tool.** Name the repository, commit or release, and how you know it is the one meant; if several projects share the name, say which you picked and why.
3. **One row per claim.** Split each tool into single, testable claims. Give each exactly one category from the table below. Two categories means two claims.
4. **Screen from docs.** Check the hard gates (license, data, platform, cost). A failed gate ends that claim: verdict `Drop for now`, state `Docs only`.
5. **Freeze the test.** Before the first run, fill the "Frozen test plan" section of the report (with a timestamp) per claim: input (synthetic data only), expected result, unacceptable failure, how much human help is allowed. Do not change the criteria after seeing the result.
6. **Use it.** Run the test in a separate session or sandbox. Record version, date, plan/account type, environment.
7. **Classify the outcome** (see Failure types). An agent getting stuck is not the product failing.
8. **Score only `Used` claims**, with [rubric.md](rubric.md). Fill the report from [report.md](report.md): decision first, then difference vs baseline, then evidence.

## Categories (one per claim)

| Category | Test method | Evidence |
|---|---|---|
| Code / Architecture | Read source, run its tests, write a small spike | commit, test output |
| UI / UX | Walk the flow end to end in the real UI | screenshots, steps |
| Security / Privacy | Try the forbidden thing: planted canary, denied permission, blocked egress | allowed/blocked log |
| Reliability / Ops | Interrupt, restart, kill mid-run; check recovery | logs, final state |
| Integration | Make one real connection (MCP, API, CLI, harness) | call record |
| License / Cost | Read the LICENSE text (not package metadata) and pricing at a dated URL | link + date |

A security setting that the tool accepts but never enforces is a Security claim, not Integration: test it by attempting the forbidden action.

## Evidence states

`Used` · `Docs only` · `Blocked` (access, account, approval) · `Not tested` · `Inconclusive`

Use exactly these five. The State cell holds one label and nothing else: `Used (partial)`, `Used (unit level)` or `Docs only (live test Blocked)` are violations. If only part of a claim was exercised, split it into two rows: the exercised part is `Used`, the rest keeps its own state. Evidence from someone else's run counts as `Used` only if their record shows the input and the result.

## Failure types

Product failed (it ran, output wrong) · Automation failed (a human can do it, the agent could not) · Access blocked · Inconclusive.

## Verdicts (pick one per claim)

`Keep current method` · `Limited pilot` · `Adopt` · `Drop for now`

The Verdict cell holds one label and nothing else; `Adopt (pattern only)` is written `Adopt` with "pattern only" in vs baseline. A verdict may not rest on a feature whose own state is not `Used`. A run that hits the plan's "Unacceptable" column cannot yield `Adopt`. An `Inconclusive` claim is reported in the Decision as "not shown", never as a result. `Adopt` requires state `Used`. A `Docs only` claim can be at most `Limited pilot`, and its row must name the test that would move it to `Used`.

## Safety boundary

Synthetic data only. No personal browser profile, no real customer data, no paid sign-up, purchase, publishing or account deletion. Never put passwords or keys in the report; check screenshots for secrets. On a login wall, CAPTCHA or permission prompt: stop and ask the human; do not work around it. Running a tool means it runs with your permissions: use a sandbox or a separate user. A fake `HOME` is not isolation: apps may still write to real app-support folders and system preferences, so list what changed outside your folder. Before evidence leaves the scratch folder, grep it for `token`, `cookie`, `.env` and key-shaped strings; move hits out and name them in the report.

## Common Mistakes

| Mistake | Fix |
|---|---|
| Scoring a feature from its README | State `Docs only`, no score, name the test |
| "Governance / UX" on one row | Split into two claims |
| Every row says "take" | Compare each against the baseline; say `Keep current method` when the baseline already covers it |
| Missing measurement shown as an average | Show `Not tested`, never a default number |
| UI control seen = enforcement works | A visible setting is `Docs only` for Security until the forbidden action is tried |
| One good run = reliable | Repeat critical tests; report the count |
