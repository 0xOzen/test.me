# Module: skills

This folder is the `aequai-skills` plugin marketplace: agent skills from AequAI for everyday work with AI. It is the root of the public repository, so everything here is meant to be published.

| Plugin | Version | Evals |
|---|---|---|
| `test-me` | 1.0.0 | `test-me/evals/` (trigger cases) |

Checks before each release:
- `claude plugin validate .` passes.
- `claude plugin eval ./<plugin> --ablation none` passes.
- No personal paths or secrets are in the folder.
- Every README claim is backed by evidence.

`site/` is the static page for skills.aequai.com (Cloudflare Pages project `aequai-skills`).

The owner unit's task list tracks publishing.
