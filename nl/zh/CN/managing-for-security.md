---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-26"

keywords: IBM CIS, optimal security, Security Level

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# 管理 IBM CIS 以获取最佳安全性
{:#manage-your-ibm-cis-for-optimal-security}
IBM Cloud Internet Services (CIS) 安全设置包括安全缺省值，旨在避免误报和对流量造成负面影响。但是，这些安全缺省设置不会为每个客户提供最佳安全态势。请执行以下步骤以确保以安全的方式配置您的 CIS 帐户。

**建议和最佳实践：**

* 通过代理和增加模糊来保护源 IP 地址
* 有选择地配置安全级别
* 安全地激活 Web 应用程序防火墙 (WAF)

## 最佳实践 1：保护源 IP 地址
{:#best-practice-secure-origin-ip-address}

使用 IBM CIS 代理子域时，所有流量都将受到保护，因为我们使用特定于 IBM CIS 的 IP 地址进行主动响应（例如，所有客户机首先连接到 CIS 代理，而源 IP 地址会被隐藏）。

### 对于来自源的所有 HTTP(S) 流量，将 IBM CIS 代理用于所有 DNS 记录
{:#use-cis-proxies-for-dns-records}

为提高源 IP 地址的安全性，应通过代理传递所有 HTTP(S) 流量。

**看到不同的自己 - 查询不使用代理和使用代理的记录：**

```
$ dig nonproxied.theburritobot.com +short
1.2.3.4 (The origin IP address)

$ dig proxied.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (CIS IP addresses)
```

### 使用非标准名称来隐藏不通过代理传递的源记录
{:#obsure-non-proxied-origin-records-with-non-standard-names}
可通过创建额外的模糊来保护无法通过 IBM CIS 进行代理的记录和仍使用源 IP 地址的记录（例如，FTP）。特别是，如果需要无法由 IBM CIS 进行代理的源的记录，请使用非标准名称。例如，不使用 `ftp.example.com`，而是使用 `[random word or-random characters].example.com`。通过此模糊处理，DNS 记录的字典扫描就更不容易公开源 IP 地址。

### 对于 HTTP 和非 HTTP 流量使用单独的 IP 范围（如果可能）
{:#use-separate-ipranges-for-traffic}
一些客户对于 HTTP 和非 HTTP 流量使用单独的 IP 范围，从而允许通过代理传递指向其 HTTP IP 范围的所有记录，并使用其他 IP 子网来隐藏所有非 HTTP 流量。

## 最佳实践 2：有选择地配置安全级别
{:#best-practice-configure-security-level-selectively}
您的**安全级别**确定 **IP 声誉数据库**的敏感度。为避免负面交互或误报，请按域配置**安全级别**以在需要的位置提高安全性，在适当的位置降低安全性。

### 将敏感区域的安全级别提高到“高”
{:#increase-security-level-for-sensitive-areas}
您可以针对域从“高级安全性”页面增加此设置，或者通过为管理页面或登录页面添加**页面规则**来增加此设置，从而减少暴力攻击尝试：

1. 使用 API 的 URL 模式创建**页面规则**（例如，`www.example.com/wp-login`）。 
2. 找到**安全级别**设置。
3. 将设置标记为**高**。
4. 选择**供应资源**。

### 降低非敏感路径或 API 的安全级别以减少误报
{:#decrease-security-level-non-sensitive-paths-reduce-false-positives}
对于常规页面和 API 流量，可以降低此设置： 

1. 使用 API 的 URL 模式创建**页面规则**（例如，`www.example.com/api/*`）。
2. 找到**安全级别**设置。
3. 将“安全级别”设为**低**或**基本关闭**。
4. 选择**供应资源**。

### “安全级别”设置意味着什么？
{:#what-do-security-level-settings-mean}
“安全级别”设置与特定 IP 地址因网络恶意行为而得到的威胁评分保持一致。高于 10 的威胁评分被视为高。

* **高**：如果威胁评分大于 0，将进行质询。
* **中**：如果威胁评分大于 14，将进行质询。
* **低**：如果威胁评分大于 24，将进行质询。
* **基本关闭**：如果威胁评分大于 49，将进行质询。
* **关闭**：*仅限企业* 
* **受到攻击**：仅应在 Web 站点遭受 DDoS 攻击时使用。在 CIS 分析流量和行为以确保是合法访问者在尝试访问 Web 站点时，访问者会收到一个显示约 5 秒的空隙页面。**受到攻击**可能影响域上的某些操作，例如，使用 API。您可以通过为该部分创建页面规则，从而设置 API 或域的任何其他部分的定制安全级别。

建议您定期检查“安全级别”设置，并且您可在[《CIS 设置的最佳实践》文档](/docs/infrastructure/cis?topic=cis-best-practices-for-cis-setup)中找到指示信息

## 最佳实践 3：安全地激活 Web 应用程序防火墙 (WAF)
{:#best-practice-activate-waf-safely}
**安全**部分中提供 WAF。我们将按照相反顺序遍历这些设置，从而确保将 WAF 配置为尽可能安全，然后再在整个域中启用。这些初始设置通过填充**安全性事件**来进一步调优，从而减少误报。WAF 将自动进行更新以处理发现的新漏洞。

WAF 保护您免受以下类型的攻击：
* SQL 注入攻击
* 跨站点脚本编制
* 跨站点伪造

WAF 包含一个缺省规则集，该规则集包含用于停止最常见攻击的规则。此时，我们允许您启用或禁用 WAF，并微调 WAF 规则集内的特定规则。请参阅[《WAF 缺省规则集》](/docs/infrastructure/cis?topic=cis-waf-default-rule-set)文档，以了解有关缺省规则集和每个规则的行为的更多详细信息。

有关 WAF 的更多信息，请参阅[《WAF 概念》文档](/docs/infrastructure/cis?topic=cis-web-application-firewall-concepts-q-a)

## 最佳实践 4：配置 TLS 设置
{:#best-practice-configure-tls-settings}
IBM CIS 提供一些用于加密流量的选项。作为逆向代理，我们会关闭数据中心的 TLS 连接，并打开与源服务器的新 TLS 连接。

TLS 提供四种操作方式：
* **关闭**：在此方式下禁用 TLS，建议不要这样做。
* **客户机到边缘**：TLS 加密从 CIS 到客户机的流量，但是不加密从 CIS 到源服务器的流量。
* **端到端灵活**：TLS 加密所有流量；但是，您可以使用自签名证书来保护 CIS 和源服务器之间的流量。
* **端到端 CA 签名**：TLS 加密所有流量；您必须使用 CA 签名的证书。

有关 TLS 选项的更多详细信息，请参阅[此文档](/docs/infrastructure/cis?topic=cis-tls-options)。

IBM CIS 允许您使用定制证书，也可以使用由 CIS 为您供应的通配符证书。

### 上传定制证书
{:#upload-custom-certs}
您可以通过单击**添加证书**按钮并输入证书、专用密钥和捆绑方法来上传自己的定制证书。如果上传自己的证书，那么马上就会与加密流量兼容，还会保持对证书（例如，扩展验证 (EV) 证书）的控制。请记住，如果上传定制证书，那么您将负责管理证书。例如，IBM CIS 不会跟踪证书到期日期。 

![custom-certificate](images/upload-custom-certificate.png)

### 订购专用证书
{:#order-dedicated-certs}
CIS 通过提供专用证书来方便证书的管理。您不再需要生成专用密钥、创建证书签名请求 (CSR) 或记住更新证书。您可以通过单击**添加证书**按钮并订购通配符证书或输入主机名以订购专用定制证书来订购专用证书。证书类型为：

 * 使用 P-256 密钥的 SHA-2/ECDSA 签名证书， 
 * 使用 RSA 2048 位密钥的 SHA-2/RSA 签名证书，和 
 * 使用 RSA 2048 位密钥的 SHA-1/RSA 签名证书。 
 
CIS 可针对所有 TLD 发出，但 `.cu`、`.iq`、`.ir`、`.kp`、`.sd`、`.ss` 和 `.ye` 除外。CIS 管理到期日期。要编辑专用定制证书上的主机名，必须重新订购，然后删除。例如，使用主机名 `alpha.yourdomain.com` 订购专用定制证书。要向专用定制证书添加主机名 `beta.yourdomain.com`，请使用主机名 `alpha.yourdomain.com` 和 `beta.yourdomain.com` 订购另一个专用定制证书。此后，您_必须_删除原始专用定制证书。

第一次订购专用证书时，发生“域控制验证”(DCV) 过程，这将生成对应的 TXT 记录。如果删除 TXT 记录，那么在订购另一个专用证书时，DCV 过程将再次发生。如果删除专用证书，那么不会删除与 DCV 过程对应的 TXT 记录。
{:note}

下面是订购专用证书时常见的错误：
* `连接到证书服务时出错。`
* `从证书服务进行请求时出错。`
{:note}

如果在订购证书时收到错误，请刷新页面并重试。

![dedicated-certificate](images/order-dedicated-certificate.png)

### 利用供应的证书
{:#utilize-provisioned-certificate}
IBM 已与多个认证中心 (CA) 合作，为客户提供域通配符证书。设置这些证书可能需要手动验证。您的支持团队可以帮助您执行这些额外的步骤。

### 边缘的证书优先级
{:#certificate-prioirity-at-our-edge}
在边缘显示证书的优先级为：
1. 上传的定制
2. 专用定制
3. 专用通配符
4. 通用

### 最低 TLS 版本
{:#security-minimum-tls-version}
请参阅[最低 TLS 版本](/docs/infrastructure/cis?topic=cis-tls-options#minimum-tls-version)。较高级别的 TLS 提供更高的安全性，但是可能阻止客户连接到站点。