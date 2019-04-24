---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM CIS connection, CIS network connection, Origin web server, troubleshooting

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 对 CIS 网络连接进行故障诊断
{:#troubleshooting-your-cis-network-connection}

## 我如何知道自己的数据是否流经 IBM CIS 连接？
{:#how-do-i-know-if-my-data-is-passing-through-my-cis-connection}

IBM Cloud Internet Services (CIS) 使用可读取、添加或修改的 HTTP 头。该头允许我们使用 CF-Ray 编号跟踪请求的路由方式。可通过 `curl` 命令或使用 Google Chrome 插件“Claire”找到 CF-Ray 编号。

要了解数据是否流经 IBM CIS，请找到每个包中的 `Ray ID`。

**Unix 命令行工具：**

 * curl（用于 HTTP）：
`$ curl -vso /dev/null http://example.com`

 * dig（用于 DNS）：
`$ dig www.example.com`

 * traceroute（用于网络）：
`$ traceroute example.com`

**例如：
**

终端命令：`curl -svo /dev/null YOUR_URL_HERE. -L`

结果：`CF-RAY: 1ca349b6c1300da3-SJC`

## 添加 CF-Ray 头

添加 CF-RAY 头可帮助跟踪通过网络的 Web 站点请求。在与支持人员合作时将其用于帮助对与连接相关的任何问题进行故障诊断。您可以通过在 Apache 和 nginx 中对配置文件进行某些编辑，以在日志中显示此“Ray 标识”。

### Apache
{:#troubleshooting-cis-apache}

```
LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-agent}i\" %{CF-Ray}i" cf_custom

CustomLog log/access_log cf_custom
```

### nginx
{:#troubleshooting-cis-nginx}

```
log_format cf_custom '$remote_addr - $remote_user [$time_local]  '
                    '"$request" $status $body_bytes_sent '
                    '"$http_referer" "$http_user_agent" '
                    '$http_cf_ray';

access_log  /var/log/nginx/access.log cf_custom;
```

## 如何跟踪路径？
{:#how-do-i-trace-a-route}

要查看某条路径是否经过 IBM CIS 路径，您可以在 Mac 或 Linux 的终端窗口中执行“dig”，或者在 Windows 的 Windows 命令提示符中使用 `nslookup`。

如果包中包含 CF-Ray 值，那么其已流经 CIS。

`traceroute` 命令显示 IP 请求所经过的完整路径。

支持团队使用这些命令为您提供帮助。

## 如果看到隐私警告
{:#troubleshooting-cis-privacy-warning}

IBM CIS 颁发证书涵盖根域 (`example.com`) 和一个子域级别 (`*.example.com`)。如果尝试访问二级子域 (`*.*.example.com`)，那么将在浏览器中看到隐私警告，因为这些主机名未添加到 SAN 中。

另外，请允许最多 15 分钟时间以便一个合作伙伴认证中心 (CA) 发布新证书。如果新证书尚未发布，那么将在浏览器中看到隐私警告。

## 如果受到 DDoS 攻击应该怎么办？
{:#troubleshooting-cis-ddos-attack}

 * **第 1 步：**从仪表板开启“防御模式”
 * **第 2 步：**设置 DNS 记录以获取最高安全性
 * **第 3 步：**对来自 IBM CIS 的请求既不限制速率也不调速
 
在“防御模式”期间，每个新访问者都会遇到“Captcha”安全质询，必须通过才能获得无质询访问 cookie。这样，僵尸网络流量被阻止，直至关闭“防御模式”。未满足安全质询的访问者会被添加到（坏）“IP 声誉”数据库。

## 您可能遇到的其他问题
{:#troubleshooting-cis-other-problems}

以下是支持团队可能遇到的一些常见错误消息：

|错误代码    |原因|
| ------------- | ------------- |
|1001  |DNS 解析错误。客户最近已注册但尚未传播其 DNS 信息，或者正在管理 DNS 的任何人遇到故障。|
|521  |源 Web 服务器拒绝了来自 CIS 的连接。源 Web 服务器未在运行，或者某项阻止 IBM CIS IP 地址。|
|522  |与源服务器的连接超时（缺省值为 30 秒）。CIS 可能存在速率限制，Web 服务器可能耗尽所有资源（共享服务器），或者 Web 服务器与 IBM CIS 之间可能存在网络连接问题。|
|523  |无法访问源服务器。确保 DNS 记录的源 IP 地址与 CIS DNS 设置页面中显示的地址相同。|
|524  |IBM CIS 可建立 TCP 连接，但是未从 Web 服务器收到响应。长时间运行的应用程序或数据库查询造成干扰。|

### 看不到任何网络流量
{:#troubleshooting-cis-network-traffic}

如果看不到流量，并且正在使用 CNAME，确保存在重定向，因此流量不会路由至根域。请记住，某些 DNS 传播可能需要 48 小时才能完成。

### Web 站点脱机
{:#troubleshooting-cis-website-offline}

以下是您可能看到的内容：

`IBM CIS 无法连接到源服务器（错误 521、522、523）`。

**Web 站点脱机 - 无高速缓存的版本**

1. 服务器联机，但其阻止 IBM CIS 请求。
2. 源服务器脱机，并且 IBM CIS 无备份 Web 站点映像 

可执行的操作：

* 验证 IBM CIS IP 地址已列入白名单。
* 确保 IBM CIS IP 无速率限制。
* 以下是[列入白名单的 IP](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses) 列表

### 502 错误“可怕的 502”
{:#troubleshooting-cis-502-error}

此错误是您可能遇到的最常见的错误之一。通常在部分网络不可用时发生（例如，在 DDoS 攻击开始时）。特定数据中心可能暂时不可用。将重新路由流量。运行跟踪路由。 

以下是您可能看到的内容：`Error 502 - bad gateway error`

发生了什么：

* IBM CIS 网络的一部分存在问题。
* 通常，问题仅限于一个数据中心内的一台服务器。
* 仅影响一部分站点访问者。
* IBM CIS 技术运营团队将处理这些问题。

可执行的操作：

* 将 `www.YOUR_DOMAIN.com/cdn-cgi/trace` 中的结果以凭单形式发送给[支持](/docs/get-support?topic=get-support-getting-customer-support).
* 暂时将 DNS 记录切换为关闭（无代理）。

