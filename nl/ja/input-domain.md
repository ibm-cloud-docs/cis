---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain Input information, IBM Cloud Internet Service, Domain Name

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# ドメインに関する情報の入力
{:#input-information-about-your-domain}

保護してグローバル・ロード・バランシングを提供する対象のドメインに関する情報を入力します。

1. 「開始」画面の左側の**「概要」**をクリックします。 ドメイン・ネーム (またはサブドメイン・ネーム) を入力して**「ドメインの追加」**をクリックします。 
    
    <img src="images/reliability3.png" alt="図面" style="width: 300px;"/>
    
    IBM Cloud Internet Service は DNS 登録機関ではないため、このドメイン (またはサブドメイン) を事前に作成しておく必要があります。
    {:note}

    「サービス詳細 (Service Details)」セクションの下に、新規追加されたドメインが最初は「処理待ち」の状態で表示されます。 

    <img src="images/reliability4.png" alt="図面" style="width: 300px;"/>    

2. 各 DNS 登録者でドメインの管理ページへナビゲートし、NS レコードを定義することでドメイン/サブドメインを IBM ネーム・サーバーに代理委任します。

情報が DNS データベース内に複製されるまで、最大 24 時間待たなければならない場合があります。 完了すると、ドメインの状態が「アクティブ」に変わります。 

<img src="images/reliability5.png" alt="図面" style="width: 300px;"/>    
