---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM Cloud Internet Services, CIS Activity Tracker events

subcollection: cis

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# CIS {{site.data.keyword.cloudaccesstrailshort}} 事件
{: #at_events}

使用 {{site.data.keyword.cloudaccesstrailfull}} 服務來追蹤使用者及應用程式如何與 {{site.data.keyword.cloud}} 中的 IBM Cloud Internet Services (CIS) 互動。
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} 服務可記錄由使用者起始的活動，而這些活動會變更 {{site.data.keyword.cloud_notm}} 中的服務狀態。如需相關資訊，請參閱 [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla)。




## 事件清單：DNS 網域
{: #events_dns_domain}

下表列出與 DNS 網域相關並產生事件的動作：

|動作   |說明|
|---|---|  
|internet-svcs.zones.create|建立 DNS 網域。|
|internet-svcs.zones.update|更新 DNS 網域。|
|internet-svcs.zones.delete|刪除 DNS 網域。|
|internet-svcs.zones.activation_check.update|對 DNS 網域執行啟動檢查。|
|internet-svcs.zones.dnssec.update|對 DNS 網域啟用或停用 DNSSEC。|

## 事件清單：DNS 記錄
{: #events_dns_record}

下表列出與 DNS 記錄相關並產生事件的動作：

|動作   |說明|
|---|---|  
|internet-svcs.zones.dns_records.create|建立 DNS 記錄。|
|internet-svcs.zones.dns_records.update|更新 DNS 記錄。|
|internet-svcs.zones.dns_records.delete|刪除 DNS 記錄。|
|internet-svcs.zones.dns_records_bulk.create|從區域檔案匯入 DNS 記錄。|


## 事件清單：負載平衡器
{: #events_load_balancers}

下表列出與負載平衡器相關並產生事件的動作：

|動作   |說明|
|---|---|  
|internet-svcs.zones.load_balancers.create|建立廣域負載平衡器。|
|internet-svcs.zones.load_balancers.update|更新廣域負載平衡器。|
|internet-svcs.zones.load_balancers.delete|刪除廣域負載平衡器。|
|internet-svcs.load_balancers.monitors.create|建立性能監視器。|
|internet-svcs.load_balancers.monitors.update|更新性能監視器。|
|internet-svcs.load_balancers.monitors.delete|刪除性能監視器。|
|internet-svcs.load_balancers.pools.create|建立廣域負載平衡器儲存區。|
|internet-svcs.load_balancers.pools.update|更新廣域負載平衡器儲存區。|
|internet-svcs.load_balancers.pools.delete|刪除廣域負載平衡器儲存區。|


## 事件清單：清除快取
{: #events_cache}

下表列出與清除快取相關並產生事件的動作：

|動作   |說明|
|---|---|  
|internet-svcs.zones.purge_cache.purge_all.update|從邊緣伺服器中清除網域的所有快取資產。|
|internet-svcs.zones.purge_cache.purge_by_urls.update|從邊緣伺服器中透過 URL 清除快取資產。|
|internet-svcs.zones.purge_cache.purge_by_cache_tags.update|從邊緣伺服器中透過快取標籤清除快取資產。|
|internet-svcs.zones.purge_cache.purge_by_hosts.update|從邊緣伺服器中透過主機名稱清除快取資產。|


## 事件清單：頁面規則
{: #events_page_rules}

下表列出與頁面規則相關並產生事件的動作：

|動作   |說明|
|---|---|  
|internet-svcs.zones.pagerules.create|建立頁面規則。|
|internet-svcs.zones.pagerules.update|更新頁面規則。|
|internet-svcs.zones.pagerules.delete|刪除頁面規則。|


## 事件清單：防火牆
{: #events_firewalls}

下表列出與防火牆相關並產生事件的動作：

|動作   |說明|
|---|---|  
|internet-svcs.zones.firewall.waf.packages.groups.update|啟用或停用 WAF 規則集的群組。|
|internet-svcs.zones.firewall.waf.packages.rules.update|啟用或停用 WAF 規則。|
|internet-svcs.zones.firewall.access_rules.rules.create|建立網域層次 IP 防火牆規則。|
|internet-svcs.zones.firewall.access_rules.rules.update|更新網域層次 IP 防火牆規則。|
|internet-svcs.zones.firewall.access_rules.rules.delete|刪除網域層次 IP 防火牆規則。|
|internet-svcs.firewall.access_rules.rules.create|建立實例層次 IP 防火牆規則。|
|internet-svcs.firewall.access_rules.rules.update|更新實例層次 IP 防火牆規則。|
|internet-svcs.firewall.access_rules.rules.delete|刪除實例層次 IP 防火牆規則。|
|internet-svcs.zones.rate_limits.create|建立速率限制規則。|
|internet-svcs.zones.rate_limits.update|更新速率限制規則。|
|internet-svcs.zones.rate_limits.delete|刪除速率限制規則。|
|internet-svcs.zones.ua_rules.create|建立使用者代理程式封鎖規則。|
|internet-svcs.zones.ua_rules.update|更新使用者代理程式封鎖規則。|
|internet-svcs.zones.ua_rules.delete|刪除使用者代理程式封鎖規則。|
|internet-svcs.zones.firewall.lockdowns.create|建立網域鎖定規則。|
|internet-svcs.zones.firewall.lockdowns.update|更新網域鎖定規則。|
|internet-svcs.zones.firewall.lockdowns.delete|刪除網域鎖定規則。|

## 事件清單：遞送
{: #events_routing}

下表列出與遞送相關並產生事件的動作：

|動作   |說明|
|---|---|  
|internet-svcs.zones.routing.smart_routing.update	|啟用或停用智慧型遞送。|
|internet-svcs.zones.routing.tiered_caching.update	|啟用或停用分層快取。|

## 事件清單：憑證套件
{: #events_certificate_packs}

下表列出與憑證套件相關並產生事件的動作：

|動作   |說明|
|---|---|  
|internet-svcs.zones.ssl.certificate_packs.create|訂購專用憑證。|
|internet-svcs.zones.ssl.certificate_packs.delete|刪除專用憑證。|


## 事件清單：自訂憑證
{: #events_custom_certificate}

下表列出與自訂憑證相關並產生事件的動作：

|動作   |說明|
|---|---|  
|internet-svcs.zones.custom_certificates.create|上傳自訂憑證。|
|internet-svcs.zones.custom_certificates.update|更新自訂憑證。|
|internet-svcs.zones.custom_certificates.delete|刪除自訂憑證。|


## 事件清單：設定
{: #events_settings}

下表列出與配置設定相關並產生事件的動作：

|動作   |說明|
|---|---|  
|internet-svcs.zones.settings.cache_level.update|變更快取層次。|
|internet-svcs.zones.settings.browser_cache_ttl.update|變更瀏覽器快取 TTL。|
|internet-svcs.zones.settings.development_mode.update|啟用或停用開發模式。|
|internet-svcs.zones.settings.security_level.update|變更安全層次。|
|internet-svcs.zones.settings.ssl.update|變更 SSL 設定。|
|internet-svcs.zones.settings.tls_1_2_only.update|啟用或停用 TLS 1.2 支援。|
|internet-svcs.zones.settings.waf.update|啟用或停用 Web 應用程式防火牆。|
|internet-svcs.zones.settings.cname_flattening.update|變更 CNAME 壓縮設定。|
|internet-svcs.zones.settings.always_online.update|對網域啟用或停用提供過時內容。|
|internet-svcs.zones.settings.sort_query_string_for_cache.update|在查詢快取中的內容時，啟用或停用排序查詢引數。|
|internet-svcs.zones.settings.tls_1_3.update|變更 TLS 1.3 設定。|
|internet-svcs.zones.settings.automatic_https_rewrites.update|啟用或停用自動 HTTPS 重寫。
|internet-svcs.zones.settings.opportunistic_encryption.update|啟用或停用機會性加密。|


## 到何處尋找事件
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} 事件可在 {{site.data.keyword.cloudaccesstrailshort}} **帳戶網域** 取得，而該網域位於產生事件的 {{site.data.keyword.cloud_notm}} 地區。



## 其他資訊
{: #info}

當您監視 IBM Cloud Internet Services (CIS) 所產生的 {{site.data.keyword.cloudaccesstrailshort}} 事件，並識別一個需要其他資訊的 API 要求時，請檢查事件中的 requestData 欄位。請開立支援問題單，並包括 requestData 中提供的 **X-CORRELATION-ID** 欄位值。
