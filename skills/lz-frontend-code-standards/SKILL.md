---
name: lz-frontend-code-standards
description: 在前端实现阶段使用。只要任务已经开始写或改 Vue、JavaScript、TypeScript 代码，或涉及组件开发、页面开发、前端重构、前端交互逻辑、composables 或 hooks 改动，就必须使用这个 skill。纯分析、纯讨论、纯方案设计阶段不要触发。
---

# 目的

这个 skill 用于在前端实现阶段统一约束 Vue、JavaScript、TypeScript 代码规范。它不是通用建议文档，而是进入写代码和改代码阶段后的执行规范。

## 何时使用

当任务已经明确进入实现阶段，并出现以下任一信号时，触发这个 skill：

- `.vue` 文件改动
- `.js` 或 `.ts` 文件改动
- 组件开发
- 页面开发
- 前端重构
- 前端交互逻辑实现
- composables / hooks 编写或修改

以下情况不要触发：

- 纯分析
- 纯讨论
- 纯方案设计

## 执行原则

1. 先识别项目当前技术上下文：
   - 当前是 Vue 2 还是 Vue 3
   - 当前主流是 Options API 还是 Composition API
   - 当前目录和文件里是否已经存在明确的主流命名和组织方式
2. 跟随项目当前主流技术风格，不主动推动整体迁移。
3. 不主动治理历史旧代码，只对本次新增和修改的代码强制执行本 skill 的规范。
4. 如果当前文件局部风格混乱，以项目主流风格和本 skill 规则为准，在本次改动范围内收敛。

## 触发标记

当这个 skill 被触发，且任务已经明确进入前端实现阶段时，先输出下面这行固定标记，再继续后续实现：

`[已触发 lz-frontend-code-standards]`

如果当前任务仍处于纯分析、纯讨论、纯方案设计阶段，则不要输出这个标记。

## JavaScript / TypeScript 通用规范

### 命名约定

- 普通事件处理方法使用 `handle` 开头，例如 `handleSubmit`
- 变量和函数使用 camelCase，例如 `userName`、`getUserData`
- 常量使用 UPPER_SNAKE_CASE，例如 `MAX_RETRY_COUNT`
- 类使用 PascalCase，例如 `UserService`
- 私有属性可使用 `_` 开头
- API 请求方法使用 `api` 开头，例如 `apiGetUser`
- Hook 或组合式函数使用 `use` 开头，例如 `useUserStore`
- 函数内部临时变量必须以 `temp` 开头或 `_` 开头，例如 `tempValue`、`_formattedList`
- 接口原始响应统一命名为 `res`
- 存储接口数据的响应式变量带 `ResData` 或 `Data` 后缀，例如 `orderResData`
- DOM 或组件模板引用统一使用 `Ref` 结尾，例如 `formRef`

### 代码风格

- 使用 2 空格缩进
- 字符串优先使用单引号
- 不要连续深层嵌套三目运算，超过两层改用 `if` / `else` 或 `switch`
- 属性较少且不影响可读性时，对象字面量可以写成单行
- 长函数优先使用早返回，减少嵌套

### 定时器规范

- 使用 `setTimeout`、`setInterval` 时，必须在合适时机清理
- 在组件卸载、路由离开或业务完成时调用 `clearTimeout` 或 `clearInterval`
- 如果在定时器回调内判断不再需要执行，先清理再返回

## Vue 规范

### 基础约定

- 组件文件使用 PascalCase
- 如果项目主流是 Composition API，则优先遵循 Composition API
- 模板中组件标签使用 kebab-case

### 事件与方法命名

- 原生 DOM 元素绑定的事件函数使用 `on` 开头
- 组件自定义事件绑定函数，以及组件内部业务处理方法，使用 `handle` 开头

### DOM / 组件 Ref 命名

- DOM 或组件 `ref` 变量统一使用 `Ref` 结尾

### 表单 options 结构

- 同一页面存在多个 `select`、`checkbox`、`radio` 配置时，将选项统一收敛到一个 `options` 对象中
- 不要将多个平级选项数组零散散落在状态定义中

## `<script setup>` 结构规范

如果当前文件使用 `<script setup>`，按以下固定顺序组织：

1. 外部依赖导入
2. `props` 与 `emits` 定义
3. 响应式状态定义
4. 衍生状态 `computed`
5. 状态监听 `watch`
6. 业务方法函数
7. 生命周期钩子

状态、方法和监听尽量集中定义，不要零散插入。

## hooks / composables 拆分规范

- 只有当前组件使用、且代码量不大时，直接保留在组件内部
- 仅当前组件使用，但逻辑明显过长时，拆到该组件同级目录下的私有 hooks 中
- 只有明确会在多个页面或组件复用时，才拆到全局 `hooks` 或 `composables` 目录
- 私有或公共 hook 都要明确入参与返回值，不要隐式依赖全局状态

## Review 友好性规则

- 避免深层解构响应式数据，优先保留语义明确的命名空间访问方式
- 不要为了“看起来整洁”而过度封装
- 命名应保持可搜索性，避免使用过度泛化的名称，如 `data`、`info`、`list`
- 优先使用带业务语义的具体命名

## 写代码前检查项

在开始实现前，先完成以下判断：

1. 当前任务是否已经进入前端实现阶段，而不是分析或讨论阶段
2. 本次改动是否涉及 `.vue`、`.js`、`.ts`、组件、页面、交互逻辑、hooks 或 composables
3. 当前项目是 Vue 2 还是 Vue 3
4. 当前项目主流是 Options API 还是 Composition API
5. 本次改动范围中的新增和修改代码，应该按哪些规范收敛
6. 如果确认已经进入实现阶段，先输出固定触发标记，再开始写代码或改代码

## 提交前自检项

在完成代码后，检查以下内容：

- 命名是否符合 `on`、`handle`、`use`、`Ref`、`res`、`ResData` 等规则
- 新增和修改代码是否保持 2 空格缩进、单引号、早返回等风格
- 如果是 Vue 文件，组件名、模板标签名、事件绑定和 `ref` 命名是否正确
- 如果使用 `<script setup>`，代码顺序是否符合固定结构
- 多个表单选项配置是否已经收敛到 `options`
- 定时器是否做了清理
- 只有一个地方使用的逻辑是否避免了过度抽离
- 命名是否具体、可搜索、便于 Review
