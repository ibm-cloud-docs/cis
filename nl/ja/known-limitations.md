---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: health checks, Free Trial plan, dedicated certificate, known issues

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 
{:note: .note} 
{:important: .important} 
{:deprecated: .deprecated} 
{:generic: data-hd-programlang="generic"}

# 既知の制限事項
{:#known-limitations}

 * Chrome の使用をお勧めします。
 
 * 無料トライアル・プランは 1 アカウントにつき 1 インスタンスに制限されています。リソース・インスタンスを作成してドメインを追加すると、CIS の新しいリソース・インスタンスを追加できなくなります。 この制限は、試用ドメインを削除してから再び同じリソース・インスタンスにドメインを追加しようとした場合にも適用されます。 この操作を行うと、エラーが表示されます。

 * このサービスの場合、別のプロバイダーで NS レコードを使用するサブドメインの委任だけをサポートしています。CNAME による委任はサポートしていません。
  
 * A、AAAA、および CNAME ワイルドカード・レコード (*) は、プロキシーを使用できません。

 * 専用の証明書を削除するときには、削除が完了するまでの短時間、それがリストに再表示されることがあります。
 
 * カスタムの専用証明書を注文した後にそのホスト名を変更するには、新しい証明書を注文してから、以前の証明書を削除する必要があります。 
 
 * 2 文字の国別コードを使用して作成される IP ルールは、`「チャレンジ」`アクションによってのみ作成できます。ある国からの訪問者をブロックするには、エンタープライズ・プランにアップグレードするか、完全にブロックするためのルールをサーバーに設定します。

## グローバル・ロード・バランサー
{:#known-limitations-glb}

 * Cloud Internet Services ではロード・バランサーのホスト名に下線文字 `_` を使用できますが、Kubernetes クラスターで `_` を使用することはできません。 

 * 標準プランでは、最大 5 つのロード・バランサー、プール、およびヘルス・チェックが許可されます。各プールには合わせて 6 つの起点を配置できますが、各 CIS インスタンスでは全体で 6 つの固有の起点だけが許可されます。

* 削除されたプールと起点のヘルス・チェック・イベントはフィルターに掛けることができませんが、テーブルには引き続き表示されます。

* ヘルス・チェック・イベントを`「プール・ヘルス」`によってフィルターに掛けた場合、`「機能低下」`プールは、技術的に正常であるため含まれます。ただし、それには 1 つ以上のクリティカルな起点が含まれている可能性があります。

* ヘルス・チェックに要求ヘッダー名を追加するときには、`Host` を使用します。ヘルス・チェックに小文字の `host` を使用すると失敗します。

## DNS
{:#known-limitations-dns}

 * DNS レコードのエクスポートには、非表示にする必要のある Cloudflare CNAME レコードが含まれています。これらのレコードは `_` で始まり、通常は、名前が同じで `_` が除去されている 2 番目のレコードがあります。
   ```
   Ex.
   _cf.generate.yourdomain.com 0	IN	CNAME address.alias.com
   cf.generate.yourdomain.com 0	IN	CNAME address2.alias.com
   ```
 
   適切にインポートするためには、これらのレコードをゾーン・ファイルから削除する必要があります。
 
 * CAA DNS レコードのエクスポートは正しく機能しません。
`<tag>` および `<value>` は 16 進でエンコードされます。 
 
    CAA `<flags>` `<tag>` `<value>`
  {:note}
   ```
   Ex.
   Original CAA record
   caa.yourdomain.com.	1	IN	CAA	0 issue "letsencrypt.org"
 
   Exported CAA record
   caa.yourdomain.com.	1	IN	CAA	0 6973737565 "6c657473656e63727970742e6f7267"
   ```
   これらのレコードは、インポートする前に、16 進から文字列に変換するか、または削除してから手動で追加する必要があります。

## ページ・ルール
{:#known-limitations-pagerules}

   * ページ・ルール ID が更新対象の JSON ストリングまたは JSON ファイルに含まれていない場合、IBM Cloud CLI 用の CIS プラグインを使用してページ・ルール設定を更新すると、エラーが発生することがあります。この回避策として、ID を含むページ・ルール用の完全な JSON 構成ファイルを使用して更新をサブミットします。
   * CIS UI を使用してページ・ルール設定を削除すると、UI で更新の成功が報告された場合でも、設定が削除されていないことがあります。この問題の回避策として、IBM Cloud CLI 用の CIS プラグインを使用して設定を削除し、ページ・ルール ID を JSON 更新文書に含めます。
      ```
      $> ibmcloud cis page-rule-update <domain-id> <rule-id> -j <file>
      ```
      JSON ファイルには、ID を含む完全なページ・ルール構成、および必要な更新が含まれている必要があります。
