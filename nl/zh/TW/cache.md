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

# 快取概念
{:#caching-concepts}

此文件包含快取的一些相關概念及定義，以及它對 IBM CIS 部署的影響。

## 何謂快取？
{:#what-is-caching}

快取是在邊緣伺服器上儲存檔案的處理程序，這麼做的目的是改善將這些檔案提供給客戶時的回應時間。透過將檔案儲存至更接近客戶的位置，即可縮短資料在網路中串流所需的時間，這通常稱為**延遲**。

已快取的檔案具有指定的有效期限，即**存活時間 (TTL)**，在該時間之後就會從快取中清除它們。也可以手動從快取中清除檔案。從快取中移除檔案之後，CIS 會回到原點伺服器以重新載入您的檔案，並使用最新版本來更新快取。

您可以在[快取及頁面規則指導教學](/docs/infrastructure/cis?topic=cis-use-page-rules-with-caching)中找到快取設定及快取選項的更深入說明。

### 快取的內容？
{:#what-content-is-cached}

依預設，我們會快取**靜態檔案**，其中包括許多類型的影像及文字檔（非 HTML 檔案）。這僅包括來自您網站的檔案，而不包括來自社交網站的協力廠商資源等等。此外，我們目前不會透過 MIME 類型進行快取。

### 如何快取 HTML？ 
{:#how-do-i-cache-html}

依預設，我們不會快取 HTML 檔案，因為我們不認為它們是靜態的；不過，如果靜態 HTML 可以與動態 HTML 明確區分，則能夠[使用頁面規則特性](/docs/infrastructure/cis?topic=cis-use-page-rules)來快取 HTML 檔案。


## 查詢字串排序
{:#query-string-sorting}

**僅限企業**：CIS 會將具有不同順序之查詢字串的 URL 視為快取中的個別檔案。這表示如果有一位使用者要求：

`/video/123456?title=0&byline=0&portrait=0&color=987654`

而另一位使用者要求：

`/video/123456?byline=0&color=987654&portrait=0&title=0`

CIS 會回到原點，即使我們的快取中已有該檔案也一樣。

「查詢字串排序」會在查詢字串命中快取_之前_ 將查詢字串排序，這可導致較高的快取命中率。請使用**快取**頁面中的切換，啟用「查詢字串排序」。

## 提供過時內容
{:#serve-stale-content-caching}

如果伺服器關閉，則保持網站的有限版本上線。即使內容過期，當原點伺服器離線時，CSI 仍將繼續提供快取內容給使用者。
