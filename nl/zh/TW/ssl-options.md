---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: TLS Options, secure connection, Automatic HTTPS

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# TLS 選項
{:#cis-tls-options}

TLS 選項可讓您控制訪客是否可以透過安全連線來瀏覽您的網站、其執行時間、CIS 如何連接至您的原點伺服器。

## 自動 HTTPS 重寫
{:#automatic-https-rewrite}

自動 HTTPS 重寫可協助修正混合內容，方法是將您網站上可以用 HTTPS 提供的所有資源或鏈結從 "http" 變更為 "https"。這項設定位於**進階**安全配置頁面中。

## TLS 加密模式
{:#tls-encryption-modes}

這些選項是依最不安全（關閉）到最安全（端對端 CA 簽章）的順序列出。 
 * 關閉（不建議使用）
 * 用戶端到邊緣（未加密邊緣到原點、不支援自簽憑證） 
 * 端對端彈性（邊緣到原點憑證可以是自簽憑證） 
 * 端對端 CA 簽章（預設及建議）
 * 僅限 HTTPS 原點取回（僅限企業）

### 關閉 
{:#tls-encryption-modes-off}
在您的訪客與 CIS 之間沒有安全連線，而且 CIS 與您的 Web 伺服器之間沒有安全連線。訪客只能透過 HTTP 檢視您的網站，而嘗試使用 HTTPS 連接的任何訪客都會收到 `HTTP 301 重新導向`至網站的一般 HTTP 版本。

### 用戶端到邊緣
{:#tls-encryption-modes-client-to-edge}

在您的訪客與 CIS 之間有安全連線，但 CIS 與您的 Web 伺服器之間沒有安全連線。您在 Web 伺服器上不需要具有 TLS 憑證，但訪客仍然會看到網站已啟用 HTTPS。如果您的網站上有任何機密性資訊，則不建議使用此選項。這項設定僅適用於埠 443->80。只有在您無法在自己的 Web 伺服器上設定 TLS 時，才能使用它作為最後手段。它的_安全低於_ 任何其他選項（甚至是「關閉」），而且在您決定離開它時，可能會發生問題。

### 端對端彈性
{:#tls-encryption-modes-end-to-end-flexible}

在您的訪客與 CIS 之間有安全連線，而且 CIS 與您的 Web 伺服器之間有安全連線（但未經鑑別）。您必須將伺服器配置成至少使用自簽憑證來回應 HTTPS 連線。未驗證憑證的確實性：從 CIS 觀點（當我們連接至原點 Web 伺服器時）來看，這相當於略過此錯誤訊息。只要原點 Web 伺服器的位址在 DNS 設定中是正確的，就表示我們正在連接至您的 Web 伺服器，而不是連接至其他 Web 伺服器。

### 端對端 CA 簽章
{:#tls-encryption-modes-end-to-end-ca-signed}

預設及建議。訪客與 CIS 之間有安全連線，而且 CIS 與您的 Web 伺服器之間有安全且已鑑別的連線。您必須將伺服器配置成使用有效的 TLS 憑證來回應 HTTPS 連線。此憑證必須由憑證管理中心簽章、到期日為未來日期，並回應要求網域名稱（主機名稱）。除非您瞭解變更為其中一種較不嚴格模式的潛在安全威脅，否則，我們建議您保持使用此 TLS 模式作為最佳安全作法。

### 僅限 HTTPS 原點取回
{:#tls-encryption-modes-origin-only-pull}

*僅限企業*。此模式的憑證需求與「端對端 CA 簽章」相同，也會將 CIS 與原點 Web 伺服器之間的所有連線從 HTTP 升級為 HTTPS，即使所要求的原點內容是透過 HTTP 也一樣。

## 最低 TLS 版本
{:#minimum-tls-version}

這會為嘗試連接至網站的資料流量設定最低 TLS 版本。依預設，這會設為 1.0。越高的 TLS 版本可提供更多安全，但並非所有瀏覽器都支援該版本。這可能會導致部分客戶無法連接至您的網站。
