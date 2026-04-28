# Skill 仓库

这个仓库用于统一管理你自己的自定义 skill。

## 目录结构

- `skills/`：存放你实际编写的 skill
- `templates/base-skill/`：基础模板，新建skill的时候，复制一份，然后修改，这样可以保证统一格式
- `docs/`：仓库规范、设计说明和后续文档
- `dist/`：后续打包产物输出目录

## 当前范围

当前采用轻量的“1.5 版”结构：

- 每个 skill 都有自己的独立目录
- 每个 skill 至少包含 `SKILL.md`、`README.md`、`skill.json`
- 仓库统一规范写在 `docs/conventions.md`

## 使用方式

1. 将 `templates/base-skill/` 复制到 `skills/<你的-skill-名称>/`
2. 修改 `skill.json` 中的元数据
3. 按需填写 `SKILL.md` 和 `README.md`
