---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: API Specs, CIS APIs

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# API 仕様
{:#api-specs}

CIS API 仕様を表示する方法を以下に示します。 

1. CIS API を表示するには、[「API Docs」](/apidocs/)のページにナビゲートします。 

2. 左側のナビゲーション・メニューで、「ネットワーキング」ボックスにチェック・マークを付けて、API をフィルタリングします。

3. 入手可能な Cloud Internet Services の API のリストから選択します。


## 注
{:#api-notes}

1. API エンドポイント: `https://api.cis.cloud.ibm.com`.

2. API 呼び出しごとに **X-Auth-User-Token** ヘッダーが必要です。 このヘッダーは、(例えば `ibmcloud iam oauth-tokens` コマンドを使用して) IAM から取得できる、ユーザーのベアラー・トークンです。

3. また、API 呼び出しごとに、パスの中に **crn** フィールドが必要です。 このフィールドには、構成される CIS リソース・インスタンスの完全なクラウド・リソース名 (CRN) が含まれています。(例えば、リソース・インスタンスの CRN は、コマンド `ibmcloud resource service-instance <instance-name>` を使用してその名前から取得できます)。CRN は、API 呼び出しの中では URL エンコードされていなければなりません。

4. API 呼び出しの速度は制限されています。 1 分間に合計 100 の API 呼び出しを行えます。 この速度を超えると、後続の呼び出しは一定時間ブロックされます。
