# clova-minutes Installation Guide

`clova-minutes` is an Agent Skill for writing verifiable meeting minutes from Clova Note transcript files and markdown meeting-minutes templates.

This repository is distributed as a single skill package. Do not copy only `SKILL.md`. You must copy `references/` together with it.

## Installed Layout

After installation, the final directory layout must look like this:

```text
clova-minutes/
├── SKILL.md
└── references/
    ├── clova-note-format.md
    ├── request-examples.md
    └── verifiable-timestamps.md
```

`SKILL.md` refers to `references/...` using relative paths, so changing this layout may break the skill.

## Common Installation Rules

1. The default install target is the user's global skill directory.
2. Install into a project-local directory only when the user explicitly asks for a project-local installation.
3. Copy both `SKILL.md` and `references/` from this repository.
4. Create a `clova-minutes/` folder under the target agent's skill directory.
5. Copy `SKILL.md` and `references/` into that folder without changing their relative paths.
6. Reopen the agent or trigger skill rediscovery after installation.

The `~` notation below refers to the user's home directory. On Windows, this usually maps to `%USERPROFILE%`.

## Agent-Specific Skill Directories

| Agent | Project-local | User-global | Notes |
| --- | --- | --- | --- |
| Codex | `.agents/skills/clova-minutes/` | `~/.agents/skills/clova-minutes/` | Based on current public Codex docs |
| Claude Code | `.claude/skills/clova-minutes/` | `~/.claude/skills/clova-minutes/` | Uses the `SKILL.md` package format directly |
| Antigravity | `.agent/skills/clova-minutes/` | `~/.gemini/antigravity/skills/crmin/clova-minutes-skill/clova-minutes/` | Based on Agent Skills catalog conventions |
| OpenCode | `.opencode/skills/clova-minutes/` | `~/.config/opencode/skills/clova-minutes/` | Also compatible with `.claude/skills` and `.agents/skills` |

## Codex

### Recommended Paths

- Project-local: `.agents/skills/clova-minutes/`
- User-global: `~/.agents/skills/clova-minutes/`

### Prompt to Give Codex

```text
Install the `clova-minutes` skill by copying both `SKILL.md` and `references/` from the current repository.
Use `~/.agents/skills/clova-minutes/` as the default install path, and only use `.agents/skills/clova-minutes/` if the user explicitly requests a project-local installation.
After installation, confirm that these files exist:
- SKILL.md
- references/clova-note-format.md
- references/request-examples.md
- references/verifiable-timestamps.md
```

### Compatibility Note

Some Codex environments and helper tools still use `$CODEX_HOME/skills` or `~/.codex/skills`. If the current environment requires that layout, copy the same `clova-minutes/` directory structure there.

## Claude Code

### Recommended Paths

- Project-local: `.claude/skills/clova-minutes/`
- User-global: `~/.claude/skills/clova-minutes/`

### Prompt to Give Claude Code

```text
Install the `clova-minutes` skill by copying `SKILL.md` and `references/` from the current repository.
Use `~/.claude/skills/clova-minutes/` as the default install path, and only use `.claude/skills/clova-minutes/` if the user explicitly requests a project-local installation.
After installation, verify that the referenced files under `references/` were copied together with `SKILL.md`.
```

### Note

Claude Code's native subagent feature uses `.claude/agents/`, but this repository is distributed as a `SKILL.md` plus `references/` package, so this guide uses the skill path instead.

## Antigravity

### Recommended Paths

- Project-local: `.agent/skills/clova-minutes/`
- User-global: `~/.gemini/antigravity/skills/crmin/clova-minutes-skill/clova-minutes/`

### Prompt to Give Antigravity

```text
Install the `clova-minutes` skill using `SKILL.md` and `references/` from the current repository.
Use `~/.gemini/antigravity/skills/crmin/clova-minutes-skill/clova-minutes/` as the default install path, and only use `.agent/skills/clova-minutes/` if the user explicitly requests a project-local installation.
Keep the filename `SKILL.md` unchanged and copy the entire `references/` directory with it.
```

## OpenCode

### Recommended Paths

- Project-local: `.opencode/skills/clova-minutes/`
- User-global: `~/.config/opencode/skills/clova-minutes/`

### Prompt to Give OpenCode

```text
Install the `clova-minutes` skill by copying `SKILL.md` and `references/` from the current repository.
Use `~/.config/opencode/skills/clova-minutes/` as the default install path, and only use `.opencode/skills/clova-minutes/` if the user explicitly requests a project-local installation.
If the environment already uses global `.claude/skills/clova-minutes/` or `.agents/skills/clova-minutes/` compatibility paths, you may reuse that global path instead.
```

## Verification Example

After installation, any agent can be asked to verify the result with a prompt like this:

```text
Check whether the `clova-minutes` skill is installed, then show the install path and the list of bundled reference files.
```
