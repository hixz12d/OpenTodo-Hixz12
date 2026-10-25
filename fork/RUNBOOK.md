# 运维手册

本 fork 只在用户的天理云美西 VPS 上运行。部署资料统一维护在 VPS 运维仓库（本仓库的上一级目录），这里只给入口，不重复步骤。

## 环境一览

| 环境 | 地址 | 服务器上的目录 | 访问方式 | 凭据在哪 |
|---|---|---|---|---|
| 生产 | `https://todo.xiaozhudf2026.foo` | `/opt/opentodo`（Compose），数据 `/data/opentodo` | `ops` 用户 + 密钥 SSH，见 VPS 仓库 `docs/RUNBOOK.md` | SSH 密钥在本机 `~/.ssh/sub2api-baseline/`；安装令牌只在服务器 `/opt/opentodo/.env` |

## 部署、回滚、健康检查

- 当前运行版本、目录、健康检查、日志、忘记密码：VPS 仓库 `docs/RUNBOOK.md` 的「OpenTodo」一节。
- 构建镜像、上线、回滚步骤：VPS 仓库 `deploy/opentodo/README.md`。要点：本机用本仓库提交构建 Linux amd64 镜像后上传，不拉原作者镜像；上线前先在应用里做一次备份。

## git 远端

- `origin`：`https://github.com/hixz12d/OpenTodo-Hixz12`（用户 fork，上线从这里构建）。fork 的 GitHub Actions 已关闭（继承自上游的 CI、夜间构建和镜像发布任务，自用不需要），推送不会触发任何任务。
- 同步原版更新：`git remote add upstream https://github.com/pixari/opentodo`（首次），然后 `git fetch upstream && git merge upstream/main`。fork 改动集中在新增文件，合并冲突主要可能出现在 `web/src/locales/index.ts`、`web/public/push-sw.js` 等登记处；合并后新增的英文条目需补译（`node scripts/i18n-check.mjs` 会列出）。
