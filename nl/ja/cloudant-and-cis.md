---

copyright:
  years: 2019
lastupdated: "2019-03-28"

keywords: Cloudant database, CORS, cross-origin resource sharing, host header

subcollection: cis

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"} 
{:note: .note}


# IBM Cloud Internet Services 経由の Cloudant データベースへのアクセス
{: #access-cloudant-through-cis}

以下のステップを実行して、IBM Cloud Internet Services (CIS) 経由で Cloudant データベースにアクセスします。

## 始める前に
{: #access-cloudant-through-cis-begin}

以下の指示は、[入門](/docs/infrastructure/cis?topic=cis-getting-started-with-ibm-cloud-internet-services-cis-)ページで略述されているとおりに、CIS にドメインを既に追加していることを前提にしています。

### ステップ 1: CIS ドメインをクロス・オリジン・リソース共有 (CORS) に追加する
{: #access-cloudant-through-cis-step1}

* Cloudant データベースにナビゲートし、`「アカウント」`->`「CORS」`ページを開きます。
* CIS ドメインを起点ドメインの入力フィールドに追加します。例えば、`https://cloudant.test.foo.com` です。

### ステップ 2. Cloudant データベースを指すように CIS を構成する
{: #access-cloudant-through-cis-step2}

* CIS ダッシュボードにナビゲートし、Cloudant データベースのホスト名を指すロード・バランサーまたは DNS レコードを作成します。例えば、`https://cloudant.test.foo.com` -> `111-222-333-444-555-test.cloudant.com` のようにします。
* DNS レコードまたはロード・バランサーについて`プロキシー`を有効にします。


### Step 3. ページ・ルールを作成してホスト・ヘッダーのオーバーライドを設定する
{: #access-cloudant-through-cis-step3}

* CIS ダッシュボードで、`「パフォーマンス」`->`「ページ・ルール」`にナビゲートします。
* ご希望の URL に関するページ・ルールを作成します。例えば、`https://cloudant.test.foo.com/*` のようにします。
* 「ルールの振る舞い」の`「ホスト・ヘッダーのオーバーライド」`設定を選択します。
* Cloudant データベースのホスト名として設定します。例えば、`111-222-333-444-555-test.cloudant.com` のようにします。

Cloudant について詳しくは、[Cloudant の資料](/docs/services/Cloudant?topic=cloudant-getting-started-with-cloudant)を参照してください。
