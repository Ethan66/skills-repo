# lz-git-commit 设计

**目标：** 创建一个在用户显式使用 `$lz-git-commit`，或明确要求提交时触发的 skill，用于生成 commit message、让用户确认，并执行 `git commit` 或 `git commit --amend`。

## 触发条件

以下两种情况触发：

- 用户显式使用 `$lz-git-commit`
- 用户明确要求提交，例如：

- 帮我提交
- 帮我 commit
- 提交这些改动
- 用合适的 message 提交

不因为任务“看起来做完了”就自动触发。

## 执行范围

- 不分析改动质量
- 不判断是否存在无关改动
- 不判断是否应该拆分为多个提交
- 不默认运行 lint 或 test

## 核心流程

1. 用户显式使用 `$lz-git-commit`，或明确要求提交时触发
2. 为当前改动生成建议的 commit message，格式为 `type: 中文描述`
3. 把建议 message 展示给用户
4. 提供四个选项：
   - 直接使用当前建议 message 提交
   - 用户基于建议 message 自定义修改
   - 直接复用上一个 commit message
   - 直接合并到上一个 commit
5. 如果用户选择“合并到上一个 commit”，并且满足：
   - 上一个 commit 是当前用户提交的
   - 远程没有比本地更新的提交
   则直接执行 amend

## 设计原则

- 提交动作由用户明确发起
- 显式使用 `$lz-git-commit`` 时，直接开始流程，不再额外询问提交意图
- message 生成与确认是主流程重点
- 自定义 message 不是从零开始，而是基于建议 message 修改
- amend 允许自动执行，但必须受限于明确前置条件
