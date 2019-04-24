---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Page Rule Use, Cache-Tag Purge, web content

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# 管理 CIS 部署以取得最佳效能
{:#manage-your-cis-deployment-for-best-performance}

IBM Cloud Internet Services (CIS) 可為您的客戶提供最快速體驗，因為它會將您的映像檔最佳化，並且會盡可能地讓您的 Web 內容儲存位置更接近一般使用者。您的內容是從 Proxy 邊緣伺服器載入（這可減少延遲）。

使用 IBM CIS，您可以利用最佳作法進一步加強網站的效能，從而加速載入 Web 內容。下列一些特定最佳作法可加強 CIS 內 Web 內容的效能。

**建議及最佳作法：**

 * 盡可能地快取最多的靜態及半靜態 Web 內容
 * 針對事件驅動的內容，使用 API 清除快取
 
## 最佳作法 1：盡可能地快取最多的靜態及半靜態內容
{:#best-practice-cache-static-content}

  * 針對靜態 HTML 網頁啟用**快取所有項目**
  * 針對偶而變更的內容，使用保守的**存活時間 (TTL)**

### 針對偶而變更的內容，利用保守的 TTL（存活時間）
{:#utilize-conservative-ttl}

如果內容很少變更，則您可以設定保守的 TTL，盡可能地利用我們的快取。如果您有高百分比的重新驗證要求，則可以增加內容的 TTL，而不會對您的客戶造成負面影響。更有效地使用快取，即會增加效能，因為您較不常重新驗證。

### 如何分辨是否正在快取項目？
{:#how-do-i-tell-if-items-are-being-cached}

IBM CIS 在嘗試快取物件時會新增回應標頭 `CF-Cache-Status`。如果快取順利完成，則此標頭的值會使用下列其中一個關鍵字指出其狀態：

* **MISS：**資產還不在快取中，或 TTL 已過期（亦即，它已達到 cache-control 最大存在時間 0）。
* **HIT：**已從快取中遞送資產。
* **EXPIRED：**已從快取中遞送資產，但下一個要求需要重新驗證。
* **REVALIDATED：**已從快取中遞送資產。TTL 已過期，但原點的 `If-Modified-Since` 要求指出尚未變更資產。因此，會將快取中的版本再次視為有效。

## 最佳作法 2：針對事件驅動的內容，使用 API 清除快取
{:#best-practice-api-purge-cache}

例如，每次將新貼文新增至您的部落格時，您可以使用 API 指令輕鬆地清除 CIS 快取。經常會看到事件驅動的內容，而且可以輕易地確保您的使用者不會收到過時內容。接下來會列出跨整個廣域網路立即清除快取的指令。您可以使用我們的快取應用程式，也可以使用 API。

  * 使用 Cache-Tag 清除快取
  * 廣域地清除快取
  * 透過頁面規則清除快取
  * 使用進階快取特性

### 透過 Cache-Tag 清除快取
{:#purge-cache-by-cache-tag}

Cache-Tag 可讓您定義要清除之內容的儲存區。結合經常一起變更的物件是一種絕佳的方法。因此，可以將 HTML 部落格文章（舉例來說）及其所有影像內容標記在一起。您也可以使用 Cache-Tag 來組合 Mobile-only 內容，以在將新的更新推送至行動網域時清除所有項目。

### 廣域地清除快取
{:#purge-cache-globally}

您也可以選擇將整個快取強制成重新驗證。您可以重設快取中所儲存的所有物件，以將每個要求都遞送至原點伺服器。

### 透過頁面規則清除快取
{:#purge-cache-by-page-rule}

「頁面規則」可讓您根據正規表示式來清除整個快取。您可以利用預先定義的「頁面規則」，並重新驗證對該「頁面規則」的所有點閱。您最多可以為每個頁面建立 50 個「頁面規則」。

### 使用進階快取特性
{:#use-advanced-caching-features}

**略過 Cookie 上的快取：**此特性已配置於「頁面規則」，除非有特定名稱的 Cookie，否則可讓您提供快取的物件。例如，除非您發現指出客戶已登入的 `SessionID` Cookie，否則您可以提供快取版本的首頁，因此應該呈現個人化內容。
