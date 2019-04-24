---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIDR blocks, Whitelist Block Challenge, IBM Cloud Internet Services, security features

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# IBM Cloud Internet Services (CIS) 如何保持工作安全
{:#how-cis-keeps-your-work-secure}

IBM CIS 是一種廣域分散式雲端服務，可封鎖威脅，以及限制浪費頻寬和伺服器資源的濫用機器人及搜索器。IBM CIS 作為廣域 HTTP(S) 反向 Proxy 及受管理 DNS 服務提供者。Web 資料流量會透過智慧型廣域網路進行遞送，以最佳化效能及安全性。

![security-graphic.png](images/security-graphic.png)

以下是快速特性概觀：

## 安全特性
{:#cis-security-features}

 * 對 [DNS 記錄](/docs/infrastructure/cis?topic=cis-dns-concepts#proxying-dns-records)或 [GLB](/docs/infrastructure/cis?topic=cis-global-load-balancer-glb-concepts) 進行 Proxy 處理，以使用安全特性。這可讓資料流量通過我們的伺服器，也可以監視資料。
### Web 應用程式防火牆 (WAF)
{:#cis-web-application-firewall}

 * WAF 透過兩個規則集實作：[OWASP](/docs/infrastructure/cis?topic=cis-owasp-rule-set-for-waf) 及 [CIS](/docs/infrastructure/cis?topic=cis-waf-settings#cis-rule-set-for-waf)。
### 無限制 DDoS 降低
{:#cis-unlimited-ddos-mitigation}

 * DDoS 降低通常是一項昂貴服務，在遭到攻擊時可能會增加成本。我們在 CIS 中包含無限制的 DDoS 降低，不另外收費。

## 安全標準及平台
{:#security-standards-and-platform}

 * TLS（SHA2 及 SHA1）
 * IPv6
 * HTTP/2 及 SPDY

## DNS
{:#cis-dns}

 * 廣域 Anycast 網路
 * DNSSEC

## 網路攻擊及降低
{:#network-attacks-and-mitigation}

一般而言，攻擊分成兩種種類：

|第 3 層或第 4 層攻擊       |第 7 層攻擊     |
|------------------------------|-----------------|
|這些攻擊包含 ISO 第 3 層（網路層）（例如 ICMP 洪水）或第 4 層（傳輸層）（例如 TCP SYN 洪水或反映的 UDP 洪水）的大量資料流量|這些攻擊會傳送惡意 ISO 第 7 層要求（應用程式層），例如 GET 洪水。|
|在邊緣自動封鎖|我們使用「防禦模式」、WAF 及「安全層次」設定來處理這些攻擊|

## IP 防火牆
{:#cis-ip-firewall}

IBM Cloud Internet Services 提供數種工具來控制您的資料流量，讓您可以在面對大量資料流量、特定要求端群組及特定要求 IP 時，保護您的網域、URL 及目錄。本節詳述可用的工具。

### IP 規則
{:#cis-ip-rules}

「IP 規則」可讓您控制對特定 IP 位址、IP 範圍、特定國家/地區、特定 ASN 及特定 CIDR 區塊的存取權。送入要求的可用動作如下：
  * 白名單 
  * 封鎖 
  * 盤查 (Captcha) 
  * JavaScript 盤查（IUAM 盤查）

比方說，如果您發現特定 IP 造成惡意要求，您可以依 IP 位址封鎖該使用者。

### 使用者代理程式封鎖規則
{:#user-agent-blocking-rules}

「使用者代理程式封鎖規則」可讓您對您選取的任何「使用者代理程式」字串採取動作。此功能的運作方式類似「網域鎖定」（如前所述），只不過封鎖是檢查送入的「使用者代理程式」字串，而不是 IP。您可以選擇如何使用您在「IP 規則」（封鎖、盤查及 JS 盤查）中建立的相同動作清單來處理比對要求。請注意，「使用者代理程式」封鎖適用於整個區域。您不能以「網域鎖定」的相同方式來指定子網域。

本工具對於封鎖任何您認為可疑的「使用者代理程式」字串很有幫助。 

### 網域鎖定
{:#cis-domain-lockdown}

「網域鎖定」可讓您將特定 IP 位址及 IP 範圍列入白名單，使得所有其他 IP 都列入黑名單。「網域鎖定」支援：

  * 特定子網域。例如，您可以容許 IP `1.2.3.4` 存取網域 `foo.example.com`，並容許 IP `5.6.7.8` 存取網域 `bar.example.com`，而不一定要容許反向設定。
  * 特定 URL。例如，您可以容許 IP `1.2.3.4` 存取目錄 `example.com/foo/*`，並容許 IP `5.6.7.8` 存取目錄 `example.com/bar/*`，但不一定要容許反向設定。當您在存取規則中需要更精細的內容時，此功能很有用，因為利用「IP 規則」可讓您對現行網域的所有子網域，或對您帳戶上的所有網域套用封鎖，但您不能指定 URI。

### 盤查進程
{:#cis-challenge-passage}

這項設定位於**進階**安全設定中，它可讓您控制通過某項盤查或 JavaScript 盤查的訪客，再重新盤查之前要經過多久才能存取您的網站。這是根據訪客的 IP，因此並不適用於 WAF 規則提供的盤查，因為它們是根據使用者對您網站執行的動作。

### 瀏覽器完整性檢查
{:#cis-browser-integrity-check}

這項設定位於**進階**安全設定中。瀏覽器完整性檢查會尋找濫發垃圾郵件者經常濫用的 HTTP 標頭。它會拒絕以那些標頭存取您頁面的資料流量。它也會封鎖沒有使用者代理程式的訪客，或是新增非標準使用者代理程式的訪客（濫用機器人、搜索器或 API 經常使用此手法）。
