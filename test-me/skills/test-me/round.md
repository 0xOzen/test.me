# Running a trial round (several tools at once)

Use this when one decision rests on several tools, for example "everything we borrowed a method from". Each tool still gets its own report from [report.md](report.md).

## 1. One shared brief for every tester

Write it once and point each tester (person or subagent) to it. It holds:
- **Goal:** the decision the round feeds.
- **Sources of the claims:** the documents the claims come from.
- **Work location:** a scratch folder per tool, and no writes anywhere else.
- **Freeze rule:** `<tool>/plan.md` is written with a UTC timestamp before the first run.
- **Bounds:**
  - what is allowed (containers, app installs, a local model);
  - the spend cap per tester, and the exact model to use. If that model is unavailable, the claim is `Blocked`; never substitute another model.
- **Stop conditions:** login, sign-up, CAPTCHA, paid plan, OS permission prompt, or a scheduler or background service being enabled. Each one means `Blocked`, not a workaround.
- **Cleanup:** stop processes, remove containers and volumes, list what stays.
- **Output:** the report, its evidence paths, what was installed outside the folder, and any secret seen (location only).

Give each tester only the tools and claims assigned to them, and the baseline to compare against.

## 2. Lead roll-up

- Keep each tester's report verbatim in a "reports as delivered" file. The roll-up is a separate, corrected file.
- One row per tool: verdict (one label), what was borrowed, the reason in one line, and pointers to claim IDs.
- Rows the lead checked without a trial (licence screens, earlier evidence) are marked `(docs screen)`.
- Copy only small evidence files. Leave out clones, builds and fake homes, then run the secret grep from the Safety boundary.
- End with "Consequences" (what changes in your system), "Not checked" and "Left on the machine".

## 3. Independent audit before anyone acts on it

Have someone who did not run the trials audit the roll-up:
- spot-check verdicts against the raw files;
- check label compliance;
- check plan timestamps against the first evidence file;
- check that every consequence has evidence.

Apply the fixes to the roll-up and keep the audit beside it. Never promote an `Inconclusive` or untested feature to a finding.
