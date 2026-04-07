# My Proxy Rules - DNS Overwrite

这是一个自用的 Clash DNS 配置覆写（Overwrite）规则与脚本仓库。主要用于优化和接管代理客户端的 DNS 解析流程，防止 DNS 污染并提升解析速度。

为了适应不同的内核特性与个人偏好，仓库内提供了基于 **DOMAIN (域名)** 与基于 **GeoData (地理数据)** 的多套实现版本，并分别提供 YAML 配置片段（Merge/Mixin）和 JavaScript 预处理脚本（Parser），以适配不同的 Clash 客户端（如 Clash Verge, Clash for Windows 等）。

## 📂 文件说明

本项目将规则分为 **现代版（域名服务器策略）** 和 **传统版（Fallback）** 两个大类，并在此基础上提供了 **DOMAIN 匹配** 与 **GeoData 匹配** 两种方式：

### 1. 基于域名服务器策略 (Nameserver Policy) 版本
使用现代 Clash 内核（如 Meta 内核）推荐的 `nameserver-policy` 进行精确的分流解析。

* **基于 DOMAIN 的精确匹配：**
  * `clash_dns.yaml`：YAML 格式的 DNS 覆写配置片段，适用于支持 Merge/Mixin 的客户端。
  * `script_clash_dns.js`：JavaScript 预处理脚本，适用于 Clash Verge 等支持 JS Parser 的客户端。
* **基于 GeoData 的轻量匹配（🆕 新增）：**
  * `clash_rules_geo_dns.yaml`：使用 `geosite` / `geoip` 数据代替海量 `DOMAIN` 规则的 YAML 配置，体积更小，解析逻辑更简洁，推荐 Meta 内核用户使用。

### 2. 基于传统 Fallback 策略 (Legacy) 版本
使用传统的 `nameserver` + `fallback` 策略，兼容较老版本的 Clash 内核（如原版 Premium 内核）。

* **基于 DOMAIN 的传统匹配：**
  * `clash_dns_legacy.yaml`：传统的 YAML 格式 DNS 覆写配置片段。
  * `script_clash_dns_legacy.js`：传统的 JavaScript 预处理脚本。
* **基于 GeoData 的传统匹配（🆕 新增）：**
  * `script_clash_rules_geo_dns.js`：结合传统的 fallback 机制与 `GeoData` 匹配方式的 JavaScript 预处理脚本。

## 💡 DOMAIN 版本 vs GeoData 版本该怎么选？

- **DOMAIN 版本**：直接在配置中列出具体的域名和后缀（如 `DOMAIN-SUFFIX,google.com`）。**优点**是规则明确透明、对内核版本要求低，无需依赖外部数据文件；**缺点**是随着拦截域名的增加，配置文件会越来越冗长。
- **GeoData 版本**：依赖内核的数据库文件（如 `geosite:cn`, `geosite:gfw` 等）。**优点**是配置文件极为短小精悍，加载极快，维护成本低；**缺点**是需要依赖支持 Geo 规则的内核（尤其是 Meta 内核），并且需要客户端定期更新 Geo 数据库。

## 🚀 使用方法 (以 Clash Verge 为例)

### 使用 JS 脚本 (推荐)
1. 打开客户端的 **订阅设置** 或 **配置预处理 (Merge/Script)** 界面。
2. 新建一个 JS 类型的预处理规则。
3. 根据你的需求，将选定的 JS 脚本（如 `script_clash_dns.js` 或 `script_clash_rules_geo_dns.js`）中的代码复制进去，并应用到你的订阅链接上。

### 使用 YAML 片段
1. 找到客户端的 **Merge / Mixin** 功能。
2. 根据你的需求，将选定的 YAML 文件（如 `clash_dns.yaml` 或 `clash_rules_geo_dns.yaml`）中的内容粘贴到对应的文本框中。
3. 保存并重载配置。

## ⚠️ 注意事项

* 本项目为个人自用配置，其中的上游 DNS 服务器（如 阿里、腾讯、Google、Cloudflare 等）是基于我个人的网络环境设置的。
* 如果你 Fork 或参考使用，请根据你当地的运营商和网络情况，自行修改代码中的 DNS 服务器 IP，以达到最佳的解析效果。
* **使用 GeoData 版本时，请务必确保你的代理客户端已配置定期更新 Geo 数据库文件（`geosite.dat` 和 `geoip.dat` 或 `Meta.db`），否则可能导致最新域名的 DNS 解析分流失效。**
