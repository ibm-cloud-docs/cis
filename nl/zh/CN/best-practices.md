---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Best practices, CIS setup

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# CIS 设置的最佳实践
{:#best-practices-for-cis-setup}

由于 IBM CIS 位于网络边缘，因此需要采取几个步骤来保证与 CIS 服务的顺利集成。以下是将 CIS 与源服务器集成的一些建议的最佳做法。 

您可以在更改 DNS 并激活代理服务之前或之后执行这些步骤。这些建议使 IBM CIS 能够正确连接到源服务器。它们将帮助您防止 API 或 HTTPS 流量出现任何问题，让日志捕获到客户的正确 IP 地址，而不是保护性 CIS IP 地址。

以下是需要设置的内容：

 * 最佳实践 1：恢复客户的原始 IP
 * 最佳实践 2：合并 CIS IP 地址
 * 最佳实践 3：确保安全设置不会影响 API 流量
 * 最佳实践 4：尽可能严格地配置安全设置
 
## 最佳实践 1：了解如何恢复客户的原始 IP
{:#best-practice-know-how-to-restore-origininating-ip}

作为逆向代理，我们在以下头中提供原始 IP：

  * `CF-Connecting-IP`
  * `X-Forwarded-For`
  * `True-Client-IP`（可选）

对于如 Apache、Windows IIS 和 NGINX 等基础架构，可以使用各种工具来恢复用户 IP 地址。

## 最佳实践 2：合并 CIS IP 地址以顺利集成
{:#best-practice-incorporate-cis-ip-addresses}

可以采取以下两个步骤：

  * 除去对 CIS IP 地址的任何速率限制
  * 设置 ACL 以仅允许 CIS IP 地址和其他可信参与方

您可以在[此位置](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses)找到 IBM CIS 的 IP 范围的更新列表。

## 最佳实践 3：复审安全设置以确保其不会干扰 API 流量
{:#best-practice-review-security-settings-interference}

IBM CIS 通常通过除去连接开销来加速 API 流量。但是，缺省安全状态可能会干扰很多 API 调用。建议您执行一些操作，以防止在代理活动后干扰 API 流量。

 * 可以使用**页面规则**功能选择性地关闭某些安全功能。
   * 使用 API 的 URL 模式（例如，`api.example.com`）创建页面规则。
   * 添加以下规则行为：
     * 将**安全级别**选择为**彻底关闭**
     * 将 **TLS** 选择为**关闭**
     * 将**浏览器完整性检查**选择为**关闭**
   * 选择**供应资源**

 * 或者，可以从“安全性”页面全局关闭 **Web 应用程序防火墙**。

|*浏览器完整性检查会做什么？*| 
|------------------------------------------------|
|*浏览器完整性检查查找通常被垃圾邮件制造者所滥用的 HTTP 头。此检查会拒绝那些头访问页面时所带来的流量。它还会阻止没有用户代理或添加非标准用户代理（滥用机器人、搜寻器或 API 通常会使用此策略）的访问者。*|

## 最佳实践 4：尽可能严格地配置安全设置
{:#best-practice-configure-stict-security-settings}

CIS 提供了一些选项用于加密流量。作为逆向代理，我们会关闭数据中心的 TLS 连接，打开与源服务器的新 TLS 连接。如果与 CIS 中断连接，那么可以从帐户上传定制证书，也可以使用 CIS 供应的通配符证书，还可以同时使用这两种方法。

### 上传定制证书
{:#strict-upload-custom-cert}
 
可以在创建企业域时上传公共和专用密钥。如果上传自己的证书，那么马上就会与加密流量兼容，还会保持对证书（例如，扩展验证 (EV) 证书）的控制。请记住，如果上传定制证书，那么您将负责管理证书。例如，IBM CIS 不会跟踪证书到期日期。 
 
### 或者，使用 CIS 供应的证书
{:#strict-utilize-cert-cis-provisioned}
 
缺省情况下，IBM CIS 与多个认证中心 (CA) 建立了合作伙伴关系，为客户提供域通配符证书。设置这些证书时可能需要手动验证，您的支持团队可以帮助您执行这些额外的步骤。
 
### 将 TLS 设置更改为**端到端 CA 签名**
{:#strict-change-tls-setting}
 
大多数企业客户使用“端到端 CA 签名”安全设置。**端到端 CA 签名**设置需要在 Web 服务器上安装有效的 CA 签名证书。证书的到期日期必须为将来日期，并且必须具有匹配的 *hostname* 或*主题备用名称 (SAN)*。

