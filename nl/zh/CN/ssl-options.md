---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: TLS Options, secure connection, Automatic HTTPS

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# TLS 选项
{:#cis-tls-options}

利用 TLS 选项，您可以控制访问者能否通过安全连接浏览您的 Web 站点，何时浏览，以及 CIS 将如何连接到您的源服务器。

## 自动 HTTPS 重写
{:#automatic-https-rewrite}

自动 HTTPS 重写通过将 Web 站点上可使用 HTTPS 提供的所有资源或链接的“http”更改为“https”，帮助修复混合内容。此设置位于**高级**安全配置页面中。

## TLS 加密方式
{:#tls-encryption-modes}

这些选项按从最不安全（关闭）到最安全（端到端 CA 签名）顺序列出。 
 * 关闭（不推荐）
 * 客户机到边缘（边缘到源不加密，不支持自签名证书） 
 * 端到端灵活性（边缘到源证书可自签名） 
 * 端到端 CA 签名（缺省值和建议值）
 * 仅 HTTPS 源提取（仅限企业）

### 关闭 
{:#tls-encryption-modes-off}
访问者和 CIS 之间无安全连接，并且 CIS 和 Web 服务器之间无安全连接。访问者只能通过 HTTP 查看您的 Web 站点，并且尝试使用 HTTPS 进行连接的任何访问者都将收到 `HTTP 301 Redirect`，并重定向至 Web 站点的纯 HTTP 版本。

### 客户机到边缘
{:#tls-encryption-modes-client-to-edge}

访问者和 CIS 之间使用安全连接，但 CIS 和 Web 服务器之间无安全连接。您不需要在 Web 服务器上具有 TLS 证书，但访问者仍将该站点视为已启用 HTTPS。如果您的 Web 站点上有任何敏感信息，建议不要使用此选项。此设置将仅对于端口 443->80 有效。仅当您无法在自己的 Web 服务器上设置 TLS 时，才应使用其作为最后的方法。其安全性_低于_任何其他选项（甚至是“关闭”），而且会在您决定离开此方法时遇到问题。

### 端到端灵活性
{:#tls-encryption-modes-end-to-end-flexible}

访问者和 CIS 之间使用安全连接，并在 CIS 和 Web 服务器之间使用安全连接（但不进行认证）。您必须将服务器配置为至少使用自签名证书来应答 HTTPS 连接。不验证证书真实性：从 CIS 视角来看（在连接到源 Web 服务器时），其等效于绕过此错误消息。只要您的 DNS 设置中的源 Web 服务器地址正确，您就知道我们正在连接到您的 Web 服务器，而不是其他人。

### 端到端 CA 签名
{:#tls-encryption-modes-end-to-end-ca-signed}

缺省值和建议值。访问者和 CIS 之间使用安全连接，并且 CIS 和 Web 服务器之间使用安全的认证连接。您必须将服务器配置为使用有效的 TLS 证书来应答 HTTPS 连接。此证书必须由认证中心签名，并且包含未来的到期日期，并且响应请求域名（主机名）。我们建议您保持使用此 TLS 方式以获取最佳安全实践，除非您了解更改为某个不太严格的方式的潜在安全威胁。

### 仅 HTTPS 源提取
{:#tls-encryption-modes-origin-only-pull}

*仅限企业。*此方式具有与端到端 CA 签名相同的证书需求，还会将 CIS 与源 Web 服务器之间的所有连接从 HTTP 升级为 HTTPS，即使请求的源内容是通过 HTTP 传输的。

## 最低 TLS 版本
{:#minimum-tls-version}

这将针对尝试连接到站点的流量设置最低 TLS 版本。缺省情况下，这将设置为 1.0。更高的 TLS 版本提供了额外的安全性，但可能并非所有浏览器都支持。这可能导致某些客户无法连接到站点。
