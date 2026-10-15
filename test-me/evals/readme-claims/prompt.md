---
name: readme-claims
tags: [trigger]
runs: 2
max_turns: 6
allowed_tools: [Read, Glob, Grep, Skill]
model: claude-sonnet-5-5
---
Our plan copies three features from an open-source agent framework, based on its README: per-call approval, a tamper-evident audit log, and network isolation. Before we build on them, how should we check that these features actually hold?
