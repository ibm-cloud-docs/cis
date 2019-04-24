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

# IBM Cloud Internet Services からのグローバル・ロード・バランシングでのアプリケーションの信頼性と拡張容易性の向上
{:#improving-application-reliability-and-scalability-with-global-load-balancing-from-ibm-cloud-internet-services}

e-コマースの Web サイトをお持ちの場合や、エンド・ユーザーから常時アクセス可能な状態でなければならないアプリケーションをホストしている場合、アプリケーションの 1 日 24 時間 週 7 日の可用性とパフォーマンスに関心をお持ちでしょう。 

IBM Cloud Internet Services (CIS) で使用可能なグローバル・ロード・バランシング機能は、最高のエンド・ユーザー・エクスペリエンスを提供しながら、アプリケーションの信頼性と拡張容易性の向上を支援します。 このガイドは、グローバル・ロード・バランシングの構成のウォークスルーを提供します。  

## このガイドで達成できること
{:#what-you-accomplish}

このステップバイステップでは、以下に図示するようなセットアップの構成方法を学びます。

<img src="images/reliability1.png" alt="図面" style="width: 300px;"/>

この例では、アプリケーション・リソースは 2 つのデータ・センターの場所 (1 つは米国西海岸、もう 1 つは米国東海岸) にデプロイされます。 エンド・ユーザーは世界中からこのアプリケーションにアクセスする可能性があります。 

タスク  | 説明
------------- | -------------
[CIS インスタンスの作成](/docs/infrastructure/cis?topic=cis-create-your-ibm-cloud-internet-services-cis-instance) | まず、IBM カスタマー・ポータルを使用して IBM Cloud Internet Services (CIS) インスタンスを作成することから始めます。|
[ドメインに関する情報の入力](/docs/infrastructure/cis?topic=cis-input-information-about-your-domain) | 保護してグローバル・ロード・バランシングを提供する対象のドメインに関する情報を入力します。
[グローバル・ロード・バランサーの構成の開始](/docs/infrastructure/cis?topic=cis-begin-global-load-balancer-configuration) | グローバル・ロード・バランサーの構成を始めます。
[アプリケーション・リソースの識別](/docs/infrastructure/cis?topic=cis-identify-your-application-resources) | 起点プールやヘルス・チェック・メカニズムなど、アプリケーションのリソースを識別します。
[グローバル・ロード・バランサーの定義](/docs/infrastructure/cis?topic=cis-define-the-global-load-balancer) | ホスト名を指定し、起点プールを追加して調整し、トラフィックが顧客に提供される方法を制御するための追加ルールを定義することにより、グローバル・ロード・バランサーの構成を定義します。
