---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: WAF Custom Rules, Custom WAF Rules

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# WAF 自訂規則
{:#waf-custom-rules}

透過**安全 > Web 應用程式防火牆 > 自訂規則**，導覽至「自訂 WAF 規則」。「WAF 規則」可用於「企業」方案，並根據該客戶特有的需求及/或其網站的資料流量型樣而建立。這表示您可以請我們封鎖要求的幾乎所有特徵組合。 

「自訂 WAF 規則」可滿足這樣的狀況：IBM WAF 尚未具備規則，但攻擊者使用專門針對您網站結構的特定型樣或使用者代理程式。在這些狀況下，您可以為 Web 內容建立自訂規則。

## 要求自訂規則
{:#request-a-custom-rule}

若想要求規則，請傳送電子郵件給 wafsup@us.ibm.com，並附上規則需求或資料流量型樣。 

請儘可能提供資訊，包括：
* 存取日誌，其顯示大約 100 個受指控惡意要求的範例。
* 範例 POST 要求，其中包括 POST 資料（如果該要求有 POST 內文），以判定該要求是否包含任何我們可以封鎖或觸發的項目。
* 在有可能誤判的情況下，您是否想要徹底封鎖或盤查要求。
* 您想要套用這些規則的特定網域。
* 您希望依預設開啟或關閉規則。

建立自訂 WAF 規則之後，您必須啟用所有自訂規則，才能使它們生效。
{:note}
