---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: WAF Custom Rules, Custom WAF Rules

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# WAF カスタム・ルール
{:#waf-custom-rules}

**「セキュリティー」>「Web アプリケーション・ファイアウォール」>「カスタム・ルール」**から「カスタム WAF ルール (Custom WAF Rules)」にナビゲートします。WAF ルールは、エンタープライズ・プランで使用できます。また、お客様の固有の要件や Web サイトのトラフィック・パターンに基づいて作成されます。つまり、要求の特性を任意に組み合わせてブロックすることができます。 

カスタム WAF ルールは、IBM WAF にカバーするルールがなく、攻撃者がお客様の Web サイトの構造を特にターゲットにした特定のパターンまたはユーザー・エージェントを用いているような状況にも対応します。このような状況では、お客様の Web 特性に合わせたカスタム・ルールを作成できます。

## カスタム・ルールの要求
{:#request-a-custom-rule}

ルールを要求するには、ルール要件またはトラフィック・パターンを記載した E メールを wafsup@us.ibm.com 宛てにお送りください。 

以下のような情報をできるだけ多く提供してください。
* 報告済みの悪意のある要求の約 100 件のサンプルを示すアクセス・ログ。
* ブロックできる、またはトリガーできる何かが要求に含まれているかどうか判断するための POST データを含むサンプル POST 要求 (要求に POST 本文がある場合)。
* 要求を即座にブロックするか、あるいは誤検出の可能性がある場合はチャレンジするか。
* これらのルールを適用する特定のドメイン。
* ルールをデフォルトでオンにするか、オフにするか。

カスタム WAF ルールを作成した後、それらの効果を得られるようにするため、すべてのカスタム・ルールを有効にする必要があります。
{:note}
