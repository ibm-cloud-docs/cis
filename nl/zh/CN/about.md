---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Caching, IBM Cloud Internet Services, Web Application Firewall

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 

# 关于 IBM Cloud Internet Services (CIS)
{:#about-ibm-cloud-internet-services-cis}

基于 Cloudflare 技术的 IBM Cloud Internet Services (CIS) 针对在 IBM Cloud 上运行业务的客户，提供快速、高性能、安全可靠的因特网服务。   

IBM CIS 通过提供缺省值，让您快速实现各个功能，可以使用 API 或 UI 轻松更改这些缺省值。以下是一些经常更改的参数：

 * **DNS 设置**：可以使用 IBM CIS 托管 DNS 或者创建 CNAME 记录。
 * **加密设置 (TLS)**：缺省值为`灵活`方式，此方式对主机与 IBM CIS 边缘服务器之间的连接进行加密，但不会对 IBM CIS 边缘服务器与源服务器之间的通信进行加密。

## Web 应用程序防火墙 (WAF)
{:#about-waf}

IBM CIS 提供 Web 应用程序防火墙 (WAF) 功能，该功能检查 Web 流量以发现可疑活动。此功能可根据规则集自动过滤不合法的流量，以查看基于 GET 和基于 POST 的 Web 请求。可以使用各种规则集来确定要阻止、质询或允许的流量。WAF 可以阻止评论垃圾邮件、跨站点脚本编制攻击和 SQL 注入。

您可以随意启用或禁用 WAF。建议始终启用。

## 防止 DDoS 攻击
{:#ddos-protection}

IBM CIS 在 Web 站点与攻击者之间提供 DDoS 保护，与攻击的规模或持续时间无关。

## 负载均衡
{:#about-load-balancing}

IBM CIS 负载均衡在授权 DNS 级别进行操作。此功能整合了高级运行状况检查，以监视源的运行状况，并动态调整 DNS 响应。此外，还可以为全局负载均衡 (GLB) 配置地理策略。

### 运行状况检查
{:#about-health-checks}

负载均衡运行状况检查通过定期 HTTP 或 HTTPS 请求在特定 URL 上执行，并使用可定制时间间隔、超时和状态码进行配置。当源服务器被标记为运行不正常时，就会使用快速故障转移路由将访问者从故障点路由到其他位置。
 
### 地理策略和全局负载均衡 (GLB)
{geo-policies-and-glb}

使用地理策略，可根据给定客户机的地理位置来控制将此客户机定向到的源服务器。例如，可以配置地理策略，以便将欧洲访问者发送到您 Web 站点或应用程序的最近欧洲源服务器，将美国访问者发送到北美源服务器等。

## 高速缓存
{:#about-caching}

通过高速缓存这种方法，可以将静态 Web 内容存储在离站点访问者最近的地方，因此可大大提高 Web 站点的性能。我们的交付环境分布在全球各地，这样 Web 内容所有者就可以在世界各地提供无缝体验。  
 
## 使用 TLS 加密
{:#encryption-with-tls}

使用传输层安全性 (TLS) 加密与 Web 站点之间的通信。在站点处于活动状态后，最多需要 24 小时，会发布新证书。

您可以在[常见问题及解答](/docs/infrastructure/cis?topic=cis-faq)中找到有关 TLS 的更多信息。
