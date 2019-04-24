---

copyright:
  years: 2018
lastupdated: "2018-03-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# API 規格

以下說明如何檢視 CIS API 規格： 

1. 若要檢視 CIS API，請導覽至 [CIS API 規格](https://console.bluemix.net/apidocs/2640-cloud-internet-services)頁面。 

2. 在左側導覽功能表中，從可用的 API 清單中進行選擇。


## 注意事項

1. API 端點：https://api.cis.cloud.ibm.com。

2. 每一個 API 呼叫都需要 **X-Auth-User-Token** 標頭。這是可以從 IAM 擷取之使用者的載送記號（例如，使用 "bx iam oauth-tokens" 指令）。

3. 每一個 API 呼叫的路徑中也需要 **crn** 欄位。這是所配置之 CIS 資源實例的完整「雲端資源名稱 (CRN)」（例如，可以使用指令 "bx resource service-instance <instance-name>" 從其名稱擷取資源實例的 CRN）。在 API 呼叫中，CRN 必須是 URL 編碼。

4. API 呼叫受到速率限制。可以在 1 分鐘內共完成 100 個 API 呼叫。如果超出此速率，則會封鎖後續呼叫一段時間。
