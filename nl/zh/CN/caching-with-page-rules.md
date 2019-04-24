---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Use Page Rules, standard cache levels, Custom Caching Sets

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# 将页面规则与高速缓存配合使用
{:#use-page-rules-with-caching}

页面规则使您能够根据页面的 URL 来执行各种操作，例如，创建重定向、微调高速缓存行为，或者启用和禁用服务。

如果给定的 URL 模式与以下格式匹配，页面规则就会生效：

`<scheme>://<hostname><:port>/<path>`

例如：


`https://www.example.com:80/image.png`

`scheme` 和 `port` 部分是可选的。如果省略 `scheme` 部分，那么格式接受 `http://` 和 `https://` 协议。如果未指定 `port`，那么规则与所有端口匹配。您可以通过在规则模式中使用 `*` 符号来执行基本通配符匹配，从而使其与一系列相似模式匹配。

**有关页面规则的重要事项：**

 * 对于任何给定请求，仅会有一个页面规则生效。
 * 将按从上到下的顺序为页面规则设定优先级。只要 URL 与某个规则匹配，就会只应用这一规则；也就是说，如果已在请求上触发了一个页面规则，那么即使有任何后续规则与该 URL 模式匹配，也不会生效。 
 * 我们建议的规则排列顺序是从最具体到最不具体，这是一般准则。
 * 可以禁用页面规则，在此情况下，页面规则将不执行任何操作，但仍可在列表中显示且可进行编辑。如果将*已启用*开关设置为“关闭”，就会创建一个初始状态为禁用的页面规则。


## 转发（URL 重定向）
{:#forwarding-url-redirection}

使用 HTTP 301 或 302 重定向将一个 URL 重定向到另一个 URL。可以使用 `$X` 语法引用 URL 中通配符匹配的任何部分的内容。`X` 指示模式中的 glob 的索引：`$1` 将替换为第一个通配符匹配项，`$2` 替换为第二个通配符匹配项，依此类推。

例如，假设设置以下规则：

![image](images/url-redirection-example.png)

此处，对 `www.example.com/stuff/things` 的请求将重定向到 `http://example.com/stuff/things`。

请注意，不要创建域指向其自身作为目标的重定向。此错误可能导致无限重定向错误，并且受影响的 URL 将无法解析。
{:note}


## 重定向到 HTTPS
{:#redirecting-to-https}

如果要重定向访问者以使用 HTTPS，请改为使用**始终使用 HTTPS** 设置：

![image2](images/url-matching-patterns.png)


## 定制高速缓存
{:#custom-caching}

使用任何标准高速缓存级别，为任何与“页面规则”模式相匹配的 URL 设置高速缓存行为。将**高速缓存级别**设置为**高速缓存所有内容**，会对任何内容进行高速缓存，即使此内容不是缺省静态文件类型之一也是如此。将**高速缓存级别**设置为**绕过**可阻止在该 URL 上进行高速缓存。

使用页面规则指定高速缓存级别时，可以设置**边缘高速缓存 TTL**，这可控制 CIS 在高速缓存中保留文件多长时间。

**浏览器高速缓存 TTL** 控制客户机浏览器高速缓存的资源保持有效的时间长度。如果浏览器再次请求资源且 TTL 未到期，那么浏览器会收到 `HTTP 304 (Not Modified)` 响应。可以设置范围为 30 分钟到 1 年的 TTL。

并非所有缺省高速缓存行为都严格符合 RFC。通过“页面规则”设置**源高速缓存控制**，会使用一组较新的高速缓存规则，此组规则旨在更严格地遵循 RFC，尤其在重新验证方面。例如，`max-age=0` 的缺省行为是完全不高速缓存，而设置**源高速缓存控制**则会高速缓存，但会始终重新验证。

以下示例设置页面规则来高速缓存在 `/images` 文件夹中找到的所有内容。在用户浏览器中，高速缓存的资源在 30 分钟后到期，在 IBM CIS 数据中心，是一天后到期：

![image3](images/url-example.png)

**提供旧内容**提供高速缓存中的页面，即使服务器停止运行也是如此。访问者将看到站点的有限版本，以及处于脱机浏览方式的消息。 

此功能会返回 HTTP 状态 503。当服务器再次联机时，CIS 会无缝地使访问者进入正常浏览。

如果请求的页面不在高速缓存中，那么访问者会看到错误页面，通知他们请求的页面处于脱机状态。如果启用**高速缓存所有内容**页面规则并且到期时间设置为低于高速缓存频率，那么会按照相应的时间间隔清除**提供旧内容**。
{:note}
