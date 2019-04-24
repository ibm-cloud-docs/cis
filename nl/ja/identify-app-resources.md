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

# アプリケーション・サーバーの識別
{:#identify-your-application-resources}

起点プールやヘルス・チェック・メカニズムなど、アプリケーションのリソースを識別します。
 
1. **「起点プール」**セクションにナビゲートし、**「プールの作成」**をクリックして新規起点プールを定義します。 

   起点プールは、アプリケーションをお客様に配信するサーバー・リソースです。 
   
2. 起点プールに名前を割り当て、以前に定義したヘルス・チェック・メカニズムを選択します。アプリケーション・サーバーを起点として追加します。**「起点の追加」**をクリックすると、1 つ以上の起点を追加できます。 

   IBM Cloud Load Balancer などのローカル・ロード・バランサーの後ろにアプリケーション・サーバーが配置されている場合は、個々のサーバーを追加するのではなく、ロード・バランサーの FQDN または仮想 IP を起点として追加してください。
   {:note}
   
3. **「リソースのプロビジョン (Provision Resource)」**をクリックし、起点プールの作成を完了します。  

   <img src="images/reliability8.png" alt="図面" style="width: 300px;"/>
   
   起点プールは最初は**「異常 (Unhealthy)」**として表示されます。この状態は、システムがヘルス・チェックを問題なく完了した後、**「正常」**に変わります。状態の変化を確認するには、ブラウザーを最新表示する必要がある場合があります。 
   
   <img src="images/reliability9.png" alt="図面" style="width: 300px;"/>
   
   起点プール内に複数の起点がある場合、正常な起点のしきい値を使用して、プールの正常性を宣言する前に正常な状態になくてはならない起点の最小数を指定します。
   {:note}
   
4. 存在するアプリケーション・ファームの数と同数の起点プールを定義します。これらのファームは同じ地域にあっても、異なる地域にあってもかまいません。この例では、米国の西海岸と東海岸にあるアプリケーション・ファームを示す 2 つの起点プールを作成します。 

   <img src="images/reliability10.png" alt="図面" style="width: 300px;"/>
