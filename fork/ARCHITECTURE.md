# 架构（fork 视角）

上游的完整代码地图在根目录 `AGENTS.md` 的 Layout 一节和 `docs/architecture.md`，这里只记 fork 改动会碰到的部分。

## 技术栈

- 服务端：Go（`cmd/opentodo`）+ SQLite，前端打包后嵌进二进制。
- 前端：`web/`，Vite + React 19 + Tailwind 4 + Dexie（浏览器本地数据库）。
- 浏览器扩展 `extension/`：只加了中文翻译；安卓壳 `mobile/`：本 fork 不改。

## 目录地图

| 路径 | 作用 |
|---|---|
| `fork/` | 本 fork 自己的文档和计划（不放 `docs/`，原因见 `AGENTS.md` 的 fork 规则） |
| `web/src/lib/i18n/` | 翻译层：`t()`、`msg()`、错误码翻译 `errors.ts` |
| `web/src/locales/messages.json` | 全部英文原文清单（脚本生成，不手改） |
| `web/src/locales/<语言>.json` | 各语言翻译，键是英文原文，值是译文；中文是 `zh.json`（语言代码 `zh`） |
| `web/src/locales/index.ts` | `SHIPPED`：设置里可选的语言列表 |
| `web/src/lib/userPrefs.ts`、`web/src/lib/types.ts` | `LANGUAGES`、`LanguagePref`：新增语言必须和 `SHIPPED` 一起登记，否则选了读回成"跟随系统" |
| `web/src/index.css` | `--font-sans` 里的中文字体回退（PingFang SC、Microsoft YaHei、Noto Sans CJK SC），上游 Inter 不含汉字 |
| `web/public/push-sw.js` | 系统推送通知的少量文案表（按语言，含 `zh` 行） |
| `web/src/lib/nlp/vocab/` | 快速添加识别日期用的各语言词汇（如"明天"）；没有中文 |
| `extension/_locales/` | 浏览器扩展的翻译，中文在 `zh_CN/` |
| `web/src/app/languageSettings.test.tsx`、`web/src/lib/settingsCopy.test.ts`、`extension/locales.test.js` | 测试里写死的语言列表，已加中文；再加语言时一起改 |
| `internal/mail/templates/` | 服务端邮件模板（`*.<语言>.txt`） |
| `scripts/i18n/`、`scripts/i18n-check.mjs` | 原文提取与翻译检查 |

## 本地运行

本机没有 `make`，用等价命令（Git Bash）：

```bash
cd web && npm ci --no-audit --no-fund && npm run build && cd ..
go run ./cmd/opentodo          # 打开 http://localhost:8080，首次访问创建所有者
# 前端热更新：另开终端 cd web && npm run dev（:5173，接口转发到 :8080）
```

## 基本检查

改完必跑（需先在 `web/` 执行过一次 `npm ci`）：

```bash
node scripts/i18n-check.mjs          # 翻译缺漏、占位符不一致、未使用的条目
cd web && npm run typecheck          # 前端类型检查
```

改了 Go 代码再加 `go build ./...`（前端没构建时也能编译，只是内嵌页面为空）。

Windows 注意：上游 i18n 脚本按 `/` 匹配路径。`scripts/i18n/extract.mjs` 里快捷键文件的判断已改成兼容 `\`；但 `node scripts/i18n/extract.mjs --write`（重新生成 `messages.json`）在 Windows 上仍会写出反斜杠路径，只翻译时不需要运行它，必须运行时在 WSL 或 Docker 里跑。
