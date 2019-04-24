---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIDR blocks, Whitelist Block Challenge, IBM Cloud Internet Services, security features

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# IBM Cloud Internet Services (CIS) 如何确保工作安全
{:#how-cis-keeps-your-work-secure}

IBM CIS 是全球分布式云服务，可阻止威胁并限制滥用机器人和搜寻器，而这些可能浪费您的带宽和服务器资源。IBM CIS 充当全球 HTTP(S) 逆向代理和受管 DNS 服务提供者。您的 Web 流量将流经我们的智能全球网络以优化性能和安全性。

![security-graphic.png](images/security-graphic.png)

以下是功能简要概述：

## 安全性功能
{:#cis-security-features}

 * 代理 [DNS 记录](/docs/infrastructure/cis?topic=cis-dns-concepts#proxying-dns-records)或 [GLB](/docs/infrastructure/cis?topic=cis-global-load-balancer-glb-concepts) 以使用安全功能。这允许流量流经我们的服务器，并且可以监视数据。
### Web 应用程序防火墙 (WAF)
{:#cis-web-application-firewall}

 * 通过两个规则集实施 WAF：[OWASP](/docs/infrastructure/cis?topic=cis-owasp-rule-set-for-waf) 和 [CIS](/docs/infrastructure/cis?topic=cis-waf-settings#cis-rule-set-for-waf)。
### 无限制 DDoS 缓解
{:#cis-unlimited-ddos-mitigation}

 * DDoS 缓解通常是昂贵的服务，在遭受攻击时成本可能增加。我们包含使用 CIS 的无限制 DDoS 缓解，而无需额外成本。

## 安全标准和平台
{:#security-standards-and-platform}

 * TLS（SHA2 和 SHA1）
 * IPv6
 * HTTP/2 和 SPDY

## DNS
{:#cis-dns}

 * 全球 anycast 网络
 * DNSSEC

## 网络攻击和缓解
{:#network-attacks-and-mitigation}

我们看到的攻击一般可以分为两个类别

|第 3 层或第 4 层攻击|第 7 层攻击|
|------------------------------|-----------------|
|这些攻击包括 ISO 第 3 层（网络层）流量攻击，例如，ICMP flood，或者第 4 层（传输层），例如，TCP SYN flood 或所谓 UDP flood|这些攻击会发送恶意 ISO 第 7 层请求（应用程序层）例如，GET flood。|
|在边缘自动阻止|我们通过“防御模式”、WAF 和“安全级别”设置来处理这些攻击|

## IP 防火墙
{:#cis-ip-firewall}

IBM Cloud Internet Services 提供多个工具来控制流量，以便可针对流量、特定请求者组和特定请求 IP 保护您的域、URL 和目录。此部分详细描述了可用工具。

### IP 规则
{:#cis-ip-rules}

IP 规则允许您控制特定 IP 地址、IP 范围、特定国家或地区、特定 ASN 和特定 CIDR 块的访问权。针对入局请求的可用操作包括：
  * 白名单 
  * 阻止 
  * 质询（验证码） 
  * JavaScript 质询（IUAM 质询）

例如，如果您注意到特定 IP 导致恶意请求，那么您可以按 IP 地址阻止该用户。

### 用户代理阻止规则
{:#user-agent-blocking-rules}

“用户代理阻止”规则允许对选择的任何“用户代理”字符串执行操作。此功能的工作方式类似于先前描述的“域锁定”，但此阻止会检查入局“用户代理”字符串而不是 IP。您还可以选择如何使用 IP 规则（阻止、质询和 JS 质询）中所建立的相同操作列表来处理匹配请求。请注意，“用户代理阻止”适用于整个区域。您无法以针对“域锁定”的相同方式来指定子域。

此工具很适合用于阻止您认为可疑的任何“用户代理”字符串。 

### 域锁定
{:#cis-domain-lockdown}

“域锁定”允许将特定 IP 地址和 IP 范围列入白名单，这样所有其他 IP 都将列入黑名单。“域锁定”支持：

  * 特定子域。例如，您可以允许 IP `1.2.3.4` 访问域 `foo.example.com`，并允许 IP `5.6.7.8` 访问域 `bar.example.com`，而不一定允许逆向操作。
  * 特定 URL。例如，您可以允许 IP `1.2.3.4` 访问目录 `example.com/foo/*`，并允许 IP `5.6.7.8` 访问目录 `example.com/bar/*`，但不一定允许逆向操作。
当您需要更细粒度的访问规则时，此功能非常有用，因为通过 IP 规则，您可以将阻止应用于当前域的所有子域或帐户上的所有域，但无法指定 URI。

### 质询通过
{:#cis-challenge-passage}

此设置位于**高级**安全设置中，允许您控制通过质询或 JavaScript 质询的访问者在再次被质询前可访问您站点的时间长度。这基于访问者的 IP，因此不适用于 WAF 规则提供的质询，因为它们基于用户在站点上执行的操作。

### 浏览器完整性检查
{:#cis-browser-integrity-check}

此设置位于**高级**安全设置中。浏览器完整性检查会查找通常被垃圾邮件制造者所滥用的 HTTP 头。此检查会拒绝那些头访问页面时所带来的流量。它还会阻止或质询没有用户代理或添加了非标准用户代理（滥用机器人、搜寻器或 API 通常会使用此策略）的访问者。
