# lz-git-commit

## 用途

这个 skill 用于在用户显式使用 `$lz-git-commit`，或明确要求提交时，生成 commit message、让用户确认，并执行 `git commit` 或 `git commit --amend`。

## 使用场景

- 直接输入 `$lz-git-commit`
- 帮我提交
- 帮我 commit
- 提交这些改动
- 用合适的 message 提交

以下情况不触发：

- 任务只是看起来完成了，但用户没有显式使用 `$lz-git-commit`，也没有明确要求提交
- 纯讨论 commit 风格
- 纯分析 git 状态

## 工作流

1. 用户显式使用 `$lz-git-commit`，或明确要求提交时触发
2. 为当前改动生成建议的 commit message，格式为 `type: 中文描述`
3. 把建议 message 展示给用户
4. 提供四个选项：
   - 直接使用当前建议 message 提交
   - 基于当前建议 message 修改后提交
   - 使用上一个 commit message 提交
   - 合并到上一个 commit
5. 如果用户选择第四项，并且满足 amend 前置条件，则直接执行 amend

## 约束边界

- 不分析改动质量
- 不判断是否存在无关改动
- 不判断是否应该拆分为多个提交
- 不默认运行 lint 或 test

## amend 前置条件

- 上一个 commit 是当前用户提交的
- 远程没有比本地更新的提交

## 示例

### 示例 1

输入：`$lz-git-commit`

预期行为：直接开始提交流程，先生成一条 `type: 中文描述` 的 message，再让用户从四个选项中选择

### 示例 2

输入：这条 message 不对，直接合并到上一个 commit

预期行为：检查 amend 前置条件，满足时直接执行 amend

### 示例 3

输入：这条 message 的 type 不对，描述也改一下，基于现在这条改成 `fix: 修复登录弹窗关闭后状态未重置`

预期行为：以自动生成的建议 message 为基础修改，使用用户确认后的最终 message 执行提交
