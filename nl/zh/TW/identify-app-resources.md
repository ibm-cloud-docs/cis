---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: origin pools, application resources, Origin Pools section

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# 識別應用程式資源
{:#identify-your-application-resources}

識別應用程式的資源，例如原點儲存區及性能檢查機制。
 
1. 導覽至**原點儲存區**區段，然後按一下**建立儲存區**，以定義新的原點儲存區。 

   原點儲存區是將應用程式遞送至用戶端的伺服器資源。 
   
2. 將名稱指派給「原點儲存區」，然後選取先前定義的性能檢查機制。新增應用程式伺服器作為「原點」。您可以按一下**新增原點**，來新增一個以上的「原點」。 

   如果您的應用程式伺服器位於本端負載平衡器（例如 IBM Cloud Load Balancer）後面，則要將負載平衡器的 FQDN 或虛擬 IP 新增為「原點」，而非新增個別伺服器。
{:note}
   
3. 按一下**佈建資源**，以完成「原點儲存區」的建立。  

   <img src="images/reliability8.png" alt="圖片" style="width: 300px;"/>
   
   一開始，「原點儲存區」會顯示為**性能不佳**。在系統順利完成性能檢查之後，它的狀態會變更為**性能良好**。您可能需要重新整理瀏覽器才能看到狀態變更。 
   
   <img src="images/reliability9.png" alt="圖片" style="width: 300px;"/>
   
   如果您的「原點儲存區」內有多個原點，請使用性能良好原點臨界值，以指定在宣告儲存區性能良好之前必須是性能良好的原點數目下限。
{:note}
   
4. 定義與您擁有的應用程式伺服器陣列數目一樣多的原點儲存區。這些伺服器陣列可能在相同的或不同的地理區域內。在我們的範例中，我們將建立兩個原點儲存區，代表位於美國西部和東岸的應用程式陣列。 

   <img src="images/reliability10.png" alt="圖片" style="width: 300px;"/>
