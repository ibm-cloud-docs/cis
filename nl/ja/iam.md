---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Access Group Writer role, CIS instance, IAM

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# IAM と CIS
{:#iam-and-cis}

IBM Cloud Internet Services (CIS) は IAM を利用して許可と認証を行います。

自分の CIS インスタンスにだれも追加しない場合は、このページを無視できます。
{:note}

ナビゲーション・ツリーに基づいて、以下の 3 つの CIS Functional Scope によりアクセスを制限します。 
* 信頼性 - DNS、GLB など
* セキュリティー - 証明書、IP ファイアウォール・ルール、速度制限など
* パフォーマンス - ページ・ルール、キャッシング、ルーティングなど

このセクションでは、インスタンスのアクセス制御を詳細に調整する方法を解説します。

## 役割
{:#iam-and-cis-roles}

以下の 3 つの役割を使用して IAM を利用します
* リーダー - インスタンスとドメインに関する情報を取得できます
* ライター - 既存の構成を変更できます
* 管理者 - インスタンス、ドメイン、構成を作成または削除できます

## アクセス・グループおよびユーザー
{:#iam-and-cis-access-groups-users}

ポリシーは、ユーザーに直接割り当てることも、アクセス・グループに割り当てることもできます。
作成されるポリシーの数を最小にし、それらのポリシーを管理する負荷を軽減するために、ポリシーをアクセス・グループに割り当てることをお勧めします。

## キャッシュ
{:#iam-and-cis-cache}

許可の結果をキャッシュに入れ、同じ要求を再び受け取るときには、そのキャッシュを使用して決定を行います。キャッシュの存続時間 (10 分) が経過すると、それは期限切れになります。

## ベスト・プラクティス
{:#iam-and-cis-best-practices}

1. ポリシーを変更する代わりに、既存のポリシーを削除してから新しく作成します。

## シナリオ
{:#iam-and-cis-scenarios}

このセクションでは、CIS によって作成されたアクセス・ポリシーのさまざまな例について説明します。 

### `config` タイプのドメイン・レベル
{:#iam-and-cis-scenarios-domain-level}

#### アクセス・グループから `security config` を使用する単一ドメインへのアクセス
##### ライター役割

Bob は CIS インスタンス `cis-test-instance`、および 2 つのドメイン `bob.com` と `bob-ibm.com` を所有しています。
Bob は、社内のすべてのセキュリティー・エンジニア (sec-group) が、**`bob.com`** の**セキュリティー構成**のみに対するライター役割にアクセスできるようにします。

以下の手順は、IAM ポリシーを作成してこのシナリオを可能にする方法を示しています。

Bob は cis-test-instance にログインした後に、以下の操作を行います。
1. ナビゲーション・バーの**「アカウント」>「アクセス」**タブをクリックします
1. アクセス権限を付与する**「アクセス・グループ」**-**「sec-group」**を選択します
1. **`bob.com`** を選択します
1. **「ライター」**役割を選択します
1. **「セキュリティー構成」**オプションを選択します
1. **「ポリシーの作成」**をクリックします

管理タブで: 以下のポリシーが **sec-group** のために作成されます。

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e

Service Instance 
    name: cis-test-instance  
    id: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9 
Domain 
    name: bob.com
    id: 4b23ec772965f672f96f05670e36827e 
Config Type
    cfgType: security
```

これで、sec-group は `bob.com` だけを参照するアクセス権限を持ち、セキュリティーに関連する値を変更できるようになりました。 

##### アクセス・グループの役割をライターから管理者へ更新する

Bob が sec-group の役割をライターから管理者に更新するためには、既存のポリシーを削除する必要があります。 
1. **「IAM の管理 (Manage IAM)」タブ >「アクセス・グループ」>「sec-group」>「アクセス・ポリシー」**に移動します
1. 以下のポリシーを削除します 
  ```
  Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
  ```

次に、Bob は以下の新しいポリシーを作成する必要があります。 
1. ナビゲーション・バーの**「アカウント」>「アクセス」**タブをクリックします
1. アクセス権限を付与する**「アクセス・グループ」**-**「sec-group」**を選択します
1. **`bob.com`** を選択します
1. **「管理者」**役割を選択します
1. **「セキュリティー構成」**オプションを選択します
1. **「ポリシーの作成」**をクリックします

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

既存のポリシー (ライター) が削除されていない場合は、管理者のポリシーを作成しようとすると失敗します。

##### セキュリティーと共にパフォーマンスも含むように構成を更新する

Bob が管理者 sec-group に、セキュリティーと共に `bob.com` でのパフォーマンス構成に対するアクセス権限を付与するためには、次のようにします。
1. ナビゲーション・バーの**「アカウント」>「アクセス」**タブをクリックします
1. アクセス権限を付与する**「アクセス・グループ」**-**「sec-group」**を選択します
1. **`bob.com`** を選択します
1. **「管理者」**役割を選択します
1. **「パフォーマンス構成 (Performance config)」**オプションを選択します
1. **「ポリシーの作成」**をクリックします

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: performance, domainId: 4b23ec772965f672f96f05670e36827e

```

#### `security config` を使用するすべてのドメインへのアクセス

以前の例の `bob.com` および `bob-ibm.com` にセキュリティー・アクションを提供するには、ドメインごとに手順を繰り返して、新しいポリシーを作成する必要があります。唯一の異なる点は、ポリシーごとに対応するドメインを選択することです。

1. ナビゲーション・バーの**「アカウント」>「アクセス」**タブをクリックします
1. アクセス権限を付与する**「アクセス・グループ」**-**「sec-group」**を選択します
1. **`bob.com`** を選択します
1. **「管理者」**役割を選択します
1. **「セキュリティー構成」**オプションを選択します
1. **「ポリシーの作成」**をクリックします

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

1. ナビゲーション・バーの**「アカウント」>「アクセス」**タブをクリックします
1. アクセス権限を付与する**「アクセス・グループ」**-**「sec-group」**を選択します
1. **`bob-ibm.com`** を選択します
1. **「管理者」**役割を選択します
1. **「セキュリティー構成」**オプションを選択します
1. **「ポリシーの作成」**をクリックします

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 7ad7341865246f5df482ad9f76aafb5a
```



#### `security config` および `reliability config` を使用する単一ドメインへのアクセス

Bob は CIS インスタンス cis-test-instance、および 2 つのドメイン `bob.com` と `bob-ibm.com` を所有しています。
Bob は Tony に、**`bob-ibm.com`** の**セキュリティーと信頼性アクション**のみに対するライター役割へのアクセス権限を付与しようとしています。

Bob は cis-test-instance にログインした後に、以下の操作を行います。
1. ナビゲーション・バーの**「アカウント」>「アクセス」**タブをクリックします
1. アクセス権限を付与する相手として **Tony** を選択します
1. **`bob-ibm.com`** を選択します
1. **「ライター」**役割を選択します
1. **「セキュリティーと信頼性 (Security and reliability)」**オプションのチェック・ボックスを選択します 
1. **「ポリシーの作成」**をクリックします

これにより、各構成タイプのバックエンドに 2 つのポリシーが作成されます。

### すべての config タイプのドメイン・レベル
{:#iam-and-cis-scenarios-domain-level-all-config-types}

Bob は Tony にドメイン・レベルでの読み取り/書き込み/管理の権限を付与しようとしています。

#### 書き込み
Bob は cis-test-instance にログインした後に、以下の操作を行います。
1. ナビゲーション・バーの**「アカウント」>「アクセス」**タブをクリックします
1. アクセス権限を付与する相手として **Tony** を選択します
1. **`bob.com`** を選択します
1. **「ライター」**役割を選択します
1. CIS Functional Scope に対するすべてのボックスにチェック・マークを入れます
1. **「ポリシーの作成」**をクリックします

```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### 管理者
Bob は cis-test-instance にログインした後に、以下の操作を行います。
1. ナビゲーション・バーの**「アカウント」>「アクセス」**タブをクリックします
1. アクセス権限を付与する相手として **Tony** を選択します
1. **`bob.com`** を選択します
1. **「管理者」**役割を選択します
1. CIS Functional Scope に対するすべてのボックスにチェック・マークを入れます
1. **「ポリシーの作成」**をクリックします

```
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### リーダー
Bob は cis-test-instance にログインした後に、以下の操作を行います。
1. ナビゲーション・バーの**「アカウント」>「アクセス」**タブをクリックします
1. アクセス権限を付与する相手として **Tony** を選択します
1. **`bob.com`** を選択します
1. **「リーダー」**役割を選択します
  1. すべてのチェック・ボックスにはあらかじめチェック・マークが入っていて、ユーザーにはドメイン全体に対する *min* 読み取りアクセス権限が必要であり、ドメインに対する部分的なアクセス権限を付与できないことを示しています。
1. **「ポリシーの作成」**をクリックします


```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

### インスタンス・レベル - すべてのドメイン
{:#iam-and-cis-scenarios-instance-level}

このポリシーは、IAM 管理ページによって作成および管理する必要があります。

インスタンス・レベルのアクセス権限を使用すると、Bob は Tony に、存在する 10 のインスタンスのうちの 1 つに対する許可を与えることができます。
Tony はそのインスタンス内のすべてのドメインを参照できます。 

Bob がライターまたは管理者に、以下に対するアクセスを許可する場合、インスタンス・レベルのアクセス権限を付与する必要があります。
* ロード・バランサー - プールおよびヘルス・チェック
* ファイアウォール・アクセス・ルール
* ワーカー 

「IAM の管理 (Manage IAM)」ページで、サービス・インスタンス cis-test-instance に対するライター/管理者のポリシーを作成します。

```
Manager	Resource	Only service instance cis-test-instance of CIS 	
または
Writer	Resource	Only service instance cis-test-instance of CIS 	
```

## IAM の管理のポリシー 
{:#manage-iam-policies}

CIS では、ユーザーが IAM ポリシーを作成できますが、管理は [IAM ページ] によって行う必要があります。(
https://{DomainName}/iam#/overview).

## 注記
{:#iam-note}
CIS インスタンスの「アクセス」ページで作成されるポリシーごとに、2 つまたは 3 つのポリシーが順次作成されます。

1. サービス・インスタンスの「プラットフォーム」ビューアー役割により、追加されたユーザーはダッシュボード上のインスタンスを表示できます。

**例**
```
Viewer	Resource	Only service instance cis-instance-instance of CIS 	
```

2. ドメイン・レベルの読み取りアクセス権限は、詳細に調整されたアクセスが機能するための最低要件です。

**例**
```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
```
3. 提示されている構成タイプで作成したポリシー。

**例**
```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

**よくある質問**
1. サービス・インスタンス ID はどのようにして取得できますか?

   概要ページにある CRN をコピーします
   ```
   crn:v1:test:public:internet-svcs:global:a/2c38d9a9913332006a27665dab3d26e8:836f33a5-d3e1-4bc6-876a-982a8668b1bb::
   ```
   CRN の末尾部分がサービス・インスタンスです: `836f33a5-d3e1-4bc6-876a-982a8668b1bb`。
   
   または
   
   リソース・リストのメインページで CIS インスタンスを含む行をクリックして、サービス・インスタンス ID の GUID をコピーします。

2. ポリシーを削除しましたが、ポリシーを付与したユーザーは、まだそのアクションを実行できています。

   CIS は許可結果をキャッシュに入れます。そのキャッシュの TTL は 10 分です。  
   
   IAM が許可を与えるときは、決定を行う前に、アクセス・グループからのアクセス・ポリシーと、ユーザー独自のポリシーを使用します。

3. インターネット・サービスをプロビジョンするにはどの許可が必要ですか?

   リソースを作成してそれをリソース・グループに追加できない場合、大抵は、アクセス権限の問題が発生しています。リソース・グループ自体に対して少なくともビューアー役割を持っている必要があり、また、アカウント内のサービスに対して少なくともエディター役割を持っている必要があります。アカウント管理者に連絡して、アカウント内で割り当てられているアクセス権限を確認してください。詳しくは、[リソースに対するアクセス権限の管理](/docs/iam?topic=iam-iammanidaccser)を参照してください。
   
 
