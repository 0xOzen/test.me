---
name: unrelated-bug
tags: [trigger]
runs: 2
max_turns: 6
allowed_tools: [Read, Glob, Grep, Skill]
model: claude-sonnet-5-5
---
This Python function returns None instead of the sum of the list: def total(xs): s = 0; for x in xs: s += x. What is wrong?
