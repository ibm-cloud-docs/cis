---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Helpful tools, whois, IPv4

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# CIS デプロイメントの管理に役立つツール
{:#helpful-tools-for-managing-your-cis-deployment}

IBM CIS デプロイメントの管理に役立つパブリック・ドメインの UNIX システム管理ツールがいくつか存在します。

## Sysadmin ツール
{:#cis-sysadmin-tools}

 * whois (ドメイン識別ツール)
 * dig (DNS ツール)
 * curl (HTTP および HTTPS ツール)
 * netcat (IP およびポート・ツール)
 * traceroute (ネットワーク・ツール)

## 外部テストとリモート・テストのための市販ツール
{:#commercial-tools-for-external-and-remote-testing}

 * GTMetrix (http)
 * Web ページ・テスト (http)
 * WhatsMyDNS (DNS ツール)
 * G Suite Toolbox (DNS および HTTP)

## ログと履歴を検索するツール
{:#tools-for-looking-at-logs-and-history}

 * HTTP アーカイブ・ファイル (HAR ファイル)


### `whois` の使用
{:#using-whois}

`whois` は UNIX システムのコマンド・ライン・ツールです。これを使用して、指定したドメイン名または IP アドレスのレジストラー情報を調べられます。例えば、ドメインの指定の権威サーバーや、特定の IP アドレスの所有者などを検索できます。

例:

`whois example.com`

`whois 8.8.8.8`

### `dig` の使用
{:#using-dig}

`dig` は UNIX のコマンド・ライン・ツールです。DNS 照会を実行し、特定ドメインの DNS レコードを確認できます。 このツールは `nslookup` に似ています。

このコマンドのスキーマは、「dig <recordtype. <domainname> <options>」です。

**例:**

`dig example.com`

`dig my.example.com`

`dig example.com +trace`

`dig NS example.com`

`dig example.com @ns.example.com`

### `cURL` の使用
{:#using-curl}

`cURL` は UNIX のコマンド・ライン・ツールです。URL 構文を使用してデータを転送できます。 HTTP 要求を作成したり、サーバー応答を比較したりするためによく使用されます。

このコマンドのスキーマは `curl -option1 -option2 http://example.com/url` です。

**例:**

`curl -svo /dev/null http://www.example.com`

`curl -svo /dev/null -A “USER_AGENT_STRING” http://www.example.com`

`curl -svo /dev/null -H “host: www.example.com” http://ORIGIN_IP`

`curl -svo /dev/null -H https://www.example.com --resolve www.example.com:443:ORIGIN_IP`

### `mtr` および `traceroute` の使用
{:#using-mtr-and-traceroute}

MTR と `traceroute` は UNIX のコマンド・ライン・ツールです。指定したホストまたは宛先サーバーへの特定のネットワーク・パスのパフォーマンスや遅延を測定できます。

**例:**

`mtr -rwc 20 example.com -T -4`
`mtr -rwc 20 8.8.8.8 -T -6`

`traceroute example.com -T -4`

`traceroute 8.8.8.8 -T -6`

| オプション | 定義 |
|---------|-----------|
| -c | 送信する ping の数を設定する |
| -T | TCP トレースルートを強制する (通常は ICMP) |
| -4 | IPv4 の使用を強制する |
| -6 | IPv6 の使用を強制する |

### HAR ファイルの生成
{:#generating-a-har-file}

HAR ファイルは Web ブラウザーからの HTTP 要求の記録です。 Chrome などのブラウザーには、HAR ファイルの作成を設定できる開発者ツールのセクションがあります。
