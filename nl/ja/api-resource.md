---

copyright:
  years: 2018
lastupdated: "2018-03-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# API 仕様

CIS API 仕様を表示する方法を以下に示します。 

1. CIS API を表示するには、[CIS API 仕様](https://console.bluemix.net/apidocs/2640-cloud-internet-services)のページにナビゲートします。 

2. 左側のナビゲーション・メニューで、使用可能な API のリストの中から選択します。


## 注

1. API エンドポイント: https://api.cis.cloud.ibm.com

2. API 呼び出しごとに **X-Auth-User-Token** ヘッダーが必要です。これは、(例えば「bx iam oauth-tokens」コマンドを使用して) IAM から取得できる、ユーザーのベアラー・トークンです。

3. また、API 呼び出しごとに、パスの中に **crn** フィールドが必要です。これは、構成される CIS リソース・インスタンスの完全なクラウド・リソース名 (CRN) です (例えば、リソース・インスタンスの CRN は、コマンド「bx resource service-instance <instance-name>」を使用してその名前から取得できます)。CRN は、API 呼び出しの中では URL エンコードされていなければなりません。

4. API 呼び出しの速度は制限されています。1 分間に合計 100 の API 呼び出しを行えます。この速度を超えると、後続の呼び出しは一定時間ブロックされます。
