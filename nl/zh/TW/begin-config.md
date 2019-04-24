---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: global load balancer configuration, glb configuration

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}

# 開始廣域負載平衡器配置
{:#begin-global-load-balancer-configuration}

開始配置「廣域負載平衡器」。

1. 在**可靠性**區段下，選取**廣域負載平衡器**。 
    
    <img src="images/reliability6.png" alt="圖片" style="width: 300px;"/>

2. 向下捲動至「性能檢查」區段。 

   這項配置是選用項目。如果您未定義任何自訂性能檢查，則系統將使用 "/" 作為預設性能檢查路徑。
   {:note}

3. 按一下**建立性能檢查**按鈕來定義一個自訂性能檢查。   

   提供您要執行性能檢查的路徑。您可以使用 HTTP 或 HTTPS 通訊協定來進行性能檢查。 
   
4. 在**進階選項**下，您可以自訂其他參數，例如「進階」選項下的性能檢查間隔、重試次數、要求方法及回應內文。 
   
   <img src="images/reliability7.png" alt="圖片" style="width: 300px;"/>
   
5. 按一下**佈建資源**來完成性能檢查配置。 
