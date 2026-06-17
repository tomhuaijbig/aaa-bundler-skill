---
name: aaa-trial-hello
description: A trial/demo skill for learning how Codex skills work. Simple hello-world style skill that prints a greeting and explains skill fundamentals. Use when the user wants to test skill installation, learn skill structure, or verify Codex skill loading.
---

# AAA Trial Hello — Codex Skill Demo

This is a trial skill for demonstrating how Codex skills are structured, installed, and triggered.

It serves as both a **smoke test** (can you install and trigger a skill successfully?) and a **learning reference** (what sections does a real skill have?).

This skill does not perform complex operations. It is intentionally minimal so new users or developers can verify their skill pipeline end to end.

## Expected Behavior

When triggered, this skill will:

1. Confirm that it was loaded correctly by Codex.
2. List the key parts of its own structure so you can use it as a reference.
3. Suggest next steps for learning about Codex skills (such as reading `skill-installer`, `skill-creator`, or `write-a-skill`).

## Skill Structure Reference

Every Codex skill has:

- **Skill folder**: a directory under `~/.codex/skills/` or a plugin cache.
- **SKILL.md**: the main file containing frontmatter (`name`, `description`, `disable-model-invocation`) and body (trigger logic, workflow, rules).
- **References** (optional): `references/` folder with supporting docs.
- **Scripts** (optional): `scripts/` folder with executable helpers.
- **Agent config** (optional): `agents/openai.yaml` for UI metadata.

## Trigger Phrases

- 试用技能 / trial skill / hello skill
- 测试技能加载 / test skill loading
- skill demo / 技能演示
- Codex 技能结构 / skill structure

## Source

This is an example skill included for demonstration and learning. Feel free to modify it, fork it, or delete it after testing.

## Notes

- This skill does not have side effects. It only reads its own structure and reports back.
- You can rename, copy, or extend this skill to create your own custom skills.
