---
name: review
description: Code review for branches, commits, and PRs
argument-hint: [COMMIT-HASH | PR-NUMBER]
allowed-tools: [Read, Write, Edit, Glob, Grep, Bash]
model: opus
source: user
enabled: true
---

## Usage

- `/review` — Review current branch (uncommitted + committed changes vs base).
- `/review COMMIT-HASH` — Review a specific commit.
- `/review PR-NUMBER` — Review a pull request.

---

## On Starting

Read the agent file:
1. Read `~/.claude/agents/review.md`

---

## Default: `/review`

Review the current branch against its base.

1. Find the base branch:
   ```bash
   git merge-base HEAD main || git merge-base HEAD master
   ```

2. Get all changes (committed and uncommitted):
   ```bash
   git diff $(git merge-base HEAD main) HEAD
   git diff HEAD  # uncommitted changes
   ```

3. Read the changed files for full context

4. Review following the agent guidelines

---

## `/review COMMIT-HASH`

Review a specific commit.

1. Get the commit info:
   ```bash
   git show --stat COMMIT-HASH
   git show COMMIT-HASH
   ```

2. Read the changed files for context

3. Review following the agent guidelines

---

## `/review PR-NUMBER`

Review a pull request.

1. Fetch PR info:
   ```bash
   gh pr view PR-NUMBER --json title,body,headRefName,baseRefName,comments,reviews
   ```

2. Checkout the PR branch:
   ```bash
   gh pr checkout PR-NUMBER
   ```

3. Get the diff against base:
   ```bash
   gh pr diff PR-NUMBER
   ```

4. **Start with context**: Before diving into code, explain:
   - What this PR does (from title, description, and code)
   - How it fits into the wider repo context
   - Any concerns or questions from existing comments

5. Read changed files for full context

6. Review following the agent guidelines

7. Consider existing review comments — don't duplicate, build on them

8. **Write review to file**:
   - Create `.claude/review/` directory if needed
   - Write to `.claude/review/PR-NUMBER-BRANCH.md` (replace `/` in branch name with `-`)
   - Every comment must reference `FILE:LINENUM`

---

## Output

Structure per agent's "Output Format" section.

**Every issue must include `file:line`** — no floating comments without location.

For PR reviews, output goes to `.claude/review/PR-NUMBER-BRANCH.md`.
