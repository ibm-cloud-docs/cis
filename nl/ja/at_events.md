---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM Cloud Internet Services, CIS Activity Tracker events

subcollection: cis

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# CIS {{site.data.keyword.cloudaccesstrailshort}} イベント
{: #at_events}

{{site.data.keyword.cloudaccesstrailfull}} サービスを使用して、ユーザーやアプリケーションと {{site.data.keyword.cloud}} 内の IBM Cloud Internet Services (CIS) との対話の状況を追跡します。
{:shortdesc}

{{site.data.keyword.cloudaccesstrailfull_notm}} サービスは、{{site.data.keyword.cloud_notm}} のサービスの状態を変更するアクティビティーをユーザーが開始すると、そのアクティビティーを記録します。詳しくは、[{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla) を参照してください。




## イベントのリスト: DNS ドメイン
{: #events_dns_domain}

以下の表に、DNS ドメインに関連した、イベントを生成するアクションをリストします。

|アクション|説明|
|---|---|  
|internet-svcs.zones.create|DNS ドメインを作成します。|
|internet-svcs.zones.update|DNS ドメインを更新します。|
|internet-svcs.zones.delete|DNS ドメインを削除します。|
|internet-svcs.zones.activation_check.update|DNS ドメインのアクティベーション・チェックを実行します。|
|internet-svcs.zones.dnssec.update|DNS ドメインに関する DNSSEC を有効または無効にします。|

## イベントのリスト: DNS レコード
{: #events_dns_record}

以下の表に、DNS レコードに関連した、イベントを生成するアクションをリストします。

|アクション|説明|
|---|---|  
|internet-svcs.zones.dns_records.create|DNS レコードを作成します。|
|internet-svcs.zones.dns_records.update|DNS レコードを更新します。|
|internet-svcs.zones.dns_records.delete|DNS レコードを削除します。|
|internet-svcs.zones.dns_records_bulk.create|ゾーン・ファイルから DNS レコードをインポートします。|


## イベントのリスト: ロード・バランサー
{: #events_load_balancers}

以下の表に、ロード・バランサーに関連した、イベントを生成するアクションをリストします。

|アクション|説明|
|---|---|  
|internet-svcs.zones.load_balancers.create|グローバル・ロード・バランサーを作成します。|
|internet-svcs.zones.load_balancers.update|グローバル・ロード・バランサーを更新します。|
|internet-svcs.zones.load_balancers.delete|グローバル・ロード・バランサーを削除します。|
|internet-svcs.load_balancers.monitors.create|ヘルス・モニターを作成します。|
|internet-svcs.load_balancers.monitors.update|ヘルス・モニターを更新します。|
|internet-svcs.load_balancers.monitors.delete|ヘルス・モニターを削除します。|
|internet-svcs.load_balancers.pools.create|グローバル・ロード・バランサー・プールを作成します。|
|internet-svcs.load_balancers.pools.update|グローバル・ロード・バランサー・プールを更新します。|
|internet-svcs.load_balancers.pools.delete|グローバル・ロード・バランサー・プールを削除します。|


## イベントのリスト: キャッシュのパージ
{: #events_cache}

以下の表に、キャッシュのパージに関連した、イベントを生成するアクションをリストします。

|アクション|説明|
|---|---|  
|internet-svcs.zones.purge_cache.purge_all.update|ドメインのキャッシュに入れられたアセットをすべてエッジ・サーバーからパージします。|
|internet-svcs.zones.purge_cache.purge_by_urls.update|キャッシュに入れられたアセットを URL 別にエッジ・サーバーからパージします。|
|internet-svcs.zones.purge_cache.purge_by_cache_tags.update|キャッシュに入れられたアセットをキャッシュ・タグ別にエッジ・サーバーからパージします。|
|internet-svcs.zones.purge_cache.purge_by_hosts.update|キャッシュに入れられたアセットをホスト名別にエッジ・サーバーからパージします。|


## イベントのリスト: ページ・ルール
{: #events_page_rules}

以下の表に、ページ・ルールに関連した、イベントを生成するアクションをリストします。

|アクション|説明|
|---|---|  
|internet-svcs.zones.pagerules.create|ページ・ルールを作成します。|
|internet-svcs.zones.pagerules.update|ページ・ルールを更新します。|
|internet-svcs.zones.pagerules.delete|ページ・ルールを削除します。|


## イベントのリスト: ファイアウォール
{: #events_firewalls}

以下の表に、ファイアウォールに関連した、イベントを生成するアクションをリストします。

|アクション|説明|
|---|---|  
|internet-svcs.zones.firewall.waf.packages.groups.update|WAF ルール・セットのグループを有効または無効にします。|
|internet-svcs.zones.firewall.waf.packages.rules.update|WAF ルールを有効または無効にします。|
|internet-svcs.zones.firewall.access_rules.rules.create|ドメイン・レベルの IP ファイアウォール・ルールを作成します。|
|internet-svcs.zones.firewall.access_rules.rules.update|ドメイン・レベルの IP ファイアウォール・ルールを更新します。|
|internet-svcs.zones.firewall.access_rules.rules.delete|ドメイン・レベルの IP ファイアウォール・ルールを削除します。|
|internet-svcs.firewall.access_rules.rules.create|インスタンス・レベルの IP ファイアウォール・ルールを作成します。|
|internet-svcs.firewall.access_rules.rules.update|インスタンス・レベルの IP ファイアウォール・ルールを更新します。|
|internet-svcs.firewall.access_rules.rules.delete|インスタンス・レベルの IP ファイアウォール・ルールを削除します。|
|internet-svcs.zones.rate_limits.create|速度制限ルールを作成します。|
|internet-svcs.zones.rate_limits.update|速度制限ルールを更新します。|
|internet-svcs.zones.rate_limits.delete|速度制限ルールを削除します。|
|internet-svcs.zones.ua_rules.create|ユーザー・エージェント・ブロック・ルールを作成します。|
|internet-svcs.zones.ua_rules.update|ユーザー・エージェント・ブロック・ルールを更新します。|
|internet-svcs.zones.ua_rules.delete|ユーザー・エージェント・ブロック・ルールを削除します。|
|internet-svcs.zones.firewall.lockdowns.create|ドメイン・ロックダウン・ルールを作成します。|
|internet-svcs.zones.firewall.lockdowns.update|ドメイン・ロックダウン・ルールを更新します。|
|internet-svcs.zones.firewall.lockdowns.delete|ドメイン・ロックダウン・ルールを削除します。|

## イベントのリスト: ルーティング
{: #events_routing}

以下の表に、ルーティングに関連した、イベントを生成するアクションをリストします。

|アクション|説明|
|---|---|  
|internet-svcs.zones.routing.smart_routing.update	|スマート・ルーティングを有効または無効にします。|
|internet-svcs.zones.routing.tiered_caching.update	|階層型キャッシングを有効または無効にします。|

## イベントのリスト: 証明書パック
{: #events_certificate_packs}

以下の表に、証明書パックに関連した、イベントを生成するアクションをリストします。

|アクション|説明|
|---|---|  
|internet-svcs.zones.ssl.certificate_packs.create|専用の証明書を注文します。|
|internet-svcs.zones.ssl.certificate_packs.delete|専用の証明書を削除します。|


## イベントのリスト: カスタム証明書
{: #events_custom_certificate}

以下の表に、カスタム証明書に関連した、イベントを生成するアクションをリストします。

|アクション|説明|
|---|---|  
|internet-svcs.zones.custom_certificates.create|カスタム証明書をアップロードします。|
|internet-svcs.zones.custom_certificates.update|カスタム証明書を更新します。|
|internet-svcs.zones.custom_certificates.delete|カスタム証明書を削除します。|


## イベントのリスト: 設定
{: #events_settings}

以下の表に、構成の設定に関連した、イベントを生成するアクションをリストします。

|アクション|説明|
|---|---|  
|internet-svcs.zones.settings.cache_level.update|キャッシュ・レベルを変更します。|
|internet-svcs.zones.settings.browser_cache_ttl.update|ブラウザー・キャッシュの TTL を変更します。|
|internet-svcs.zones.settings.development_mode.update|開発モードを有効または無効にします。|
|internet-svcs.zones.settings.security_level.update|セキュリティー・レベルを変更します。|
|internet-svcs.zones.settings.ssl.update|SSL 設定を変更します。|
|internet-svcs.zones.settings.tls_1_2_only.update|TLS 1.2 サポートを有効または無効にします。|
|internet-svcs.zones.settings.waf.update|Web アプリケーション・ファイアウォールを有効または無効にします。|
|internet-svcs.zones.settings.cname_flattening.update|CNAME フラット化の設定を変更します。|
|internet-svcs.zones.settings.always_online.update|ドメインに関する失効コンテンツの提供を有効または無効にします。|
|internet-svcs.zones.settings.sort_query_string_for_cache.update|キャッシュ内のコンテンツの照会時に照会引数のソートを有効または無効にします。|
|internet-svcs.zones.settings.tls_1_3.update|TLS 1.3 設定を変更します。|
|internet-svcs.zones.settings.automatic_https_rewrites.update|HTTPS 自動再書き込みを有効または無効にします。
|internet-svcs.zones.settings.opportunistic_encryption.update|便宜的暗号化を有効または無効にします。|


## イベントを探す場所
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} イベントは、イベントが生成される {{site.data.keyword.cloud_notm}} 地域内にある {{site.data.keyword.cloudaccesstrailshort}} **アカウント・ドメイン**で使用可能です。



## 追加情報
{: #info}

IBM Cloud Internet Services (CIS) で生成される {{site.data.keyword.cloudaccesstrailshort}} イベントをモニターしているときに、追加情報が必要な API 要求を識別する場合は、そのイベント内の requestData フィールドを確認してください。サポート・チケットを開き、requestData 内の入手可能な **X-CORRELATION-ID** フィールドの値を組み込みます。
