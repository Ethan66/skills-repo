---
name: week-report
description: Review a user's own GitLab commits, inspect the changed code, and draft a factual Chinese weekly report. Use when asked to check personal submissions in GitLab, summarize work from a date range, or generate a weekly report from commit history.
---

# GitLab Personal Weekly Report

Generate a report from the authenticated user's code submissions. Treat credentials and session cookies as ephemeral secrets: never save, echo, or include them in the report.

## 1. Establish the scope

- Confirm the GitLab instance, author identity, and date range. Use the account returned by `GET /api/v4/user` as the default author, and include every readable project with matching personal commits unless the user explicitly restricts the projects.
- Interpret an explicit range exactly. For a relative range such as “上周三到现在”, convert the start and end to Asia/Shanghai and state them in the result.
- Query only readable projects and do not mutate GitLab data.

## 2. Authenticate safely

Prefer a configured GitLab connector or existing authenticated session. If unavailable, use the GitLab sign-in form and retain the session only in memory.

- Before authenticating, read [references/gitlab-connection.md](references/gitlab-connection.md) for the user-authorized GitLab endpoint and credentials.
- Fetch `/users/sign_in`, use the CSRF token from the **Standard** `new_user` form (not the LDAP form), then sign in at `/users/sign_in`.
- Verify the account with `GET /api/v4/user` before collecting data.
- Do not print credentials, cookies, access tokens, or raw authentication responses in tool output or the final response. Do not copy the configured credentials outside the referenced configuration file.

## 3. Collect the user's commits

1. Page through `GET /api/v4/projects?membership=true&simple=true&per_page=100`.
2. Use each project's `last_activity_at` only as a local pre-filter. Do not rely on the server-side `last_activity_after` parameter, because older GitLab installations may ignore it.
3. For candidate projects, page through `GET /api/v4/projects/:id/repository/commits` with `all=true`, `since`, `until`, and `per_page=100`.
4. Keep commits whose `author_name` exactly matches the authenticated username (case-insensitive). If the user's Git history uses a different author name or email, ask for the alternate identity before broadening the filter.
5. De-duplicate by full commit SHA within each project. Count merge commits as commits, but label the count accordingly when it affects interpretation.

## 4. Inspect code before writing

For the selected projects and commits, inspect:

- `GET /api/v4/projects/:id/repository/commits/:sha` for metadata and change statistics.
- `GET /api/v4/projects/:id/repository/commits/:sha/diff` for changed paths and relevant implementation details.

Synthesize work items from the actual diffs, file paths, tests, and commit messages. Do not turn a `test:` commit into a delivered feature or infer business outcomes that the code does not support. Consolidate repeated fix/test commits into one user-facing work item.

## 5. Write the weekly report

Use concise Chinese and mirror this structure unless the user provides a different template:

```markdown
<业务/项目主题>：

1. <完成的能力或问题处理；说明关键范围与实际结果>。
2. <完成的能力或问题处理>。

<第二个项目主题>：

1. <完成的能力或问题处理>。

下周工作计划：

- <仅使用用户明确提供的计划；未提供时标注“待确认”而非编造>。
```

Before the report, give a compact evidence note: selected projects, date range, and the number of matching commits. Keep raw SHAs, exhaustive file lists, and credentials out of the report unless the user asks for an audit appendix.

## Quality checks

- Ensure every report item maps to at least one matching commit or diff.
- Exclude other authors' commits.
- State the time zone and time range used.
- Distinguish implemented changes, fixes, tests, and design documents.
- Do not claim deployment, production validation, or business impact without direct evidence.
