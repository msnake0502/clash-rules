# clash-rules

适用于 Clash / Mihomo 的个人规则集，提供国内及按需指定服务直连、海外 AI 域名和需要魔法上网的应用进程规则。

## 规则文件

| 文件 | 用途 | Raw 地址 | Provider 行为 |
| --- | --- | --- | --- |
| `mydirect.txt` | 常见中国大陆网站及指定服务直连 | `https://raw.githubusercontent.com/msnake0502/clash-rules/release/mydirect.txt` | `domain` |
| `myproxy.txt` | 常见海外服务代理 | `https://raw.githubusercontent.com/msnake0502/clash-rules/release/myproxy.txt` | `domain` |
| `ai.txt` | 海外 AI 服务域名代理 | `https://raw.githubusercontent.com/msnake0502/clash-rules/release/ai.txt` | `domain` |
| `app.txt` | 需要魔法上网的应用进程代理 | `https://raw.githubusercontent.com/msnake0502/clash-rules/release/app.txt` | `classical` |

所有规则文件均使用 YAML `payload` 格式。域名规则采用 `'+.example.com'` 通配符写法。

## Surge 规则集

`surge/` 包含上述规则转换后的 Surge 外部规则集（`.list`）和 `surge-rules.conf` 模板。域名已转换为 `DOMAIN-SUFFIX`，CIDR 已转换为 `IP-CIDR` / `IP-CIDR6`，应用规则保留为 `PROCESS-NAME`。详情见 [`surge/README.md`](surge/README.md)。

## 配置示例

```yaml
rule-providers:
  mydirect:
    type: http
    behavior: domain
    format: yaml
    url: https://raw.githubusercontent.com/msnake0502/clash-rules/release/mydirect.txt
    path: ./ruleset/mydirect.yaml
    interval: 86400

  myproxy:
    type: http
    behavior: domain
    format: yaml
    url: https://raw.githubusercontent.com/msnake0502/clash-rules/release/myproxy.txt
    path: ./ruleset/myproxy.yaml
    interval: 86400

  ai:
    type: http
    behavior: domain
    format: yaml
    url: https://raw.githubusercontent.com/msnake0502/clash-rules/release/ai.txt
    path: ./ruleset/ai.yaml
    interval: 86400

  app:
    type: http
    behavior: classical
    format: yaml
    url: https://raw.githubusercontent.com/msnake0502/clash-rules/release/app.txt
    path: ./ruleset/app.yaml
    interval: 86400

rules:
  - RULE-SET,mydirect,DIRECT
  - RULE-SET,app,PROXY
  - RULE-SET,ai,PROXY
  - RULE-SET,myproxy,PROXY
```

## 内容说明

- `mydirect.txt`：腾讯、阿里、百度、字节跳动、电商、银行、交通、物流等常见国内服务，以及按需指定的直连服务。
- `myproxy.txt`：Google、YouTube、Telegram、Discord、X、GitHub、Dropbox、Netflix 等常见海外服务。
- `ai.txt`：ChatGPT、OpenAI、Claude、Gemini、OpenCode、Perplexity、Mistral、Grok、Hugging Face 等海外 AI 服务域名。
- `app.txt`：ChatGPT、Codex、Claude、Gemini、OpenCode、Cursor、Windsurf、Telegram、iStat Menus、UU Remote 等需要魔法上网的应用进程标识。

## 注意事项

- `PROCESS-NAME` 的可用性取决于所用 Clash / Mihomo 内核及操作系统；桌面端通常使用进程名，移动端通常使用应用包名或标识。
- 应用进程规则仅决定流量路由，不能保证规避服务商的账号风控、限制或封禁。
- 请遵守所在地法律法规及各服务的使用条款。
