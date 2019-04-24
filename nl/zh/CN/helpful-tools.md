---
copyright:
  years: 2018
lastupdated: "2018-03-01"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 用于管理 CIS 部署的有用工具

具有一些可帮助您管理 IBM CIS 部署的公共域 Unix 系统管理工具。

## Sysadmin 工具

 * whois（域标识工具）
 * dig（DNS 工具）
 * curl（HTTP 和 HTTPS 池）
 * netcat（IP 和端口池）
 * traceroute（网络工具）

## 用于外部和远程测试的商业工具：

 * GTMetrix (http)
 * Web 页面测试 (http)
 * WhatsMyDNS（DNS 工具）
 * G Suite Toolbox（DNS 和 HTTP）

## 用于查看日志和历史记录的工具

 * HTTP 归档文件（HAR 文件）


### 使用 `whois`

`whois` 是一种 Unix 系统命令行工具，可用于查找给定域名或 IP 地址的注册器信息，例如，该域的给定授权服务器或特定 IP 地址的所有者。

示例：

`whois example.com`

`whois 8.8.8.8`

### 使用 `dig`

`dig` 是一种 Unix 命令行工具，可用于执行 DNS 查询并检查特定域的 DNS 记录。它类似于 `nslookup`。

此命令的模式为：dig <recordtype. <domainname> <options>

**示例：**

`dig example.com`

`dig my.example.com`

`dig example.com +trace`

`dig NS example.com`

`dig example.com @ns.example.com`

### 使用 `cURL`

`cURL` 是一种 Unix 命令行工具，使您能够使用 URL 语法来传输数据。此工具通常用于发出 HTTP 请求或比较服务器响应。

此命令的模式为：curl -option1 -option2 http://example.com/url

**示例：**

`curl -svo /dev/null http://www.example.com`

`curl -svo /dev/null -A “USER_AGENT_STRING” http://www.example.com`

`curl -svo /dev/null -H “host: www.example.com” http://ORIGIN_IP`

`curl -svo /dev/null -H https://www.example.com --resolve www.example.com:443:ORIGIN_IP`

### 使用 `mtr` 和 `traceroute`

MTR 和 `traceroute` 是 Unix 命令行工具，使您能够在指定主机或目标服务器的特定网络路径中测量性能或等待时间。

**示例：**

`mtr -rwc 20 example.com -T -4`
`mtr -rwc 20 8.8.8.8 -T -6`

`traceroute example.com -T -4`

`traceroute 8.8.8.8 -T -6`

| 选项| 定义
|
|---------|-----------|
| -c | 设置发送的 ping 数量|
| -T | 强制实施 TCP traceroute（通常为 ICMP）|
| -4 | 强制使用 IPv4|
| -6 | 强制使用 IPv6|

### 生成 HAR 文件

HAR 文件是从 Web 浏览器对 HTTP 请求进行的记录。诸如 Chrome 的浏览器具有“开发者工具”部分，可帮助您设置以生成 HAR 文件。
