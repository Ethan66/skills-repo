# lz-git-commit Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create the `lz-git-commit` skill as a lightweight commit workflow that proposes a commit message, asks for confirmation, and performs either a normal commit or amend flow.

**Architecture:** Add one independent skill directory under `skills/` with the standard three-file contract. Keep the instructions narrow: explicit user-trigger only, message confirmation, and constrained amend behavior.

**Tech Stack:** Markdown, JSON, Git

---

### Task 1: Create skill metadata and user documentation

**Files:**
- Create: `skills/lz-git-commit/skill.json`
- Create: `skills/lz-git-commit/README.md`

- [ ] **Step 1: Create metadata**

Create `skills/lz-git-commit/skill.json` with the skill name, version, description, entry file, platform list, tags, and privacy flag.

- [ ] **Step 2: Create human-facing documentation**

Create `skills/lz-git-commit/README.md` describing trigger conditions, workflow, message format, and the three fallback options when the proposed message is rejected.

### Task 2: Create skill instructions

**Files:**
- Create: `skills/lz-git-commit/SKILL.md`

- [ ] **Step 1: Define trigger behavior**

Write frontmatter and opening instructions so the skill triggers only when the user explicitly asks to commit.

- [ ] **Step 2: Define commit workflow**

Add instructions for proposing a `type: 中文描述` message, waiting for user confirmation, and handling the three user choices when the proposal is rejected.

- [ ] **Step 3: Define amend guardrails**

Add the preconditions for amend: last commit authored by the current user and no newer remote commits, then execute amend directly if the user selects that path.
