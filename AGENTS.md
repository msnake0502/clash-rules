# Repository Guidelines

## 项目结构与模块组织

这是一个仅包含 Clash / Mihomo 规则数据的仓库。`release` 分支是 Raw 地址和 Release 附件的发布来源。

- `mydirect.txt`：常见中国大陆网站直连域名规则。
- `ai.txt`：海外 AI 服务域名代理规则。
- `app.txt`：AI 应用的 `PROCESS-NAME` 进程规则。
- `README.md`：规则提供程序、路由行为与使用示例。

每份规则文件均为 UTF-8 YAML，顶层键为 `payload:`。仓库不包含应用源代码、构建产物或测试目录。

## 构建、测试与开发命令

无需构建。提交前请检查变更文件，例如：

```powershell
Get-Content .\ai.txt
```

确认域名文件以 `payload:` 开头，且每条规则形如 `  - '+.example.com'`。`app.txt` 使用 `  - PROCESS-NAME,Example.exe`。检查空行、重复项、YAML 缩进错误，以及 `+.google.com`、`+.microsoft.com` 这类范围过宽的域名。

## 规则风格与命名规范

每条 `payload` 项目前固定使用两个空格。域名通配符必须加引号，例如 `  - '+.chatgpt.com'`；`PROCESS-NAME` 规则不加引号。优先使用能覆盖目标服务的最小官方域名后缀；除非路由目的明确，否则不要加入共享云服务、CDN、搜索引擎或企业根域名。

文件名使用小写和 `.txt` 后缀。规则按服务归类，删除完全重复项，并保持 YAML 格式一致。进程别名仅添加已确认的可执行文件名或移动端包标识。

## 测试指南

按数据规则进行验证：解析 YAML、检查每行只包含一条规则，并在发布后访问 Raw 地址。域名 Provider 使用 `behavior: domain`；`app.txt` 使用 `behavior: classical`。`PROCESS-NAME` 的支持因内核和操作系统而异；新增不熟悉的标识时，请在 PR 中说明平台依据。

## 提交与拉取请求规范

提交标题使用简短祈使句，遵循现有风格：`Add OpenCode service domains`、`Add AI application process rules` 或 `Document Clash rule providers`。每次提交只聚焦一个规则文件或文档变更。

PR 需说明影响的文件、增删规则及路由原因，并附上验证结果。对于不熟悉的服务或进程名，应链接官方资料。不要声称路由规则能够规避账号风控、限制或封禁。
