# Skill 仓库初始化实施计划

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 初始化一个轻量的多 skill 仓库结构，包含共享模板和仓库级规范。

**Architecture:** 建立一个小而清晰的仓库骨架，先明确目录职责和文件边界。当前不引入运行时工具，只覆盖编写和组织 skill 所需的最小文件集合。

**Tech Stack:** Markdown, JSON, Git

---

### Task 1: 创建仓库文档

**Files:**
- Create: `README.md`
- Create: `docs/conventions.md`
- Create: `docs/superpowers/specs/2026-04-28-skill-repo-design.md`

- [ ] **Step 1: 编写仓库说明**

创建 `README.md`，简要说明仓库用途、目录结构和初始使用方法。

- [ ] **Step 2: 编写仓库规范**

创建 `docs/conventions.md`，定义命名规则、必需文件、范围约束和版本规则。

- [ ] **Step 3: 记录已确认设计**

创建 `docs/superpowers/specs/2026-04-28-skill-repo-design.md`，记录仓库结构和暂缓项。

### Task 2: 创建基础模板

**Files:**
- Create: `templates/base-skill/SKILL.md`
- Create: `templates/base-skill/README.md`
- Create: `templates/base-skill/skill.json`

- [ ] **Step 1: 添加 skill 指令模板**

创建 `templates/base-skill/SKILL.md`，提供 frontmatter、触发说明和工作流占位结构。

- [ ] **Step 2: 添加说明文档模板**

创建 `templates/base-skill/README.md`，包含用途、使用场景、输入、输出、备注和示例。

- [ ] **Step 3: 添加元数据模板**

创建 `templates/base-skill/skill.json`，包含名称、版本、描述、入口、平台、标签和私有标记。

### Task 3: 创建可扩展目录

**Files:**
- Create: `skills/.gitkeep`
- Create: `dist/.gitkeep`
- Create: `docs/superpowers/plans/2026-04-28-skill-repo-bootstrap.md`

- [ ] **Step 1: 保留空的 skills 目录**

创建 `skills/.gitkeep`，确保在还没有真实 skill 时目录也能保留。

- [ ] **Step 2: 保留空的 dist 目录**

创建 `dist/.gitkeep`，为未来打包产物预留固定目录。

- [ ] **Step 3: 保存本实施计划**

创建 `docs/superpowers/plans/2026-04-28-skill-repo-bootstrap.md`，作为本次初始化的实施记录。
