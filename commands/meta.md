---
name: meta
description: Create, review, and manage agents and commands
argument-hint: <new|review|list> [name] [--primer] [--all]
allowed-tools: [Read, Write, Edit, Glob, Bash]
model: opus
source: user
enabled: true
---

## Usage

- `/meta new <name>` — Create a new agent and command pair.
- `/meta new <name> --primer` — Also create a primer file.
- `/meta review <name>` — Review agent, command, and primer for consistency.
- `/meta list` — List user agents and commands.
- `/meta list --all` — Include system agents and commands.

---

## On Starting

Read the primer first:

1. Read `~/.claude/primer/meta.md` — guidance on creating agents/commands

---

## For `/meta new <name>`

1. Read the primer to understand structure and conventions.
2. Ask key questions:
   - What is this agent for? (one sentence)
   - What tools does it need?
   - What model should it use? (opus, sonnet, inherit)
   - Any special behavior or personality?
3. Draft the agent file and command file.
4. Show Julia both files for review before writing.
5. If `--primer` flag, also create a stub primer file.

Keep files short. Avoid fluff. Match existing style.

---

## For `/meta review <name>`

1. Read these files (if they exist):
   - `~/.claude/agents/<name>.md`
   - `~/.claude/commands/<name>.md`
   - `~/.claude/primer/<name>.md`
2. Check for:
   - Consistency in language and structure
   - Clarity of purpose
   - Unnecessary verbosity (trim it)
   - Missing essential information
   - Alignment between agent and command
3. Propose specific edits with reasoning.
4. Ask Julia before making changes.

---

## For `/meta list`

List agents and commands with a brief summary.

By default, show only user agents (`source: user` in frontmatter).
With `--all` or `-a`, include system agents (no source field).

Check:
- `~/.claude/agents/*.md`
- `~/.claude/commands/*.md` (files only, not directories)
- `~/.claude/primer/*.md`

Show which have matching pairs (agent + command) and which have primers.
