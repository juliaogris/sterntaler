---
name: meta
description: Create, review, and manage agents and commands
argument-hint: <new|review|list|md> [name] [--primer] [--all]
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
- `/meta md` — Update CLAUDE.md files (global or project).

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

List commands with their subcommands and usage patterns.

By default, show only user commands (`source: user` in frontmatter).
With `--all` or `-a`, include system commands.

For each command, read its file and extract the Usage section to show all
subcommands/invocation patterns. Format as a table:

```
┌─────────────────────┬────────────────────────────────────────┐
│ Command             │ Description                            │
├─────────────────────┼────────────────────────────────────────┤
│ /go                 │ Explore mode — write Go code           │
│ /go tidy            │ Reorganize file for readability        │
│ /go names           │ Review naming                          │
│ ...                 │ ...                                    │
└─────────────────────┴────────────────────────────────────────┘
```

**Convention:** Agents with dashes (e.g., `go-secure`) are subagents invoked
via the parent command (`/go secure`). Don't list them separately.

Also show which commands have primers.

---

## For `/meta md`

Update CLAUDE.md configuration files.

**Philosophy:** Ask questions before making changes. Challenge assumptions.
Help Julia discover what she actually needs, not just what she asked for.

1. Read current CLAUDE.md first:
   - `~/.claude/CLAUDE.md` (global)
   - `.claude/CLAUDE.md` (project, if in a project)
2. Ask clarifying questions:
   - "When would you NOT want this behavior?"
   - "Does this apply globally or just this project?"
   - "What problem are you actually solving?"
3. Propose changes with clear before/after
4. Get approval before editing

**Principles:**
- Keep instructions concise
- Group related instructions with clear headers
- Prefer specific, actionable instructions over vague preferences
- Consider edge cases and conflicts with existing rules
