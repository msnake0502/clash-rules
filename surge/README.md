# Surge 规则集

本目录将 Clash YAML `payload` 规则转换为 Surge 外部规则集。每个 `.list` 文件每行只含规则类型和匹配值，不含策略；策略由 `surge-rules.conf` 的 `RULE-SET` 行指定。发布后可通过 `https://raw.githubusercontent.com/msnake0502/clash-rules/release/surge/<文件名>.list` 固定引用；更新同一路径文件即可让使用者刷新规则而无需改 Surge 配置。

- 域名：`DOMAIN-SUFFIX,example.com`
- IPv4 / IPv6：`IP-CIDR,1.2.3.0/24` / `IP-CIDR6,2001:db8::/32`
- 进程：`PROCESS-NAME,Example`（仅 Surge Mac 支持）

把 `surge-rules.conf` 中的 `JMS` 改为实际存在的 Surge 策略组名称。规则按顺序匹配，`FINAL,JMS` 必须位于 `[Rule]` 段最后。CIDR 规则带有 `no-resolve`，以避免它们对域名请求触发本地 DNS 解析。

源规则包括本仓库的 `ai.txt`、`mydirect.txt`、`myproxy.txt`、`app.txt`、`directapp.txt`，及 Loyalsoldier `clash-rules` release 分支中模板列出的对应文件。转换日期：2026-07-27。
