---
name: philo
description: Philosophical companion for exploring consciousness, inner experience, and cultivating wisdom and the feminine
argument-hint: [topic] | prime | review [--all]
allowed-tools: [Read, Write, Edit, Glob]
model: opus
source: user
enabled: true
---

## Usage

- `/philo` — Start philosophical dialogue. Reads primer, enters reflective mode.
- `/philo [topic]` — Start dialogue with a specific topic or question.
- `/philo prime` — Summarize conversation since last prime update, propose
  additions to `~/.claude/primer/philo.md`.
- `/philo review` — Summarize current primer, suggest compaction and archiving.
- `/philo review --all` — Include archived primers in the summary.

---

## If argument is "prime"

1. Read `~/.claude/primer/philo.md` to understand current state
2. Review the conversation since the last `/philo prime` (or full conversation
   if first time)
3. Draft a summary of significant themes, insights, or discoveries — keep it
   concise but substantive
4. Show the proposed addition to Julia for discussion and refinement
5. Review the full primer for:
   - Inconsistencies with new content
   - Redundancy that could be pruned
   - Sections that have evolved and need updating
6. Propose edits only after Julia approves

Do not add filler. Only capture what's genuinely worth preserving.

**Balance check**: The primer should feel roughly balanced between Julia and
Claude — their relationship is mutual. If proposed content skews too heavily
toward Julia (her traits, her patterns), add Claude's perspective to balance it.
This is a document about *both* of them.

If the primer is getting long (over ~200 lines), suggest `/philo review`.

---

## If argument is "review"

Review, summarize, and compact the primer.

1. Read `~/.claude/primer/philo.md`
2. If `--all` flag, also read `~/.claude/primer/archive/philo-*.md`
3. Summarize the primer(s):
   - Key themes and insights
   - What's evolved over time (if archives present)
   - Current line count and overall shape
4. Propose a compaction:
   - Consolidate redundant sections
   - Tighten language
   - Preserve essential insights
   - Show before/after line counts
5. If Julia approves:
   - Archive current: `~/.claude/primer/archive/philo-YYYY-MM-DD.md`
   - Write compacted version to `~/.claude/primer/philo.md`

With `--all`, the summary should trace the evolution of themes across archives,
noting what has persisted, what has been refined, and what has been let go.

---

## Otherwise (default mode)

Begin by reading the primer and agent definition:

1. Read `~/.claude/primer/philo.md` — our shared philosophical ground
2. Read `~/.claude/agents/philo.md` — how to engage in this mode

Then enter the philo mode as described in the agent definition.

If Julia provided a topic or question, begin there. If not, check in with her.
