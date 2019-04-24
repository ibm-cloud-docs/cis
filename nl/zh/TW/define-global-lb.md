---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: global load balancer, global load balancer configuration

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# 定義廣域負載平衡器
{:#define-the-global-load-balancer}

定義廣域負載平衡器配置，方法為指定主機名稱、新增並調整原點儲存區，然後定義其他規則來控制如何將資料流量提供給用戶端。

1. 按一下右側的「建立負載平衡器」按鈕來建立「廣域負載平衡器」。  

2. 指定網域的主機名稱，並在需要時調整 TTL 值（預設值為 60 秒），然後使用**新增儲存區**來新增「原點儲存區」。 

   <img src="images/reliability11.png" alt="圖片" style="width: 300px;"/>
   
   **附註：**與「網域」名稱結合的主機名稱會構成應用程式的完整網域名稱 (FQDN)。您的一般使用者會使用此 FQDN 來連接至您的應用程式。 
   
3. 調整原點儲存區的相對優先順序，方法為按一下儲存區左側的上下箭頭。這些原點儲存區會以循環式方式為來自一般使用者的應用程式要求提供服務。 
   
   <img src="images/reliability12.png" alt="圖片" style="width: 300px;"/>   
   
4. 您可以選擇性地定義其他規則，來控制如何將資料流量提供給來自不同地理區域的用戶端。在下面範例中，從南美洲地區傳過來的用戶端會遞送至「美國西岸」原點儲存區。您可以使用這些規則，將用戶端引導至最接近的地區。如果其中任一個地區失敗，則要求會遞送至其他可用的正常位置，以免一般使用者受到關閉時間影響。 

   <img src="images/reliability13.png" alt="圖片" style="width: 300px;"/>   
   
5. 按一下**佈建資源**來完成廣域負載平衡器的配置。 
6. 最後，在行動式瀏覽器視窗中鍵入 `FQDN URL` 來驗證與應用程式的連線。如果可以連接，您將看到歡迎訊息。
