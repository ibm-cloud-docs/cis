---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIDR blocks, Whitelist Block Challenge, IBM Cloud Internet Services, security features

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# IBM Cloud Internet Services (CIS) を使用して作業をセキュアにする方法
{:#how-cis-keeps-your-work-secure}

IBM CIS は、処理能力やサーバー・リソースの消耗の原因となる脅威をブロックし、悪意のあるボットやクローラーを制限する、グローバルに分散されたクラウド・サービスです。 IBM CIS は、グローバル HTTP(S) リバース・プロキシーおよび管理対象 DNS サービス・プロバイダーとして機能します。 Web トラフィックは、パフォーマンスとセキュリティーの両方を最適化するように、インテリジェント・グローバル・ネットワーク内で経路指定されます。

![security-graphic.png](images/security-graphic.png)

機能の概要を以下に示します。

## セキュリティー機能
{:#cis-security-features}

 * セキュリティー機能に使用するプロキシー [DNS レコード](/docs/infrastructure/cis?topic=cis-dns-concepts#proxying-dns-records)または [GLB](/docs/infrastructure/cis?topic=cis-global-load-balancer-glb-concepts)。これにより、サーバーを通過するトラフィックやデータを監視できます。
### Web アプリケーション・ファイアウォール (WAF)
{:#cis-web-application-firewall}

 * WAF は、[OWASP](/docs/infrastructure/cis?topic=cis-owasp-rule-set-for-waf) と [CIS](/docs/infrastructure/cis?topic=cis-waf-settings#cis-rule-set-for-waf) の 2 つのルール・セットを介して実装されます。
### 無制限の DDoS 緩和
{:#cis-unlimited-ddos-mitigation}

 * DDoS 緩和は通常、攻撃されたときにコストが増える可能性があり、費用のかかるサービスと言えます。IBM では、CIS をご利用のお客様に追加コストなしで無制限の DDoS 緩和を提供いたします。

## セキュリティー規格とプラットフォーム
{:#security-standards-and-platform}

 * TLS (SHA2 および SHA1)
 * IPv6
 * HTTP/2 および SPDY

## DNS
{:#cis-dns}

 * グローバル・エニーキャスト・ネットワーク
 * DNSSEC

## ネットワーク攻撃と緩和
{:#network-attacks-and-mitigation}

一般に、検出される攻撃は 2 つのカテゴリーに分類されます

| レイヤー 3 またはレイヤー 4 の攻撃 | レイヤー 7 の攻撃 |
|------------------------------|-----------------|
|これらの攻撃には、ICMP フラッディングなどの ISO レイヤー 3 (ネットワーク層) のトラフィックのフラッディングや、TCP SYN フラッディング や反射型 UDP フラッディングなどのレイヤー 4 (トランスポート層) のトラフィックのフラッディングが含まれます。 |これらは、GET フラッディングなど、ISO レイヤー 7 (アプリケーション層) の悪意のある要求を送信する攻撃です。  |
| エッジで自動的にブロックされます | これらは防御モード、WAF、およびセキュリティー・レベル設定によって対処します |

## IP ファイアウォール
{:#cis-ip-firewall}

IBM Cloud Internet Services では、大量のトラフィック、特定の要求者グループ、特定の要求 IP からドメイン、URL、およびディレクトリーを保護できるように、トラフィックを制御するためのいくつかのツールを提供しています。このセクションでは、利用可能なツールをご紹介します。

### IP ルール
{:#cis-ip-rules}

IP ルールでは、特定の IP アドレス、IP 範囲、特定の国、特定の ASN、および特定の CIDR ブロックのアクセスを制御できます。着信要求に対して以下のアクションを実行できます。
  * ホワイトリスト 
  * ブロック 
  * チャレンジ (Captcha) 
  * JavaScript チャレンジ (IUAM チャレンジ)

例えば、特定の IP が悪意のある要求を送信していることに気付いた場合、IP アドレスでそのユーザーをブロックできます。

### ユーザー・エージェント・ブロッキング・ルール
{:#user-agent-blocking-rules}

ユーザー・エージェント・ブロッキング・ルールによって、選択したユーザー・エージェント・ストリングに対してアクションを実行できます。この機能は、前述のドメイン・ロックダウンのように機能します。ただし、このブロックでは IP ではなく着信ユーザー・エージェント・ストリングを調べる点が異なります。IP ルールで確立したのと同じアクション・リスト (ブロック、チャレンジ、JS チャレンジ) を使用して、一致した要求を処理する方法を選択できます。ユーザー・エージェント・ブロッキングはゾーン全体に適用されることに注意してください。ドメイン・ロックダウンでできるのと同じ方法でサブドメインを指定することはできません。

このツールは、疑わしいと思われるユーザー・エージェント・ストリングをブロックするのに役立ちます。 

### ドメイン・ロックダウン
{:#cis-domain-lockdown}

ドメイン・ロックダウンでは、特定の IP アドレスや IP 範囲でホワイトリストを作成し、その他すべての IP がブラックリストに含められるかのようにすることができます。ドメイン・ロックダウンでは、以下をサポートします。

  * 特定のサブドメイン。例えば、IP `1.2.3.4` にドメイン `foo.example.com` へのアクセスを許可し、IP `5.6.7.8` にドメイン `bar.example.com` へのアクセスを許可します (逆を許可する必要はありません)。
  * 特定の URL。例えば、IP `1.2.3.4` にディレクトリー `example.com/foo/*` へのアクセスを許可し、IP `5.6.7.8` にディレクトリー `example.com/bar/*` へのアクセスを許可します (逆を許可する必要はありません)。この機能は、アクセス・ルールをより細かく設定する必要がある場合に役立ちます。IP ルールでは、ブロックを現行のドメインのすべてのサブドメインに適用するか、アカウントのすべてのドメインに適用することができますが、URI を指定することはできないからです。

### チャレンジ・パッセージ
{:#cis-challenge-passage}

**「拡張」**セキュリティー設定にあるこの設定により、チャレンジまたは JavaScript チャレンジをパスした訪問者が、もう一度チャレンジの対象となるまでに、どれほどの期間サイトにアクセスできるかを制御できます。これは訪問者の IP に基づくため、WAF ルールによって提供されるチャレンジには適用されません。WAF ルールは、ユーザーがサイトで実行する操作に基づくためです。

### ブラウザーの完全性チェック
{:#cis-browser-integrity-check}

この設定は、**「拡張」**セキュリティー設定にあります。ブラウザー保全性チェックでは、スパマーがよく不正使用する HTTP ヘッダーを探します。 ご使用のページに対してそうしたヘッダーを含むトラフィックがアクセスするのを拒否します。 また、ユーザー・エージェントを持たない訪問者や、非標準のユーザー・エージェントを追加している (この手法は、悪用ボット、クローラー、または API でよく使用される) 訪問者をブロックするか、チャレンジを行います。
