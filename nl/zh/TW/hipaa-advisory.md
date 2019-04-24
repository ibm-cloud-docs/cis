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

# HIPAA 諮詢
{:#hipaa-advisory}

**禁止**對控管資料（例如，PHI、ITAR）使用快取 (CDN)。所有使用 CIS 的控管資料流程都必須設為**非快取**。
{:important}

CIS CDN 可以利用多種方式來停用內容快取。 
- 原點伺服器可以在管控內容的 **Cache-Control** 標頭中設定 **no-cache**
- 使用「CIS 頁面規則」可停用指定路徑上任何內容的快取，即使原點未傳送 **Cache-Control** 標頭 **no-cache** 也一樣。 
