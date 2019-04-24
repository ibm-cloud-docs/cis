---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Advisory, Use of Caching, content caching, Cache-Control header

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# HIPAA Advisory
{:#hipaa-advisory}

**禁止**将高速缓存 (CDN) 用于受管控数据（例如，PHI 和 ITAR）。所有使用 CIS 的受管控数据流必须设置为**不高速缓存**。
{:important}

可通过多种方式按 CIS CDN 禁用内容高速缓存。 
- 源服务器可在 **Cache-Control** 头中针对受管控内容设置 **no-cache**。
- 使用“CIS 页面规则”以禁用指定路径上任何内容的高速缓存，即使源不发送 **no-cache** **Cache-Control** 头。 
