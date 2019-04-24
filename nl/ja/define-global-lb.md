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

# グローバル・ロード・バランサーの定義
{:#define-the-global-load-balancer}

ホスト名を指定し、起点プールを追加して調整し、トラフィックが顧客に提供される方法を制御するための追加ルールを定義することにより、グローバル・ロード・バランサーの構成を定義します。

1. 右側の「ロード・バランサーの作成 (Create load balancer)」ボタンをクリックしてグローバル・ロード・バランサーを作成します。  

2. ドメインのホスト名を指定して、必要に応じて TTL 値を調整し (デフォルトは 60 秒)、**「プールの追加 (Add Pool)」**を使用して起点プールを追加します。 

   <img src="images/reliability11.png" alt="図面" style="width: 300px;"/>
   
   **注:** ドメイン・ネームと組み合わせたホスト名が、アプリケーションの完全修飾ドメイン・ネーム (FQDN) を形成します。 エンド・ユーザーはこの FQDN を使用してお客様のアプリケーションに接続します。 
   
3. プールの左側の上矢印と下矢印をクリックして、起点プールの相対優先度を調整します。 エンド・ユーザーからのアプリケーション要求は、これらの起点プールによりラウンドロビン形式で提供されます。 
   
   <img src="images/reliability12.png" alt="図面" style="width: 300px;"/>   
   
4. オプションで、異なる地域から顧客にトラフィックがどのように提供されるかを制御するための追加ルールを定義することもできます。 下の例では、南米大陸の南部から到着するお客様は、米国西海岸の起点プールに経路指定されます。 これらのルールを使用して、お客様を最寄りの地域へ誘導できます。 これらのいずれかの地域に障害が発生すると、その地域のエンド・ユーザーがダウンタイムによる影響を受けないように、他の使用可能な正常な場所へ要求が経路指定されます。 

   <img src="images/reliability13.png" alt="図面" style="width: 300px;"/>   
   
5. **「リソースのプロビジョン (Provision Resource)」**をクリックして、グローバル・ロード・バランサーの構成を完了します。 
6. 最後に、モバイル・ブラウザーのウィンドウに `FQDN URL` と入力して、アプリケーションへの接続性を検証します。 接続できた場合はウェルカム・メッセージが表示されます。
