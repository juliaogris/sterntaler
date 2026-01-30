# Meta Primer: Creating Agents and Commands

This document captures what works well when creating agents and commands.

---

## Structure Overview

Three types of files work together:

- **Commands** (`~/.claude/commands/NAME.md`): Entry point for `/name`. Defines
  usage modes, what to read on start, and instructions per mode.
- **Agents** (`~/.claude/agents/NAME.md`): Persona and behavior. Who Claude
  becomes when this agent is active.
- **Primers** (`~/.claude/primer/NAME.md`): Optional. Accumulated knowledge,
  context, or guidance. Living documents that evolve.

---

## Command File Structure

```yaml
---
name: example
description: One sentence about what this does
argument-hint: [optional args description]
allowed-tools: [Read, Write, Edit, Glob]
model: opus
source: user
enabled: true
---
```

After frontmatter:
- **Usage**: List all invocation patterns
- **On Starting**: What to read before doing anything
- **Per-mode sections**: Clear instructions for each subcommand/mode

Keep it short. Tell Claude what to do, not how to think.

---

## Agent File Structure

```yaml
---
name: example
description: When to use this agent (one sentence, can include examples)
model: opus
color: blue
source: user
---
```

The `source` field distinguishes user-created agents from system agents:
- `source: user` — your agents
- No source field — system/bundled agents

After frontmatter:
- Brief intro of who/what this agent is
- **Core principles** or approach
- **Specific behaviors** for different situations
- **Style notes** if relevant

Write in second person: "You are..." or "You help..."

Avoid "comprehensive", "robust", "powerful", etc.

---

## Primer File Structure

No frontmatter needed. Use markdown headers.

- Start with a brief purpose statement
- Organize by topic or theme
- Keep entries substantive but concise
- Update when significant insights emerge

Primers are optional. Only create when there's accumulated knowledge worth
preserving between sessions.

---

## Consistency Checklist

When creating or reviewing:

- [ ] Command and agent names match
- [ ] Descriptions are short (one sentence ideal)
- [ ] No marketing language
- [ ] Tool list is minimal (only what's needed)
- [ ] Instructions are actionable, not philosophical
- [ ] Formatting matches existing files
- [ ] No redundant information between command and agent

---

## Common Patterns

**Simple utility agent**: Short agent file, command file defines modes.
See: make, docker

**Dialogue agent**: Longer agent file with personality, command file handles
modes like "prime". See: philo

**Review/analysis agent**: Focus on process steps and output format.
See: code-reviewer

---

## What to Ask When Creating

1. What's the single purpose? (If you can't say it in one sentence, split it)
2. What tools are actually needed?
3. What model? (opus for complex reasoning, inherit for simple tasks)
4. Is a primer needed? (Only if knowledge accumulates between sessions)
5. What are the distinct modes of use?

---

## Notes

- Simpler is better. Start minimal, add only when needed.
- Read existing agents before creating new ones — match the style.
- Command files instruct. Agent files embody. Primers remember.
