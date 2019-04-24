---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: health checks, Free Trial plan, dedicated certificate, known issues

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 
{:note: .note} 
{:important: .important} 
{:deprecated: .deprecated} 
{:generic: data-hd-programlang="generic"}

# 已知限制
{:#known-limitations}

 * 建议使用 Chrome。
 
 * 免费试用套餐限制为每个帐户一个实例。创建资源实例并向其添加域后，不允许为 CIS 添加新资源实例。即使您删除了一个试用域，然后再次尝试将域添加到同一资源实例，也会强制实施此限制。如果您尝试这样做，那么会遇到错误。

 * 对于此服务，仅支持使用来自其他提供者的 NS 记录进行子域委派。不支持 CNAME 委派。
  
 * 无法代理 A、AAAA 和 CNAME 通配符记录 (*)。

 * 删除专用证书时，在删除完成前的短时间内，它可能会在列表中再次显示。
 
 * 要在订购后修改定制专用证书的主机名，必须订购新证书，然后删除旧证书。 
 
 * 使用两字母国家或地区代码创建的 IP 规则只能使用`质询`操作来生成。如果要阻止来自某个国家或地区的访问者，请升级到企业套餐或在服务器上设置规则以完全阻止。

## 全局负载均衡器
{:#known-limitations-glb}

 * Cloud Internet Services 允许在负载均衡器主机名中使用字符 `_`，但是，Kubernetes 集群无法使用 `_`。 

 * 标准套餐最多允许 5 个负载均衡器、池和运行状况检查。每个池总共可以有 6 个源，但是在每个 CIS 实例中，仅允许 6 个唯一源。

* 无法过滤已删除的池和源的运行状况检查事件，它们仍将显示在表中。

* 如果按`池运行状况`过滤运行状况检查事件，那么将包含`已降级`的池，因为它们在技术上运行正常，但是可能包含 1 个或多个处于临界状态的源。

* 在针对运行状况检查添加请求头名称时，使用 `Host`。将小写 `host` 用于运行状况检查会失败。

## DNS
{:#known-limitations-dns}

 * 导出 DNS 记录包含应隐藏的 Cloudflare CNAME 记录。这些记录以 `_` 开头并且通常具有同名但除去 `_` 的另一个记录。
   ```
   示例
   _cf.generate.yourdomain.com 0	IN	CNAME address.alias.com
   cf.generate.yourdomain.com 0	IN	CNAME address2.alias.com
   ```
 
   必须从区域文件中除去这些记录才能正确导入。
 
 * 导出 CAA DNS 记录无法正常工作。`<tag>` 和 `<value>` 采用十六进制编码。 
 
    CAA `<flags>` `<tag>` `<value>`
  {:note}
   ```
   示例
   原始 CAA 记录
   caa.yourdomain.com.	1	IN	CAA	0 issue "letsencrypt.org"
 
   导出的 CAA 记录
   caa.yourdomain.com.	1	IN	CAA	0 6973737565 "6c657473656e63727970742e6f7267"
   ```
   必须在导入前将这些记录从十六进制转换为字符串或者除去并手动添加。

## 页面规则
{:#known-limitations-pagerules}

   * 如果页面规则标识未包含在更新的 JSON 字符串或 JSON 文件中，那么使用 IBM Cloud CLI 的 CIS 插件更新页面规则设置可能导致错误。要解决此问题，请使用页面规则的完整 JSON 配置文件（包含标识）提交更新。
   * 使用 CIS UI 除去页面规则设置可能不会除去设置，尽管 UI 会报告成功更新。要解决此问题，请使用 IBM Cloud CLI 的 CIS 插件来除去设置，并在 JSON 更新文档中包含页面规则标识：
      ```
      $> ibmcloud cis page-rule-update <domain-id> <rule-id> -j <file>
      ```
      JSON 文件应包含完整的页面规则配置（包含标识）以及必需的更新。
