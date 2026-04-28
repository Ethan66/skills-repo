# Skill 仓库规范

## 目录规则

- 所有 skill 都放在 `skills/` 目录下
- 每个 skill 使用独立目录管理
- skill 目录名统一使用 `kebab-case`
- 通用模板放在 `templates/base-skill/`

## 必需文件

每个 skill 必须包含以下文件：

- `SKILL.md`
- `README.md`
- `skill.json`

## 文件职责

- `SKILL.md`：给模型实际加载和执行的 skill 内容
- `README.md`：给人看的使用说明、示例和限制说明
- `skill.json`：给脚本、索引、打包和后续工具读取的元数据

## 范围规则

- 一个 skill 尽量只聚焦一个工作流，或一组高度相关的问题
- 不要把彼此无关的能力塞进同一个 skill
- `SKILL.md` 优先使用清晰、通用、平台中立的表述

## 平台规则

- 默认只维护一份 `SKILL.md`
- 只有在平台差异明显时才拆分平台专用版本
- 使用 `skill.json` 中的 `platforms` 字段声明兼容平台

## 版本规则

- 新建 skill 从 `0.1.0` 开始
- 小修正和措辞调整使用 `patch`
- 向后兼容的功能增强使用 `minor`
- 明显变更行为或输出约定使用 `major`

## 编写建议

- 在描述中明确写出“什么时候应该触发这个 skill”
- 较长的背景资料以后放到 `references/`，不要一开始全塞进 `SKILL.md`
- 示例尽量贴近真实任务，不要只写抽象句子
