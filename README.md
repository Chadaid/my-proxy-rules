# My Proxy Rules - DNS Overwrite

这是一个自用的 Clash DNS 配置覆写（Overwrite）规则与脚本仓库。主要用于优化和接管代理客户端的 DNS 解析流程，防止 DNS 污染并提升解析速度。

仓库内包含了两种不同 DNS 策略的实现版本，分别提供 YAML 配置片段（Merge/Mixin）和 JavaScript 预处理脚本（Parser），以适配不同的 Clash 客户端（如 Clash Verge, Clash for Windows 等）。

## 📂 文件说明

本项目将规则分为<b>现代版（域名服务器策略）<b/>和<b>传统版（Fallback）<b/>两个大类：

### 1. 基于域名服务器策略 (Nameserver Policy) 版本
使用现代 Clash 内核（如 Meta 内核）推荐的 `nameserver-policy` 进行精确的分流解析。
* **`clash_dns.yaml`**：YAML 格式的 DNS 覆写配置片段，适用于支持 Merge 或 Mixin 的客户端。
* **`script_clash_dns.js`**：JavaScript 预处理脚本，适用于 Clash Verge 等支持 JS Parser 的客户端。

### 2. 基于传统 Fallback 策略 (Legacy) 版本
使用传统的 `nameserver` + `fallback` 策略，兼容较老版本的 Clash 内核。
* **`clash_dns_legacy.yaml`**：传统的 YAML 格式 DNS 覆写配置片段。
* **`script_clash_dns_legacy.js`**：传统的 JavaScript 预处理脚本。

## 🚀 使用方法 (以 Clash Verge 为例)

### 使用 JS 脚本 (推荐)
1. 打开客户端的 **订阅设置** 或 **配置预处理 (Merge/Script)** 界面。
2. 新建一个 JS 类型的预处理规则。
3. 将 `script_clash_dns.js` (或 legacy 版本) 中的代码复制进去，并应用到你的订阅链接上。

### 使用 YAML 片段
1. 找到客户端的 **Merge / Mixin** 功能。
2. 将 `clash_dns.yaml` (或 legacy 版本) 中的内容粘贴到对应的文本框中。
3. 保存并重载配置。

## ⚠️ 注意事项
* 本项目为个人自用配置，其中的上游 DNS 服务器（如 阿里、腾讯、Google、Cloudflare 等）是基于我个人的网络环境设置的。
* 如果你 Fork 或参考使用，请根据你当地的运营商和网络情况，自行修改代码中的 DNS 服务器 IP，以达到最佳的解析效果。
