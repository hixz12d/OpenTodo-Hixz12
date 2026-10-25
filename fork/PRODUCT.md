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
| 简体中文界面 | 设置 → 通用 → 语言 选"简体中文"；选"跟随系统"时中文浏览器自动显示中文（繁体浏览器也显示简体）。覆盖网页界面全部 5252 条文案、系统推送通知、浏览器扩展 | 已上线 |

中文界面的边界：
- 译文由 AI 完成，未逐条人工审核；用着觉得别扭的词，直接改 `web/src/locales/zh.json` 对应条目。
- 不翻译：邮件模板与每周摘要（服务器未配 SMTP）、通知渠道（ntfy 等）消息、应用内帮助文档（上游规定保持英文）、安卓壳。
- 快速添加只认英文日期写法（如 `tomorrow at 3pm`），不认"明天下午 3 点"。
- 已知小问题：侧边栏"项目"标题后的读屏隐藏文字显示为"，0 项"前带英文逗号；个别一词多用的键（如 `on` 同时用于筛选"当天"和开关"开"）只能取一种译法。

## 术语表（中文翻译统一用词）

翻译时界面用词以此表为准，新增词条先补到这里。表里没有的词，以 `zh.json` 里同一英文词的现有译法为准（先搜再译）。对照上游 `docs/translating.md` 的 Glossary。

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
| You（设置分组） | 你 | 同一个键也用作"你"这个人 |
| General / Capture / People | 通用 / 收集 / 人员 | 设置分区 |
| Workspace | 工作区 | |
| Do on | 计划日 | Due date 的口语叫法 |
| Group（动作） / Groups（成员组） | 归类 / 成员组 | 不用"分组"，避免与 Section 混淆 |
| Filter | 筛选器（名词） / 筛选（动作） | 筛选语法关键词不译 |
| Archive（任务、项目） / Archive（备份打包文件） | 归档 / 存档 | |
| Undo / Revoke | 撤销 / 吊销 | 令牌、链接、密码用"吊销" |
| Remove / Delete | 移除 / 删除 | Remove 是从某处拿掉，Delete 是删掉本身 |
| Snooze / Defer | 再提醒 / 推迟 | |
| Token / API tokens | 令牌 / API 令牌 | |
| App password | 应用专用密码 | CalDAV 用 |
| Provider | 提供方 | 登录提供方、身份提供方 |
| Delivery channels | 通知渠道 | |
| Issues | 议题 | GitHub、GitLab 的 issue |
| Focus / Close the day | 专注 / 今日收尾 | |
| Open Loops、Webhook、MCP、SSO | 不译 | 产品名、方法名和缩写 |

## 体验约定

- 中文用"你"，不用"您"；语气简洁口语化，与上游各语言风格一致。
- 占位符（`{name}`）、标签（`<a>`）、复数结构必须与英文原文一致。
- 任务标题、项目名等用户数据从不翻译；筛选语法、重复规则关键词保持英文（上游规定）。
