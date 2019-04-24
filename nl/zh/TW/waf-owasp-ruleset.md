---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: OWASP Rule Set, Rule Set

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# WAF 的 OWASP 規則集
{:#owasp-rule-set-for-waf}

「OWASP 規則集」包含一般的攻擊偵測規則。OWASP 規則可防範許多一般攻擊種類，包括「SQL 注入」、「跨網站 Scripting」及「語言環境檔併入」等等。IBM CIS 會提供但不會策劃這些規則。OWASP 是一種能夠提供良好安全基準的業界標準。如需相關資訊，請參閱下列鏈結：
  * [Github 上的 OWASP](https://github.com/SpiderLabs/owasp-modsecurity-crs)
  * [OWASP.org](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project)

## 管理 OWASP
{:#managing-owasp}

與 [CIS 規則集](/docs/infrastructure/cis?topic=cis-cis-rule-set-for-waf)不同，OWASP 可讓您設定「靈敏度」。
一個要求可能觸發一組 OWASP 規則，其具有相關聯的由高至低嚴重性評分。最後得分是根據所有觸發的規則來計算。計算最後得分之後，CIS 會將它與開始時選取的靈敏度臨界值進行比較，然後封鎖或容許該要求。

|靈敏度評分|觸發的臨界值|
|------|---------------|
|低|60 以上|
|中|40 以上|
|高|25 以上|

我們建議您將 OWASP 靈敏度設為`低`。如果您將它設為`高`，請檢查 CIS 上的日誌，並細部調整 OWASP 規則集以適合您的應用程式。

請記住，OWASP 規則只能切換為_開啟_ 或_關閉_，它們跟 CIS 規則集的規則不同，後者可設為_停用_、_模擬_、_盤查_ 或_封鎖_。

## 如何處理誤判？
{:#owasp-false-positives}

當變數或值評估為 _true_ 或_正數_，但實際上是負數時，即發生誤判。在我們的 WAF 環境定義中，誤判表示已封鎖要求，因為它被錯誤評估為惡意。

若要處理誤判，並確保未來能夠避免誤判，您必須知道如何找出它們並加以更正。請檢閱所封鎖要求的日誌，然後評估在網站的預期及正常資料流量環境定義內，這些要求遭到封鎖是否合理。
