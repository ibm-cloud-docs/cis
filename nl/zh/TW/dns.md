---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM CIS DNS records, parts of the DS record, Type

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"} 
{:note: .note} 
{:important: .important} 
{:deprecated: .deprecated} 
{:generic: data-hd-programlang="generic"}

# 設定 IBM CIS 的網域名稱系統 (DNS)
{:#set-up-your-dns-for-cis}

本文件包含如何配置 IBM CIS DNS 記錄的一些特定指示（包括如何配置「安全 DNS」）。

## 安全 DNS
{:#secure-dns}

**DNSSec** 是數位「簽署」DNS 資料的一種技術，讓您可以確定它是有效的。若要消除網際網路的漏洞，必須在查閱（從根區域到最終網域名稱（例如 www.icann.org））的每一個步驟上部署 DNSSec。

## 配置及管理安全 DNS 
{:#configuring-and-managing-your-secure-dns}

DNSSec 會將鑑別層新增至網際網路的 DNS 基礎架構，否則會不安全。安全 DNS 可保證訪客在 Web 瀏覽器中鍵入您的網域名稱時，將他們導向至**您的** Web 伺服器。您只需要從 IBM CIS 帳戶的 DNS 頁面中啟用 DNSSec，並將 DS 記錄新增至您的登記員。

![安全 DNS](images/dns/secure-dns.png)

您可以選取**檢視 DS 記錄**按鈕來開啟對話框，說明如何將 DS 記錄新增至您的登記員。您必須複製 DS 記錄的某些部分，並將它們貼入登記員的儀表板。每個登記員都不同，而且您的登記員可能只需要您輸入部分可用欄位的資訊。

## 新增 DNS 記錄
{:#adding-dns-records}

您可以使用**類型**下拉清單，選取您要建立的記錄類型。每一筆 DNS 記錄類型都具有相關聯的「名稱」及「存活時間 (TTL)」。 

只要在「名稱」欄位中輸入內容，就會在該內容附加網域名稱，除非已在欄位中手動附加網域名稱（例如，如果已在欄位中鍵入 `www` 或 `www.example.com`，則 API 會將兩者處理為 `www.example.com`）。如果在名稱欄位中鍵入確切的網域名稱，則不會附加它（例如 `example.com` 將會處理為 `example.com`）。不過，DNS 記錄清單只會顯示未鎖定網域名稱的名稱，因此 `www.example.com` 會顯示為 `www`，而 `example.com` 會顯示為 `example.com`。TTL 的預設值會是`自動`，但使用者可以進行變更。Proxy DNS 記錄一律會有`自動`的 TTL，因此，在這項變更期間，新的 Proxy 記錄將會變更為此配置。

### A 類型記錄
{:#a-type-record}

若要新增此記錄類型，**名稱**及 **IPv4 位址**欄位中必須要有有效值。也可以從下拉功能表指定 **TTL**，預設值為`自動`。

![建立「A 類型」記錄](images/dns/create-a-type-record.png)

    必要欄位：名稱、IPv4 位址
    選用欄位：TTL（預設值為「自動」）

### AAAA 類型記錄
{:#aaaa-type-record}

若要新增此記錄類型，**名稱**及 **IPv6 位址**欄位中必須要有有效值。也可以從下拉功能表指定 **TTL**，預設值為`自動`。

![建立「AAAA 類型」記錄](images/dns/create-aaaa-type-record.png)

    必要欄位：名稱、IPv6 位址
    選用欄位：TTL（預設值為「自動」）

### CNAME 類型記錄
{:#cname-type-record}

若要新增此記錄類型，**名稱**欄位中必須要有有效值，而且**網域名稱** (FQDN) 欄位中必須要有完整網域名稱。也可以從下拉功能表指定 **TTL**，預設值為`自動`。


![建立「CNAME 類型」記錄](images/dns/create-cname-type-record.png)

    必要欄位：名稱、網域名稱（適用於 CNAME）
    選用欄位：TTL（預設值為「自動」）

只要在 CIS 內配置網域，企業方案便能夠 CNAME（指向）另一個網域。
{:note}

```
例如：
配置的 CIS 網域：
  - example.com
  - different.com

test.example.com -CNAME-> test.different.com
```

### MX 類型記錄
{:#mx-type-record}

若要新增此記錄類型，**名稱**欄位中必須要有有效值，而且**郵件伺服器**欄位中必須要有有效位址。也可以從下拉功能表指定 **TTL**，預設值為`自動`。

![建立「MX 類型」記錄](images/dns/create-mx-type-record.png)

    必要欄位：名稱、郵件伺服器
    選用欄位：TTL（預設值為「自動」）、優先順序（預設值為 1）

### LOC 類型記錄
{:#loc-type-record}

若要新增此記錄類型，**名稱**欄位中必須要有有效值。如果您需要更具體的資訊，請選取**配置 LOC 選項**按鈕。也可以從下拉功能表指定 **TTL**，預設值為`自動`。

![建立「LOC 類型」記錄](images/dns/create-loc-type-record-1.png)

    必要欄位：名稱
    選用欄位：LOC 選項（按一下按鈕進行配置）

![建立「LOC 類型」記錄](images/dns/create-loc-type-record-2.png)

### CAA 類型記錄
{:#caa-type-record}

若要新增此記錄類型，**名稱**及**值**欄位中必須要有有效值。「值」欄位將會與**標籤**下拉欄位的值產生關聯，而預設值為「將違規報告傳送至 URL」。也可以從下拉功能表指定 **TTL**，預設值為`自動`。

![建立「CAA 類型」記錄](images/dns/create-caa-type-record.png)

    必要欄位：名稱、值（與標籤相關聯）
    選用欄位：TTL（預設值為「自動」）、標籤（預設值是將違規報告傳送至 URL）

### SRV 類型記錄
{:#srv-type-record}

若要新增此記錄類型，**名稱**、**服務名稱**及**目標**欄位中必須要有有效值。使用下拉功能表來選取**通訊協定**，而預設值為 UDP 通訊協定。此外，您可以指定**優先順序**、**加權**及**埠**。這三個欄位的預設值為 1。也可以從下拉功能表指定 **TTL**，預設值為`自動`。

![建立「SRV 類型」記錄](images/dns/create-srv-type-record.png)

    必要欄位：名稱、服務名稱、目標
    選用欄位：TTL（預設值為「自動」）、通訊協定（預設為 UDP）、優先順序（預設為 1）、加權（預設為 1）、埠（預設為 1）

### SPF 類型記錄
{:#spf-type-record}

若要新增此記錄類型，**名稱**及**內容**欄位中必須要有有效值。也可以從下拉功能表指定 **TTL**，預設值為`自動`。

![建立「SPF 類型」記錄](images/dns/create-spf-type-record.png)

    必要欄位：名稱、內容
    選用欄位：TTL（預設值為「自動」）

### TXT 類型記錄
{:#txt-type-record}

若要新增此記錄類型，**名稱**及**內容**欄位中必須要有有效值。也可以從下拉功能表指定 **TTL**，預設值為`自動`。

![建立「TXT 類型」記錄](images/dns/create-txt-type-record.png)

    必要欄位：名稱、內容
    選用欄位：TTL（預設值為「自動」）

第一次訂購專用憑證時，會發生「網域控制驗證 (DCV)」處理程序，它會產生相對應的 TXT 記錄。如果您刪除 TXT 記錄，則當您訂購另一個專用憑證時，DCV 處理程序會再次發生。如果您刪除專用憑證，則不會刪除對應於 DCV 處理程序的 TXT 記錄。
{:note}

### NS 類型記錄
{:#ns-type-record}

若要新增此記錄類型，**名稱**及**名稱伺服器**欄位中必須要有有效值。也可以從下拉功能表指定 **TTL**，預設值為`自動`。

![建立「NS 類型」記錄](images/dns/create-ns-type-record.png)

    必要欄位：名稱、名稱伺服器
    選用欄位：TTL（預設值為「自動」）

## 更新 DNS 記錄
{:#updating-dns-records}

在每一個記錄列中，您可以按一下功能表中的**編輯記錄**選項以開啟對話框，讓您用來更新記錄。

![編輯 DNS 記錄](images/dns/edit-dns-record.png)

例如，這是 **A** 類型記錄的更新對話框。完成變更之後，請選取**更新記錄**進行儲存。

![編輯 DNS 記錄對話框](images/dns/update-dns-dialog.png)

## 刪除記錄
{:#deleting-dns-records}

在每一個記錄列中，您可以從功能表中選取**刪除記錄**選項，以開啟對話框來確認刪除處理程序。

![刪除 DNS 記錄](images/dns/delete-record.png)

您可以選取**刪除**按鈕，以確認您的刪除動作。如果您不要刪除，則請選取**取消**。

![刪除 DNS 記錄對話框](images/dns/delete-record-dialog.png)

## 匯入及匯出記錄
{:#import-export-records}

可以在 CIS 中進行 DNS 記錄的匯入及匯出。所有檔案都會匯入及匯出成 BIND 格式的 .txt 檔案。[BIND 格式](https://en.wikipedia.org/wiki/Zone_file)的相關資訊。
按一下溢位功能表，然後選取匯入或匯出記錄。
![DNS 記錄選項](images/dns/import-export-records.png)

### 匯入記錄
{:#import-dns-records}

依預設，總共容許 3500 個 DNS 記錄（在 CIS 上匯入及建立）。您可以匯入多個檔案（一次一個），但記錄總數不得超出上限。匯入之後，您會看到順利新增的記錄數目及失敗數目的摘要，以及每筆記錄失敗的原因。
![匯入 DNS 記錄摘要](images/dns/import-records-summary.png)

### 匯出記錄
{:#export-dns-records}

使用`匯出記錄`來建立區域檔案的備份，或將其匯出，以便與另一個 DNS 提供者搭配使用。按一下這個功能表選項時，該記錄會下載到瀏覽器設定所指定的位置（通常是「下載」資料夾）。若要選取另一個資料夾位置，請變更瀏覽器的設定，以提示您輸入每次下載的位置。
