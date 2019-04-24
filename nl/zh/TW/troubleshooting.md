---
copyright:
  years: 2018
lastupdated: "2018-03-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# CIS 網路連線疑難排解

## 如何得知我的資料是否通過 IBM CIS 連線？

IBM Cloud Internet Services (CIS) 使用 HTTP 標頭，以進行讀取、新增或修改。標頭可讓我們追蹤如何使用 CF-Ray 號碼遞送要求。您可以透過 `curl` 指令或使用稱為 "Claire" 的 Google Chrome 外掛程式找到 CF-Ray 號碼。

若要知道資料是否已通過 IBM CIS，請找出將出現在每個封包上的 `Ray ID`。

**Unix 指令行工具：**

 * curl（適用於 HTTP）：
`$ curl -vso /dev/null http://example.com`

 * dig（適用於 DNS）：
`$ dig www.example.com`

 * traceroute（適用於網路）：
`$ traceroute example.com`

**例如：**

終端機指令：`curl -svo /dev/null YOUR_URL_HERE. -L`

導致：`CF-RAY: 1ca349b6c1300da3-SJC`

## 如何追蹤路徑？

若要查看路徑是否通過您的 IBM CIS 路線，您可以在 Mac 或 Linux 的「終端機」視窗中執行 'dig'，或在 Windows 的 Windows 命令提示字元中使用 `nslookup`。

如果封包具有 CF-Ray 值，則已通過 CIS。

`traceroute` 指令會顯示 IP 要求所採用的整個路徑。

支援團隊會利用這些指令來協助您。

## 如果您看到隱私權警告：

IBM CIS 所發出的憑證涵蓋根網域 (`example.com`) 以及一個層次的子網域 (`*.example.com`)。如果您嘗試到達第二層子網域 (`*.*.example.com`)，則會在瀏覽器中看到隱私權警告，因為這些主機名稱不會新增至 SAN。

另請容許最多 15 分鐘，讓我們的其中一個夥伴「憑證管理中心 (CA)」來發出新憑證。如果尚未發出新憑證，則您會在瀏覽器中看到隱私權警告。

## 我受到 DDoS 攻擊時該怎麼辦？

 * **步驟 1：**從儀表板開啟「防禦模式」
 * **步驟 2：**設定 DNS 記錄以達到最高安全
 * **步驟 3：**請不要對來自 IBM CIS 的要求進行速率限制或節流控制
 
在「防禦模式」期間，每一個新訪客都會經歷 "Captcha" 安全盤查，而他們必須在獲授與未經盤查存取的 Cookie 之前通過。因此，除非關閉「防禦模式」，否則會封鎖殭屍網路資料流量。不符合安全盤查的訪客會新增至（不正確的）「IP 信譽」資料庫。

## 您可能遇到的其他問題：

以下是您或支援團隊可能會看到的一些常見錯誤訊息：

| 錯誤碼        | 原因   |
| ------------- | ------------- |
| 1001  | DNS 解析錯誤。客戶最近已註冊但尚未傳播其 DNS 資訊，或管理 DNS 的任何人失敗。|
| 521  | 原點 Web 伺服器已拒絕來自 CIS 的連線。原點 Web 伺服器未執行，或有某個項目封鎖 IBM CIS IP 位址。|
| 522  | 原點伺服器的連線逾時（預設值為 30 秒）。CIS 可能已進行速率限制、Web 伺服器可能將耗用所有資源（共用伺服器），或 Web 伺服器與 IBM CIS 之間可能存在網路連線問題。|
| 523  | 無法連接原點伺服器。請確定 DNS 記錄的原點 IP 位址與出現在「CIS DNS 設定」頁面中的 IP 位址相同。|
| 524  | IBM CIS 可以建立 TCP 連線，但未收到來自 Web 伺服器的回應。長時間執行的應用程式或資料庫查詢將會干擾。|

### 看不到任何網路資料流量

如果您看不到資料流量，而且要使用 CNAME，則請確定已有重新導向，因此不會將資料流量遞送至根網域。請記住，部分 DNS 傳播最多可能需要 48 小時才能完成。

### 網站離線

以下是您可能會看到的內容：

`IBM CIS 無法連接至原點伺服器（錯誤 521、522、523）`。

**網站離線 - 無快取的版本**

1. 伺服器已上線，但正在封鎖 IBM CIS 要求。
2. 原點伺服器已離線，而且 IBM CIS 沒有備份網站映像檔 

您可以執行的作業：

* 驗證 IBM CIS IP 位址已列入白名單。
* 確定 IBM CIS IP 未進行速率限制。
* 以下是[要列入白名單的 IP](whitelisted-ips.html) 清單

### 502 錯誤「可怕的 502」

此錯誤是您可能會看到的其中一個最常見錯誤。它通常發生在無法使用網路的某個部分時（例如，在 DDoS 攻擊的開始處）。特定資料中心可能會有一段時間無法使用。將會重新遞送資料流量。請執行追蹤路徑。 

以下是您可能會看到的內容：`錯誤 502 - 不正確的閘道錯誤`

會發生的情況：

* IBM CIS 網路的某個部分發生問題。
* 通常只有一個資料中心內的一部伺服器會發生問題。
* 它只會影響網站某個部分的訪客。
* IBM CIS Technical Operations 團隊會處理這些項目。

您可以執行的作業：

* 將問題單中 `www.YOUR_DOMAIN.com/cdn-cgi/trace` 的結果傳送給[支援中心](https://console.bluemix.net/docs/support/index.html#contacting-support)。
* 暫時關閉 DNS 記錄（無 Proxy）。

