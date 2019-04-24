---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM CIS deployment, query strings, HTML files

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# 高速缓存概念
{:#caching-concepts}

本文档包含一些与高速缓存相关的概念和定义，描述了高速缓存如何影响 IBM CIS 部署。

## 什么是高速缓存？
{:#what-is-caching}

高速缓存是在我们的边缘服务器上存储文件的过程，用于缩短向客户提供这些文件时产生的响应时间。通过将文件存储在更靠近客户的位置，可以缩短数据在网络中传送所需的时间，即通常所说的**等待时间**。

高速缓存文件具有指定的到期时间，即，**生存时间 (TTL)**，在此时间之后将从高速缓存中清除这些文件。也可以从高速缓存中手动清除这些文件。从高速缓存除去这些文件后，CIS 将返回到源服务器以重新装入文件，并使用最新版本更新高速缓存。

可以在[高速缓存和页面规则教程](/docs/infrastructure/cis?topic=cis-use-page-rules-with-caching)中找到高速缓存设置和高速缓存选项的更详细说明。

### 高速缓存了哪些内容？
{:#what-content-is-cached}

缺省情况下，我们会高速缓存**静态文件**，其中包含许多类型的图像和文本文件（非 HTML 文件）。这仅包含来自 Web 站点的文件，而不包含来自社交网络站点的第三方资源等。此外，我们目前不会按 MIME 类型进行高速缓存。

### 如何高速缓存 HTML？ 
{:#how-do-i-cache-html}

缺省情况下，不会高速缓存 HTML 文件，因为它们被视为非静态文件；但是，如果静态 HTML 与动态 HTML 可以明确区分开，那么可以[使用“页面规则”功能](/docs/infrastructure/cis?topic=cis-use-page-rules)对 HTML 文件进行高速缓存。


## 查询字符串排序
{:#query-string-sorting}

**仅限企业** CIS 将具有不同顺序的查询字符串的 URL 视为高速缓存中的单独文件。这意味着，如果一个用户请求以下内容：

`/video/123456?title=0&byline=0&portrait=0&color=987654`

而另一个用户请求以下内容：

`/video/123456?byline=0&color=987654&portrait=0&title=0`

那么 CIS 将返回到源，尽管在高速缓存中有该文件。

“查询字符串排序”在命中高速缓存_之前_对查询字符串进行排序，从而实现更高的高速缓存命中率。使用**高速缓存**页面中的切换开关来启用查询字符串排序。

## 提供旧内容
{:#serve-stale-content-caching}

如果服务器宕机，保持有限版本的站点联机。在源服务器脱机时，即使内容已到期，CIS 也将继续向用户提供高速缓存的内容。
