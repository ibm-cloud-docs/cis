---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: range application, tls encryption, ddos protection, global tcp proxy

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# 範囲
{:#cis-range}

「範囲」機能は、DDoS 対策、ロード・バランシング、およびコンテンツの加速を、任意の TCP ベースのプロトコルにもたらします。
「範囲」は、CIS/Cloudflare のエッジ・ノードで実行されるグローバル TCP プロキシーです。 

「範囲」は、以下の目的に使用できます。 
* TCP ポートやプロトコルを**レイヤー 3 およびレイヤー 4 の DDoS** 攻撃から保護する。 
* **TLS 暗号化**を有効にすることで、機密データのスヌープや窃盗を防ぐ。
* CIS IP Firewall と統合することで、IP アドレスまたは IP 範囲全体を、TCP サービスに届かないようにブロックしたり、チャレンジしたりする。 
* TCP ヘルス・チェック、フェイルオーバー、およびステアリング・ポリシーを搭載したロード・バランサーを構成して、トラフィックが流れるべき場所を指示する。

## 「範囲」の概説
{:#getting-started-with-range}

「範囲」は、エンタープライズ版でのみ、帯域幅使用量ごとの追加コストでご利用いただけます。
{:note}

### アプリケーションの追加
{:#range-add-an-application}
以下のステップを実行して、アプリケーションを追加します。

1. **「セキュリティー」>「範囲」**に移動します。
1. **「アプリケーションの追加 (Add application)」**ボタンをクリックします。 
1. 最初の入力フィールドにアプリケーション名を入力します。アプリケーションが、ご使用の CIS ドメインの DNS 名に関連付けられます。
1. 次の入力フィールドにエッジ・ポートを入力します。これらのアドレスへの着信接続がこのポート上で listen されます。これらのアドレスへの接続はご使用の起点にプロキシー化されます。(プロキシー化は、ポート 21 を除くすべてのポートでサポートされています。)
1. 「起点」セクションで、TCP アプリケーションの起点 IP とポートを入力します。既存のロード・バランサーを選択することもできます。
1. IP Firewall を有効にします。有効にすると、「ブロック」または「ホワイトリスト」アクションを含むファイアウォール・ルールがこのアプリケーションに強制されます。国ベースや ASN ベースのルールは、まだサポートされていません。
1. PROXY Protocol v1 をサポートするプロキシーをインラインで持っている場合、プロキシー・プロトコルを有効にします。この機能は、真のクライアント IP の知識が必要なサービスを実行している場合に役立ちます。ほとんどの場合、この設定は無効のままにします。
1. **「プロビジョン」**をクリックします。

プロキシー・プロトコルは、すべての接続にクライアント IP アドレスとポートを報告するヘッダーを前に付けます。プロキシー・プロトコルのヘッダーは、次の形式です。
  * PROXY_STRING + シングル・スペース + INET_PROTOCOL + シングル・スペース + CLIENT_IP + シングル・スペース + PROXY_IP + シングル・スペース + CLIENT_PORT + シングル・スペース + PROXY_PORT + "\r\n"
  * IPv4 アドレスに対するプロキシー・プロトコルの行の例は次のとおりです。
    `PROXY TCP4 192.0.2.0 192.0.2.255 42300 443\r\n`
  * IPv6 アドレスに対するプロキシー・プロトコルの行の例は次のとおりです。
    `PROXY TCP6 2001:db8:: 2001:db8:ffff:ffff:ffff:ffff:ffff:ffff 42300 443\r\n`
   
「範囲」アプリケーションをプロビジョニングすると、アプリごとに使用する帯域幅の量に応じて追加コストが発生します。
{:note}

ユーザーのアプリケーションが、次のプロパティーとともにタイルに表示されるようになりました。
  * アプリケーション名
  * エッジ・ポート
  * 起点 & ポート
  * 過去 1 時間の接続数 (毎分ポーリングを実施)
  * 過去 1 時間のスループット (毎分ポーリングを実施)
  * オーバーフロー・メニュー (右上隅) では、次の操作を行えます。 
    * アプリケーションの編集
    * 指定したアプリケーションのメトリックの表示
    * アプリケーションの削除 
    
「範囲」アプリケーションが作成されると、それに固有の IPv4 アドレスと IPv6 アドレスが割り当てられます。これらの IP アドレスは静的ではなく、変更される可能性があります。割り当てられた IP アドレスは、DNS を使用して判別できます。DNS 名は常に、アプリケーションに割り当てられた IP アドレスを戻します。     
    
### メトリックの表示
{:#range-view-metrics}
ユーザーのアプリケーションは、Cloudflare/CIS を通じて TCP トラフィックをプロキシーできるようになりました。

**「メトリック」>「範囲」**に移動して、アプリケーションへの接続の数とスループットのトラフィックを表示します。
グラフには、最大で 10 個のアプリケーションのメトリックが表示されます。
{:note}

アプリケーションのメトリックはグラフ・キー、または**「アプリケーションの選択」**ボタンをクリックして切り替えることができます。メトリック・データの時間フレームは、ドロップダウン・メニューから変更できます。

## 範囲 AppTile
{:#range-apptiles}
アプリをいくつか作成すると、**「セキュリティー」>「範囲」**ページにアプリケーション・タイルが表示されます。アプリケーション・タイルには、以下の情報が含まれます。
* アプリケーション名
* エッジ・ポート
* 起点 & ポート
* 過去 1 時間の接続数 (毎分ポーリングを実施)
* 過去 1 時間のスループット (毎分ポーリングを実施)


アプリケーション・タイルには、上部隅にオーバーフロー・メニューも含まれます (3 つのドット)。オーバーフロー・メニューには、次の操作のためのオプションがあります。
* アプリケーションの編集
* 指定したアプリケーションのメトリックの表示
  * **「メトリック」>「範囲」**ページが開き、そのアプリケーションのメトリックのみが表示されます
* アプリケーションの削除


## API の使用例
{:#range-api-usage-examples}
「範囲」を使用した、アプリケーションの作成とリストの例を示します。

### 「範囲」アプリの作成
{:#create-range-app}
「範囲」アプリで起点を指定する方法は 2 つあります
1. 起点 IP - パラメーター `origin_direct` を使用します
2. ロード・バランサー - パラメーター `origin_dns` および `origin_port` を使用します

**要求:**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_direct":["tcp://172.0.2.1:22"],"proxy_protocol":true,"ip_firewall":true}'

```
**応答:**
```
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_direct": [
            "tcp://172.0.2.1:22"
        ],
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:33:09.190606Z",
        "modified_on": "2019-01-09T17:33:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```

**要求:**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_dns": {"name": "test"},"proxy_protocol":true,"ip_firewall":true, "origin_port": 43}'

```
**応答:**
```
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_dns": {
          "name": "test"
        },
        "origin_port": 43,
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:39:09.190606Z",
        "modified_on": "2019-01-09T17:39:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```

**DNS 名:** アプリケーションがご使用のドメインの DNS 名に関連付けられます。

**プロトコル/エッジ・ポート:** アプリケーションを実行するポート。これらのアドレスへの接続はご使用の起点にプロキシー化されます。

**起点ダイレクト:** アプリケーションを実行する場所の IP と、エッジから起点までトラフィックを通すポート。

**IP Firewall:** 有効にすると、ブロック・アクションを含むファイアウォール・ルールがこの「範囲」アプリケーションに強制されます。

**PROXY Protocol:** PROXY Protocol v1 をサポートするプロキシーをインラインで持っている場合に有効にします。ほとんどの場合、この設定は無効のままにします。

**起点 DNS:** 起点として設定するロード・バランサーの名前。

**起点ポート:** サービスのポート。 

### すべてのアプリのリスト
{:#range-list-all-apps}

**要求:**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps
```

**応答:**
```
{
    "result": [
        {
            "id": "4f70c3d4f20546b79135b898295e8093",
            "protocol": "tcp/22",
            "dns": {
                "type": "CNAME",
                "name": "ssh.example.com"
            },
            "origin_direct": [
                "tcp://172.0.2.1:22"
            ],
            "ip_firewall": true,
            "proxy_protocol": true,
            "created_on": "2019-01-09T17:33:09.190606Z",
            "modified_on": "2019-01-09T17:33:09.190606Z"
        }
    ],
    "success": true,
    "errors": [],
    "messages": []
}
```

### 特定の「範囲」アプリのリスト
{:#range-list-a-specific-range-app}
**要求:**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps/4f70c3d4f20546b79135b898295e8093
```

**応答:**
起点 IP を使用するアプリ
```
{
    "result": {
        "id": "4f70c3d4f20546b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_direct": [
            "tcp://172.0.2.1:22"
        ],
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:33:09.190606Z",
        "modified_on": "2019-01-09T17:33:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
} 
```

ロード・バランサーを使用するアプリ
```
{
    "result": {
        "id": "555359036e7f4acc82d69b916f62caba",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_dns": {
            "name": "test_update"
        },
        "origin_port": 76,
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-10T22:26:47.167008Z",
        "modified_on": "2019-01-10T22:26:47.167008Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}

```
