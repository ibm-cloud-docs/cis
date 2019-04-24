---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain Input information, IBM Cloud Internet Services, Global Load balancing

subcollection: cis

---


{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# 使用來自 IBM Cloud Internet Services 的「廣域負載平衡」來改善應用程式可靠性及可調整性
{:#improving-application-reliability-and-scalability-with-global-load-balancing-from-ibm-cloud-internet-services}

如果您有電子商務網站，或是管理的應用程式需要讓一般使用者隨時都能存取，則您可能會關心應用程式的全天候可用性及效能。 

IBM Cloud Internet Services (CIS) 提供的廣域負載平衡功能可協助改善應用程式的可靠性及可調整性，同時提供最好的一般使用者體驗。本手冊提供廣域負載平衡配置的逐步演練。  

## 您將達成的目標
{:#what-you-accomplish}

在此「逐步」說明中，您將學習如何配置與下列圖解類似的配置。

<img src="images/reliability1.png" alt="圖片" style="width: 300px;"/>

在此範例中，應用程式資源會部署在兩個資料中心位置，一個在美國西部，另一個在美國東岸。一般使用者可從世界各地存取此應用程式。 

作業|說明
------------- | -------------
[建立 CIS 實例](/docs/infrastructure/cis?topic=cis-create-your-ibm-cloud-internet-services-cis-instance)|從使用「IBM 客戶入口網站」建立 IBM Cloud Internet Services (CIS) 實例開始。|
[輸入您網域的相關資訊](/docs/infrastructure/cis?topic=cis-input-information-about-your-domain)|針對您要保護並為其提供廣域負載平衡的網域，輸入其相關資訊。
[開始廣域負載平衡器配置](/docs/infrastructure/cis?topic=cis-begin-global-load-balancer-configuration)|開始配置「廣域負載平衡器」。
[識別應用程式資源](/docs/infrastructure/cis?topic=cis-identify-your-application-resources)|識別應用程式的資源，例如原點儲存區及性能檢查機制。
[定義廣域負載平衡器](/docs/infrastructure/cis?topic=cis-define-the-global-load-balancer)|定義廣域負載平衡器配置，方法為指定主機名稱、新增並調整原點儲存區，然後定義其他規則來控制如何將資料流量提供給用戶端。
