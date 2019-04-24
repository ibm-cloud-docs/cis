---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM Cloud Internet Services, reliable IBM Cloud Internet Services, Global Load Balancing

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# IBM Cloud Internet Services (CIS) 如何保持工作可靠性
{:#how-cis-keeps-your-work-reliable}

IBM Cloud Internet Services (CIS) 可協助您改善 Web 服務及應用程式的可靠性，因為它可協助您避免應用程式及基礎架構中斷所造成的關閉時間。例如，使用「廣域負載平衡」，您可以將 Web 服務及應用程式部署至多個地區。IBM CIS 會將客戶要求遞送至啟用「廣域負載平衡」時可用的最接近地區。如果任何地區失敗，則會將要求遞送至下一個最接近的位置，以免關閉時間影響您的客戶。如果您的網站或 API 失敗，則 IBM CIS 會自動將通知傳送給您，並在還原時通知您。


![reliability-graphic.png](images/reliability-graphic.png)

以下是快速特性概觀：

## 可靠性特性
{:#cis-reliability-features}

 * 廣域負載平衡 
 * 用於負載平衡的 Proxy 及非 Proxy 選項
 * 原點儲存區及性能監視器
 * DNS 管理
 
### 摘要
{:#cis-reliability-features-summary}
 
  * 性能監視器會檢查原點儲存區是否性能良好。
  * 如果性能監視失敗，則會將您的要求重新遞送至性能良好的原點。
  * Web 服務或 API 失敗時，以及還原時，您都會收到通知。
