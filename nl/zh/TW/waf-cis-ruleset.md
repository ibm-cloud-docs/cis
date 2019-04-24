---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIS Rule Set, WAF settings, WAF CIS Rules

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# WAF 設定
{:#waf-settings}

下表顯示「Web 應用程式防火牆 (WAF)」可以採取的動作。 


|動作   |定義       |
|---|---|
|封鎖|封鎖攻擊會在任何動作張貼到網站之前就停止動作。|
|模擬|若要測試是否誤判，請將 WAF 設為「模擬」模式，這會記錄對於可能攻擊的回應，而不進行盤查或封鎖。|
|盤查|盤查頁面會請訪客提交 CAPTCHA 以繼續造訪您的網站。|
|臨界值或靈敏度設定|設定規則來觸發更多或更少，視靈敏度而定。|

## WAF 的 CIS 規則集
{:#cis-ruleset-for-waf}

選取**檢視 CIS 規則**，以顯示此套件的規則集。規則集如下：
  * Drupal
  * Flash
  * Joomla
  * Magento
  * Miscellaneous
  * PHP
  * Plone
  * Specials
  * WHMCS
  * Wordpress

**Specials** 包含一些適用於網際網路上幾乎所有應用程式及網站的規則。此規則集是 WAF 提供的安全核心，其規則瞄準常見的攻擊，例如 SQLi、XSS 及 LFI。建議您一律保持啟用 Specials。

只啟用對應於您技術堆疊的規則集。比方說，如果您只使用 Wordpress，而無其他任何技術，請只啟用 Specials 及 Wordpress 規則集。請避免啟用與技術堆疊無關的規則集。

請選取任何特定的「規則集」，以查看每個所包含規則的進一步詳細資料。

CIS 規則集可讓您對每一個規則執行四個動作：
  1. **停用**：關閉規則。
  2. **模擬**：記載事件且不封鎖或盤查訪客（在檢閱日誌之後，您仍可決定要設為封鎖或盤查）。
  3. **封鎖**：封鎖就是直接整個封鎖要求，讓要求無法選擇略過它。
  4. **盤查**：會顯示盤查 (CAPTCHA) 頁面，在容許存取有問題的要求之前必須先完成此頁面。

您可能會發現規則的名稱並未確切顯示其運作方式，而多半只是其功能的一般摘要。這是故意的。基於安全考量，我們不會顯示我們用來過濾資料流量的程式碼（或其他確切的資訊）。這可防止惡意動作者進行反向工程來避開我們的防禦。
