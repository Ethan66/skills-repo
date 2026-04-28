# lz-frontend-code-standards Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create the `lz-frontend-code-standards` skill with clear trigger conditions, implementation rules, and human-readable documentation.

**Architecture:** Add one new skill directory under `skills/` using the repository's three-file contract. Keep the content focused on trigger rules, implementation boundaries, concrete frontend coding standards, and lightweight execution checks.

**Tech Stack:** Markdown, JSON

---

### Task 1: Create skill metadata and documentation

**Files:**
- Create: `skills/lz-frontend-code-standards/skill.json`
- Create: `skills/lz-frontend-code-standards/README.md`

- [ ] **Step 1: Create metadata**

Create `skills/lz-frontend-code-standards/skill.json` with the skill name, version, description, entry file, platform list, tags, and privacy flag.

- [ ] **Step 2: Create human-facing documentation**

Create `skills/lz-frontend-code-standards/README.md` describing purpose, trigger scenarios, scope boundaries, covered standards, and usage examples.

### Task 2: Create skill instructions

**Files:**
- Create: `skills/lz-frontend-code-standards/SKILL.md`

- [ ] **Step 1: Define trigger behavior**

Write the frontmatter and opening section so the skill triggers only during frontend implementation tasks involving Vue, JavaScript, or TypeScript code changes.

- [ ] **Step 2: Define implementation rules**

Add sections for project-style detection, modified-code-only enforcement, JS/TS standards, Vue standards, `<script setup>` order, hooks/composables split rules, and review-friendly coding rules.

- [ ] **Step 3: Add execution checklists**

Add a pre-coding checklist and a pre-submit self-check so the skill behaves like a lightweight implementation guard rather than a passive style guide.
