# AAA Skill Bundler

[![skills.sh](https://skills.sh/b/tomhuaijbig/aaa-skill-bundler)](https://skills.sh/tomhuaijbig/aaa-skill-bundler)

Organize your installed skills into clean `aa-*` bundle entries. Works with Codex and Claude Code.

## The Problem

Installing skills is easy. Using them is hard. After installing a bunch of skills, your list becomes a wall of English names. You forget what `metric-diagnostics` does. You can't remember if `figma-use` or `figma-generate-design` is the right one. You end up scrolling and guessing.

## The Fix

`aaa-skill-bundler` scans every installed skill, groups related ones by source and function, and generates lightweight `aa-*` bundle entries that sit at the top of your skill list. Each entry acts as a Chinese-friendly router — telling you what each child skill does, when to use it, and what trigger phrases work.

The actual work still happens through the original skills. The bundle just makes them findable.

When you run it, it asks whether you want descriptions translated to Chinese. If yes, it localizes grey/list descriptions while **keeping original titles untouched**. If no, it generates English-only bundles. No renaming, no deleting, no surprises.

## Quickstart

### skills.sh (recommended)

```bash
npx skills@latest add tomhuaijbig/aaa-skill-bundler
```

Pick the skills you want, choose your coding agent (Codex or Claude Code), and you're ready.

### Manual

```powershell
# Codex
Copy-Item -Recurse .\skills\aaa-skill-bundler "$env:USERPROFILE\.codex\skills\aaa-skill-bundler"

# Claude Code
Copy-Item -Recurse .\skills\aaa-skill-bundler "$env:USERPROFILE\.agents\skills\aaa-skill-bundler"
```

### Trigger It

```text
整理一下我的技能
```

```text
bundle my skills
```

---

## Skills

### `aaa-skill-bundler` — The Organizer

The main skill. Scans, groups, and generates `aa-*` bundle entries.

**Source**: [`skills/aaa-skill-bundler/SKILL.md`](./skills/aaa-skill-bundler/SKILL.md)

**What it does**:

- Scans `~/.codex/skills/`, plugin caches, and agent directories
- Groups skills by source, install time, and function
- Generates one `aa-*` entry per meaningful group
- Validates YAML, JSON, paths, and references after every change
- Preserves user-edited Chinese copy on updates

**Modes**:

| Mode | When | Trigger |
|------|------|---------|
| Post-install | Just installed new skills | `刚安装完技能` |
| Backfill | Skills installed earlier | `整理一下我的技能` |
| Localization | Translate only | `汉化技能说明` |

**Safety**:

- Asks before localizing
- Never deletes or renames original skills
- Never copies full skill bodies into bundles
- Never localizes titles by default

### `aaa-trial-hello` — Smoke Test

A minimal demo skill for verifying your skill pipeline works.

**Source**: [`skills/aaa-trial-hello/SKILL.md`](./skills/aaa-trial-hello/SKILL.md)

**Trigger**: `试用技能` / `trial skill` / `skill demo`

**Use it to**: confirm installation works, learn skill structure, test cross-platform compatibility.

**Platform**: Codex :check_mark: | Claude Code :check_mark:

---

## Platform Support

| Platform | Skill Directory | Notes |
|----------|----------------|-------|
| Codex | `~/.codex/skills/` | Full trigger support, all metadata |
| Claude Code | `~/.agents/skills/` | `SKILL.md` convention; `agents/openai.yaml` ignored |

---

## Reference

| File | What it is |
|------|-----------|
| [aaa-skill-bundler SKILL.md](./skills/aaa-skill-bundler/SKILL.md) | The organizer skill |
| [aaa-trial-hello SKILL.md](./skills/aaa-trial-hello/SKILL.md) | Smoke-test demo |
| [bundle-template.md](./skills/aaa-skill-bundler/references/bundle-template.md) | Template for generated bundles |
| [chinese-copy-rules.md](./skills/aaa-skill-bundler/references/chinese-copy-rules.md) | Rules for Chinese descriptions |
| [grouping-rules.md](./skills/aaa-skill-bundler/references/grouping-rules.md) | How skills get grouped |

---

## Why This Exists

> "The rate of feedback is your speed limit."
>
> David Thomas & Andrew Hunt, The Pragmatic Programmer

Good tools are useless if you can't find them. `aaa-skill-bundler` shortens the feedback loop between "I need a skill for this" and "I found the right one." It turns a wall of English entries into a clean, scannable index — optionally in Chinese.

No magic. No automation that renames your stuff. Just grouping, routing, and optional localization.

## License

MIT
