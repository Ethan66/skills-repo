---
name: lz-git-commit
description: 在用户显式使用 `$lz-git-commit`，或明确要求提交时使用。触发后直接开始 git 提交流程：生成 commit message、展示四个选项，并在用户选择后执行提交。如果用户不接受建议 message，还要支持基于建议 message 修改、复用上一个 commit message，或在满足条件时直接合并到上一个 commit。不要在任务只是看起来完成时自动触发。
---

# 目的

这个 skill 用于处理用户主动发起的 git 提交流程。它不负责代码质量判断和提交拆分策略，只负责生成 message、让用户确认，并执行正常提交或 amend。

## 何时使用

以下两种情况都应该触发：

1. 用户显式使用 `$lz-git-commit`
2. 用户明确要求提交，例如：

- 帮我提交
- 帮我 commit
- 提交这些改动
- 用合适的 message 提交

以下情况不要触发：

- 任务只是看起来已经做完
- 用户只是讨论 commit 风格
- 用户只是查看 git 状态

## 执行原则

1. 不因为任务看起来完成就自动提交。
2. 如果用户显式使用 `$lz-git-commit`，直接开始提交流程，不再要求用户补充“提交当前改动”之类的意图语句。
3. 先生成建议的 commit message，再让用户选择后续动作。
4. commit message 格式统一为 `type: 中文描述`。
5. 不默认运行 lint、test 或其他检查。
6. 不分析改动质量，不判断无关改动，不判断是否应该拆分多个提交。

## Commit Message 规范

- 使用 `type: 中文描述`
- `type` 优先使用以下类型：
  - `feat`
  - `fix`
  - `refactor`
  - `docs`
  - `style`
  - `test`
  - `chore`
- 中文描述应简洁、明确，直接概括本次改动

## 正常提交流程

1. 用户显式使用 `$lz-git-commit`，或明确要求提交时触发
2. 读取当前改动，生成一条建议的 commit message
3. 先把建议 message 展示给用户
4. 然后明确给出以下四个选项，让用户选择下一步：
   - 直接使用当前建议 message 提交
   - 基于当前建议 message 修改后提交
   - 使用上一个 commit message 提交
   - 合并到上一个 commit
5. 只有用户做出选择后，才执行对应的提交动作

## 选项处理

在展示建议 message 后，必须提供以下四个选项：

1. 直接使用当前建议 message 提交
2. 基于当前建议 message 修改后提交
3. 使用上一个 commit message 提交
4. 合并到上一个 commit

### 选项 1：直接使用当前建议 message 提交

- 使用当前自动生成的建议 message 执行提交

### 选项 2：基于当前建议 message 修改后提交

- 用户自定义 message 时，应以当前自动生成的建议 message 为基础进行修改
- 默认先展示建议 message，再由用户指出需要改成什么
- 使用用户确认后的最终 message 执行提交

### 选项 3：复用上一个 commit message

- 读取上一个 commit message
- 使用相同 message 执行新的提交

### 选项 4：合并到上一个 commit

只有在以下条件全部满足时，才允许执行：

- 上一个 commit 是当前用户提交的
- 远程没有比本地更新的提交

满足条件后，直接执行 amend。

## amend 判断要点

执行“合并到上一个 commit”前，至少确认：

1. `git log -1` 显示的作者是当前用户
2. 本地分支与远程分支相比，没有远程领先的提交

如果任一条件不满足，不要执行 amend，应明确告诉用户当前不能直接合并到上一个 commit。

## 输出要求

- 先展示建议的 commit message
- 如果用户是通过 `$lz-git-commit` 触发，直接开始流程，不再额外追问提交意图
- 明确展示四个可选动作
- 在真正执行提交后，明确告诉用户使用了哪一种方式：
  - 使用建议 message 正常提交
  - 基于建议 message 修改后提交
  - 复用上一个 message 提交
  - amend 到上一个 commit
