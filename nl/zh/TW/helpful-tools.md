---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Helpful tools, whois, IPv4

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 管理 CIS 部署的有用工具
{:#helpful-tools-for-managing-your-cis-deployment}

具有一些公用網域 Unix 系統管理工具，可協助您管理 IBM CIS 部署。

## Sysadmin 工具
{:#cis-sysadmin-tools}

 * whois（網域識別工具）
 * dig（DNS 工具）
 * curl（HTTP 及 HTTPS 工具）
 * netcat（IP 及埠工具）
 * traceroute（網路工具）

## 用於外部及遠端測試的商業工具
{:#commercial-tools-for-external-and-remote-testing}

 * GTMetrix (http)
 * 網頁測試 (http)
 * WhatsMyDNS（DNS 工具）
 * G Suite Toolbox（DNS 及 HTTP）

## 用於查看日誌及歷程的工具
{:#tools-for-looking-at-logs-and-history}

 * HTTP 保存檔（HAR 檔案）


### 使用 `whois`
{:#using-whois}

`whois` 是一種 Unix 系統指令行工具，可用來查閱給定網域名稱或 IP 位址的登記員資訊，例如，網域的給定授權性伺服器或特定 IP 位址的擁有者。

範例：

`whois example.com`

`whois 8.8.8.8`

### 使用 `dig`
{:#using-dig}

`dig` 是一種 Unix 指令行工具，可執行 DNS 查詢，以及檢查特定網域的 DNS 記錄。它與 `nslookup` 類似。

此指令的綱目為：dig <recordtype. <domainname> <options>

**範例：**

`dig example.com`

`dig my.example.com`

`dig example.com +trace`

`dig NS example.com`

`dig example.com @ns.example.com`

### 使用 `cURL`
{:#using-curl}

`cURL` 是一種 Unix 指令行工具，可讓您使用 URL 語法來傳輸資料。這通常用來提出 HTTP 要求或比較伺服器回應。

此指令的綱目為：`curl -option1 -option2 http://example.com/url`

**範例：**

`curl -svo /dev/null http://www.example.com`

`curl -svo /dev/null -A "USER_AGENT_STRING" http://www.example.com`

`curl -svo /dev/null -H "host: www.example.com" http://ORIGIN_IP`

`curl -svo /dev/null -H https://www.example.com --resolve www.example.com:443:ORIGIN_IP`

### 使用 `mtr` 及 `traceroute`
{:#using-mtr-and-traceroute}

MTR 及 `traceroute` 是 Unix 指令行工具，可讓您測量指定主機或目的地伺服器之特定網路路徑的效能或延遲。

**範例：**

`mtr -rwc 20 example.com -T -4`
`mtr -rwc 20 8.8.8.8 -T -6`

`traceroute example.com -T -4`

`traceroute 8.8.8.8 -T -6`

|選項   |定義       |
|---------|-----------|
|-c |設定傳送的連線測試數目|
|-T |強制 TCP traceroute（通常是 ICMP）|
|-4 |強制使用 IPv4|
|-6 |強制使用 IPv6|

### 產生 HAR 檔案
{:#generating-a-har-file}

HAR 檔案是來自 Web 瀏覽器的 HTTP 要求記錄。瀏覽器（例如 Chrome）的「開發人員工具」區段可協助您設定以製作 HAR 檔案。
