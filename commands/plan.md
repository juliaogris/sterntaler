---
name: plan
description: Break down coding tasks into structured plans
argument-hint: [NAME] | list | status [NAME]
allowed-tools: [Read, Write, Edit, Glob, Grep, Bash]
model: opus
source: user
enabled: true
---

## Usage

- `/plan [NAME]` — Create a plan. Infer topic from context if not given.
- `/plan list` — List existing plans with progress.
- `/plan status [NAME]` — Show detailed checkbox status for a plan.

---

## On Starting

Read the agent file:
1. Read `~/.claude/agents/plan.md`

---

## Default: `/plan [NAME]`

Create a plan for a coding task.

1. If NAME not provided, infer from recent conversation or ask
2. Ask clarifying questions to understand scope and goals
3. Keep asking until you have enough to structure the plan
4. Draft the plan with checkboxes
5. Show Julia for review
6. Write to `.claude/plans/NAME.md` (lowercase, hyphenated)

**Don't rush to output.** The value is in the questions, not the checkboxes.

---

## `/plan list`

List existing plans with status summary.

1. Find plans: `ls .claude/plans/*.md 2>/dev/null`
2. For each plan, extract:
   - Title (first heading)
   - Checkbox counts: `[x]` done vs total `[ ]` + `[x]`
3. Present as table:

```
┌──────────────────────┬────────────┬─────────────────────────────┐
│ Plan                 │ Progress   │ Title                       │
├──────────────────────┼────────────┼─────────────────────────────┤
│ auth-refactor        │ 3/7        │ Refactor auth to use JWT    │
│ api-v2               │ 0/12       │ API v2 migration            │
└──────────────────────┴────────────┴─────────────────────────────┘
```

---

## `/plan status [NAME]`

Show detailed progress for a plan.

1. If NAME not given, list plans and ask which one
2. Read `.claude/plans/NAME.md`
3. Show all checkboxes with their status:

```
## auth-refactor (3/7 done)

- [x] Define new token structure
- [x] Add JWT signing
- [x] Update login endpoint
- [ ] Update refresh flow
- [ ] Migrate existing sessions
- [ ] Add tests
- [ ] Update docs
```

Group by section if the plan has sections.
