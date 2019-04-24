---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: health checks, Free Trial plan, dedicated certificate, known issues

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 
{:note: .note} 
{:important: .important} 
{:deprecated: .deprecated} 
{:generic: data-hd-programlang="generic"}

# 已知限制
{:#known-limitations}

 * 建議您使用 Chrome。
 
 * 「免費試用」方案限制為每個帳戶只能有一個實例。建立資源實例並在其中新增網域之後，不容許您為 CIS 新增資源實例。即使您刪除試用網域，然後再次嘗試將網域新增至相同的資源實例，也會強制執行此限制。如果您嘗試這麼做，則會發生錯誤。

 * 對於此服務，我們只支援使用來自另一個提供者的 NS 記錄進行子網域委派。不支援 CNAME 委派。
  
 * A、AAAA 及 CNAME 萬用字元記錄 (*) 無法進行 Proxy 處理。

 * 當您刪除專用憑證時，在完成刪除之前，它可能會短暫地重新出現在清單中。
 
 * 若要在訂購之後修改自訂專用憑證的主機名稱，您必須訂購新憑證，然後刪除舊憑證。 
 
 * 使用兩個字母國碼所建立的 IP 規則，只能利用`盤查`動作來建立。如果您想要封鎖某個國家/地區的訪客，請升級至「企業」方案，或在您的伺服器上執行完全封鎖的規則。

## 廣域負載平衡器
{:#known-limitations-glb}

 * Cloud Internet Services 可讓您在負載平衡器主機名稱中使用 `_` 字元，不過，Kubernetes 叢集無法使用 `_`。 

 * 「標準」方案最多允許使用 5 個負載平衡器、儲存區及性能檢查。每個儲存區最多可以有 6 個原點，但在每個 CIS 實例中只允許使用 6 個唯一原點。

* 無法過濾已刪除儲存區及原點的性能檢查事件，但它們仍會出現在表格中。

* 如果您依`儲存區性能`來過濾「性能檢查」事件，則會包括`欠佳`儲存區，因為它們在技術上性能良好，但可能包含一個以上的嚴重原點。

* 新增用於性能檢查的要求標頭名稱時，請使用 `Host`。對性能檢查使用小寫 `host` 則會失敗。

## DNS
{:#known-limitations-dns}

 * 匯出 DNS 記錄包括應該隱藏的 Cloudflare CNAME 記錄。這些記錄的開頭為 `_`，而且通常會有名稱相同但移除了 `_` 的第二個記錄。
   ```
   Ex.
   _cf.generate.yourdomain.com 0	IN	CNAME address.alias.com
   cf.generate.yourdomain.com 0	IN	CNAME address2.alias.com
   ```
 
   這些記錄必須從區域檔案中移除後，才能正確匯入。
 
 * 匯出 CAA DNS 記錄未正確運作。`<tag>` 及 `<value>` 為 HEX 編碼。 
 
    CAA `<flags>` `<tag>` `<value>`
  {:note}
   ```
   Ex.
   Original CAA record
   caa.yourdomain.com.	1	IN	CAA	0 issue "letsencrypt.org"

   )xported CAA record
   caa.yourdomain.com.	)	IN	CAA	0 6973737565 "6c657473656e63727970742e6f7267"
   ```
   這些記錄必須從 HEX 轉換成字串，或在匯入之前手動移除並新增。

## 頁面規則
{:#known-limitations-pagerules}

   * 如果用於更新的 JSON 字串或 JSON 檔案中未包括頁面規則 ID，則使用 IBM Cloud CLI 的 CIS 外掛程式來更新頁面規則設定可能會導致錯誤。暫時解決之道，是對頁面規則使用完整的 JSON 配置檔來提交更新，包括該 ID 在內。
   * 利用 CIS 使用者介面來移除頁面規則設定可能無法移除設定（雖然使用者介面會報告更新順利完成）。若要暫時解決此問題，請使用 IBM Cloud CLI 的 CIS 外掛程式來移除設定，並在 JSON 更新文件中包括頁面規則 ID：
      ```
      $> ibmcloud cis page-rule-update <domain-id> <rule-id> -j <file>
      ```
      JSON 檔案應該包括完整的頁面規則配置（包括 ID）及必要的更新項目。
