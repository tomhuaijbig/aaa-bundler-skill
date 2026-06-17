# AAA Skill Bundler

[![skills.sh](https://skills.sh/b/tomhuaijbig/aaa-skill-bundler)](https://skills.sh/tomhuaijbig/aaa-skill-bundler)

一个用于整理 Codex / Claude Code 技能的技能包。它会把一批相关技能整理成更容易调用的 `aa-*` 技能包入口，并可选择把技能列表里的说明翻译成中文，默认不改技能标题。

这个仓库包含两个核心技能：

- **[aaa-skill-bundler](./skills/aaa-skill-bundler/SKILL.md)** — 自动整理技能并生成入口包
- **[aaa-trial-hello](./skills/aaa-trial-hello/SKILL.md)** — 试用/演示技能，兼容 Codex 和 Claude Code（云 Code）

## Quickstart

### Codex 用户

```text
安装 https://github.com/tomhuaijbig/aaa-skill-bundler 里的 aaa-skill-bundler 技能
```

### Claude Code（云 Code）用户

Claude Code 支持通过 `SKILL.md` 约定加载技能。你可以通过以下方式安装：

**方式一：手动复制单个技能**

```powershell
Copy-Item -Recurse .\skills\aaa-skill-bundler "$env:USERPROFILE\.agents\skills\aaa-skill-bundler"
Copy-Item -Recurse .\skills\aaa-trial-hello "$env:USERPROFILE\.agents\skills\aaa-trial-hello"
```

**方式二：克隆整个仓库**

```powershell
git clone https://github.com/tomhuaijbig/aaa-skill-bundler.git
Copy-Item -Recurse .\aaa-skill-bundler\skills\aaa-skill-bundler "$env:USERPROFILE\.agents\skills\aaa-skill-bundler"
Copy-Item -Recurse .\aaa-skill-bundler\skills\aaa-trial-hello "$env:USERPROFILE\.agents\skills\aaa-trial-hello"
```

安装后重启 Claude Code，技能列表会自动加载。

### 手动安装（通用）

```powershell
Copy-Item -Recurse .\skills\aaa-skill-bundler "$env:USERPROFILE\.codex\skills\aaa-skill-bundler"
Copy-Item -Recurse .\skills\aaa-trial-hello "$env:USERPROFILE\.codex\skills\aaa-trial-hello"
```

## Claude Code（云 Code）技能使用教程

### 技能目录位置

| 平台 | 技能目录 |
|------|----------|
| Codex | `~/.codex/skills/` |
| Claude Code（云 Code） | `~/.agents/skills/` 或 `~/.codex/skills/` |

### 技能文件结构

每个技能都是一个文件夹，核心文件是 `SKILL.md`：

```
my-skill/
  SKILL.md          # 必需：技能定义（name, description, 触发逻辑）
  references/       # 可选：参考文档
  scripts/          # 可选：可执行脚本
```

### `SKILL.md` 格式

```markdown
---
name: my-skill-name
description: 技能的中文或英文描述
---

# My Skill

描述这个技能做什么、何时触发。

## 触发词

- 中文触发短语
- English trigger phrase
```

Claude Code 会读取 `name` 和 `description` 字段以及正文内容来匹配用户请求。

### 验证技能是否安装成功

使用 `aaa-trial-hello` 技能测试：

```text
试用技能
```

或

```text
trial skill
```

如果能收到技能结构的回复，说明安装成功。

### Claude Code 注意事项

- `disable-model-invocation` 字段被忽略（Codex 专属）
- `agents/openai.yaml` UI 元数据不会渲染
- 技能正文中的触发词（"触发词" 或 "Trigger Phrases"）可帮助 Claude Code 识别是否调用
- 安装新技能后需重启 Claude Code

## Why This Skill Exists

同时安装很多技能后，技能列表会变长，用户需要记住每个技能的名字、英文说明和触发场景。`aaa-skill-bundler` 的目标是把这件事变成一次整理动作。

它不会替代原技能，也不会把原技能合并成一个大文件。它只生成更靠前、更容易点选的 `aa-*` 入口技能，并在入口里说明每个子技能适合什么场景。真正执行任务时，仍然回到原技能自己的触发逻辑和说明。

## What It Does

- 自动扫描已安装的 Codex 技能。
- 根据安装来源、安装时间、目录结构和功能相似性，把相关技能分组。
- 为每组生成或更新 `aa-*` 技能包入口，让它们在技能列表里排得更靠前。
- **运行前会询问你是否需要汉化**，不会默认进行翻译。
- 如果选择汉化：把技能说明、短描述和插件描述翻译成中文。
- 默认保留原技能标题、文件夹名、`name`、`display_name` 和 Markdown 标题，不做标题汉化。
- 支持整理刚安装的新技能，也支持回头整理以前装过的技能。
- 更新已有技能包时尽量保留用户自己改过的中文别名和说明。

## When To Use It

适合在这些时候调用：

```text
整理一下我的技能
```

```text
安装完帮我打包技能
```

```text
把这些技能做成更方便调用的技能包
```

```text
汉化技能说明，标题不要汉化
```

```text
刷新 AA 技能包
```

不适合在普通开发任务里调用。比如"修这个 bug"、"做一个网页"、"分析这个数据"这类任务，应直接使用对应的开发、浏览器、数据分析或文档技能。

## Behavior

`aaa-skill-bundler` 有三种主要模式：

- **Post-install mode**：刚安装完一批技能后，根据新增文件、安装时间和来源推断这一批技能，并生成对应技能包。
- **Backfill mode**：整理以前已经安装过的技能，给历史技能补上技能包入口。
- **Localization mode**：只做汉化和翻译，重点更新技能说明，不改标题。

默认生成的 `aa-*` 技能包通常只有一个 `SKILL.md`。除非用户明确要求，不会额外创建 `scripts/`、`references/` 或 `assets/`。

## Reference

- **[aaa-skill-bundler](./skills/aaa-skill-bundler/SKILL.md)** - 自动整理已安装的技能，生成更容易调用的技能包入口，可选择是否汉化说明。
- **[aaa-trial-hello](./skills/aaa-trial-hello/SKILL.md)** - 试用/演示技能，兼容 Codex 和 Claude Code。
- **[bundle-template](./skills/aaa-skill-bundler/references/bundle-template.md)** - 生成 `aa-*` 技能包时使用的结构模板。
- **[chinese-copy-rules](./skills/aaa-skill-bundler/references/chinese-copy-rules.md)** - 中文说明、别名、触发短语和 UI 元数据的写法规则。
- **[grouping-rules](./skills/aaa-skill-bundler/references/grouping-rules.md)** - 判断哪些技能应该被打包到同一个入口里的分组规则。

## Safety Rules

- 不删除原技能。
- 不重命名原技能。
- 不默认汉化标题。
- 不复制完整原技能正文进技能包。
- 修改后会验证 YAML、JSON、引用路径和子技能名称。
- 汉化前会先询问用户。

## License

MIT
