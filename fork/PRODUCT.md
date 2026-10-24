# OpenTodo（hixz12d fork）

## 一句话

用户在自己 VPS 上运行的自托管待办与任务管理应用。fork 自 `pixari/opentodo`，在原版基础上只加用户需要的改动，目前主要是简体中文界面。

## 用户与场景

- 用户本人（所有者）和受邀的人：在浏览器或手机上管理任务、项目、提醒，多设备离线同步。
- 入口 `https://todo.xiaozhudf2026.foo`，部署见 [RUNBOOK.md](RUNBOOK.md)。

原版功能全集见上游 `README.md` 和 `docs/`（英文用户手册），这里不重复。

## fork 相对原版的改动

| 改动 | 说明 | 状态 |
|---|---|---|
| 简体中文界面 | 设置 → General → Language 可选中文；翻译文件 `web/src/locales/zh.json` | 计划中 |

## 术语表（中文翻译统一用词）

翻译时界面用词以此表为准，新增词条先补到这里。对照上游 `docs/translating.md` 的 Glossary。当前是初稿，汉化开工前与用户确认。

| English | 中文 | 说明 |
|---|---|---|
| Task / Subtask | 任务 / 子任务 | |
| Project / Section | 项目 / 分组 | Section 是项目内的分段 |
| Label | 标签 | |
| Inbox | 收件箱 | 未归入项目且未安排日期的任务 |
| Today / Upcoming | 今天 / 即将到来 | |
| Anytime / Someday | 随时 / 某天 | |
| This Evening | 今晚 | |
| Completed / Trash | 已完成 / 回收站 | |
| Due date / Deadline | 到期日 / 截止日期 | Due 是计划做的日子，Deadline 是最晚期限 |
| Reminder | 提醒 | |
| Quick add | 快速添加 | |
| Settings | 设置 | |
| Owner, admin, editor, viewer | 所有者、管理员、编辑者、查看者 | |
| Passkey | 通行密钥 | |
| Two-factor authentication | 双重验证 | |
| Weekly review | 每周回顾 | |

## 体验约定

- 中文用"你"，不用"您"；语气简洁口语化，与上游各语言风格一致。
- 占位符（`{name}`）、标签（`<a>`）、复数结构必须与英文原文一致。
- 任务标题、项目名等用户数据从不翻译；筛选语法、重复规则关键词保持英文（上游规定）。
