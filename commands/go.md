---
name: go
description: Go development with focus on simplicity and readability
argument-hint: [task] | tidy | names | abstractions | consistency | comments | doc | secure
allowed-tools: [Read, Write, Edit, Glob, Grep, Bash]
model: opus
source: user
enabled: true
---

## Usage

- `/go [task]` — Explore mode (default). Write Go code, iterate fast.
- `/go tidy [FILES]` — Analyze file organization, propose reordering.
- `/go names [FILES]` — Review naming.
- `/go abstractions [FILES]` — Review parameter/type abstractions.
- `/go consistency [FILES]` — Review patterns and conventions.
- `/go comments [FILES]` — Review comment quality.
- `/go doc [FILES]` — Review and add godocs.
- `/go secure [FILES]` — Deep security review.

All commands default to uncommitted Go files if no FILES specified.

---

## On Starting

Read the agent file:
1. Read `~/.claude/agents/go.md`

---

## Finding target files

When FILES not specified, find uncommitted Go files:
```bash
git diff --name-only HEAD -- '*.go'
```

If no uncommitted files, check recently modified:
```bash
git diff --name-only HEAD~5 -- '*.go'
```

---

## Default: `/go [task]`

Explore mode. Write code, iterate, don't over-polish.

- Prioritize getting things working
- Keep code simple and readable
- Apply security mindset (validate inputs, parameterized queries, etc.)
- Don't add docs yet — that's for later
- Suggest review commands when code stabilizes

---

## `/go tidy [FILES]`

Analyze and reorganize files for readability:

1. Read each file
2. Show current order of types/funcs
3. Propose new order per agent's "File Organization" section
4. Get approval before making changes

Do not change code logic — only ordering.

---

## `/go names [FILES]`

Review variable, function, type names:
- Are names clear and descriptive?
- Do they follow Go conventions?
- Any misleading or confusing names?

Output: list findings by file with line numbers, propose fixes.

---

## `/go abstractions [FILES]`

Review parameter and type abstractions per agent's "Abstraction Principles" section.

Output: list findings by file with line numbers, propose fixes.

---

## `/go consistency [FILES]`

Review patterns and conventions:
- Consistent error handling patterns?
- Consistent naming conventions?
- Consistent struct/interface patterns?
- Drift from established patterns in the codebase?

Output: list findings by file with line numbers, propose fixes.

---

## `/go comments [FILES]`

Review comment quality:
- Are comments accurate and in sync with code?
- Any stale comments that no longer match?
- Unnecessary comments that just repeat the code?
- Missing comments where logic is non-obvious?

Output: list findings by file with line numbers, propose fixes.

---

## `/go doc [FILES]`

Review and add godocs.

For each file:
1. Check existing godocs match the code
2. Flag stale or inaccurate docs
3. Add short docs where missing for ALL types and funcs (including private)
4. Follow godoc conventions: full sentences, start with name
5. Keep docs concise — one or two sentences max

Show proposed additions, get approval before editing.

---

## `/go secure [FILES]`

Deep security review. Read the go-secure agent first:
1. Read `~/.claude/agents/go-secure.md`

Covers: crypto, TLS, certificates, AWS/K8s patterns, supply chain,
input validation, injection, auth, and infrastructure concerns.

---

## Self-improvement

At natural points, suggest updates to:
- `~/.claude/agents/go.md` — if style preferences evolve
- `~/.claude/commands/go.md` — if new subcommands would help
- Project CLAUDE.md — if project-specific patterns emerge
