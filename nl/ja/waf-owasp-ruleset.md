---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: OWASP Rule Set, Rule Set

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# WAF 用の OWASP ルール・セット
{:#owasp-rule-set-for-waf}

OWASP ルール・セットには、一般的な攻撃検出ルールが含まれています。OWASP ルールは、一般的な攻撃カテゴリーの多くから保護します。これには、SQL インジェクション、クロスサイト・スクリプティング、ロケール・ファイル・インジェクションなどが含まれます。IBM CIS は、これらのルールを提供しますが、キュレートすることはありません。OWASP は、優れたセキュリティー・ベースラインを提供する業界標準となっています。詳細については、以下のリンクを参照してください。
  * [Github での OWASP](https://github.com/SpiderLabs/owasp-modsecurity-crs)
  * [OWASP.org](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project)

## OWASP の管理
{:#managing-owasp}

[CIS ルール・セット](/docs/infrastructure/cis?topic=cis-cis-rule-set-for-waf)とは異なり、OWASP では感度を設定できます。
要求は、それらに関連付けられた「高」から「低」までの重大度が設定された一連の OWASP ルールをトリガーすることができます。最終スコアは、トリガーされたすべてのルールに基づいて計算されます。最終スコアを計算した後、CIS はそのスコアを最初に選択した感度しきい値と比較して、要求をブロックするか、許可します。

|感度スコア| トリガーしきい値|
|------|---------------|
|低   |  60 以上|
|中   |  40 以上|
|高   |  25 以上|

OWASP 感度を`「低」`に設定することをお勧めします。`「高」`に設定した場合、CIS のログを確認し、お客様のアプリケーションに合わせて OWASP ルール・セットを微調整してください。

_「無効化」_、_「シミュレート」_、_「チャレンジ」_、または_「ブロック」_に設定できる CIS ルール・セットとは異なり、OWASP ルールは_「オン」_ または_「オフ」_でしか切り替えられないことに注意してください。

## 誤検出の処理方法
{:#owasp-false-positives}

変数または値が_「真」_または _「正」_と評価しても、実際には負だった場合に、誤検出が発生します。WAF のコンテキストでは、誤検出は、悪意のあるものとして誤って評価されたために、要求がブロックされることを意味します。

誤検出を処理し、今後同じ誤検出が発生しないようにするには、それらを発見して修正する方法について知っている必要があります。ブロックされた要求のログを確認し、Web サイトの予想される通常のトラフィックのコンテキスト内で、それらの要求が適切にブロックされているかどうかを評価してください。
