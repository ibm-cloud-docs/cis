---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Glossary, load balancer, pool, health check

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# 名詞解釋
{:#glossary}

此名詞解釋包含您在使用「廣域負載平衡器 (GLB)」時可能會遇到之一般術語的定義。

## 性能檢查 (Health check)
{:#glossary-health-check}

性能檢查有助於深入瞭解儲存區的可用性，以將資料流量遞送至性能良好儲存區。這些檢查會定期傳送 HTTP/HTTPS 要求，以及監視回應。它們可以使用自訂間隔、逾時、狀態碼等等進行配置。只要將儲存區標示為性能不佳，就會將資料流量聰明地重新遞送至另一個可用的儲存區（如果可用的話）。

## 負載平衡器 (Load balancer)
{:#glossary-load-balancer}

負載平衡器是作為反向 Proxy 的裝置，可在許多伺服器之間分配網路或應用程式資料流量。負載平衡器是用來增加系統容量（並行使用者數目）及改善應用程式的可靠性。

## 原點伺服器 (Origin Servers)
{:#glossary-origin-servers}

原點伺服器會處理及回應來自用戶端的送入要求，且通常與快取伺服器一起使用。原點伺服器會執行一個以上的程式，這些程式設計來接聽及處理送入的網際網路要求。原點伺服器與提出要求的用戶端之間的實際距離會增加連線的延遲，進而增加載入時間。使用快取伺服器可減少此延遲。


## 儲存區 (Pool)
{:#glossary-pool}

儲存區是在連接至 GLB 時將資料流量聰明地遞送至其中的原點伺服器群組。使用者可以配置要標示為性能良好之儲存區的可用原點伺服器數目下限，以及要使用的特定性能檢查。原點儲存區可以與特定地區相關聯，也可以可供所有地區使用。

