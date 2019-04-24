---

copyright:
  years: 2019
lastupdated: "2019-03-28"

keywords: resolve override, Cloud Object Storage, bucket resource

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# COS を使用してオーバーライドを解決
{: #resolve-override-cos}

## ユース・ケース
{: #cos-use-cases}

ページ・ルールをマッチングする要求が Cloud Object Storage (COS) バケット・リソースに解決されるようにします。


## 前提条件
{: #cos-prerequisites}

次の手順は、既存の COS インスタンスと、パブリック・アクセスを持つバケットがあることを想定しています。パブリック・アクセスについては、[パブリック・アクセスの許可](/docs/services/cloud-object-storage/iam?topic=cloud-object-storage-allowing-public-access)を参照してください。


## ページ・ルールの作成の手順
{: #cos-create-page-rule}

* **「パフォーマンス」->「ページ・ルール」**に移動します。
* **「ルールの作成」**ボタンをクリックします。
* URL マッチングに使用する値を入力します。例えば、`*.foo.com/*` と入力します。
  * URL マッチングは、COS オブジェクト名と一致する必要があることにご注意ください。
  * 例えば、バケット `my-bucket1` の下に reports.txt というオブジェクトがある場合、次のいずれの URL マッチングも有効です。
    * `*.foo.com/*`
    * `*.foo.com/reports.txt`
* ドロップダウンを使用して、**「パフォーマンス」**の下の**「COS を使用してオーバーライドを解決」**を選択します。
* **「クラウド・オブジェクト・ストレージ・インスタンス (Cloud Object Storage Instance)」**ドロップダウンを使用して、希望するインスタンスを選択します。
* **「バケット」**ドロップダウンを使用して、希望するバケットを選択します。
* ページ・ルールを作成するには、**「1 件のリソースのプロビジョン」**ボタンをクリックします。


## コンセプトの詳細な説明
{: #cos-detail-concepts}

**「COS を使用してオーバーライドを解決」**ページ・ルールを作成する際、CIS は自動的に COS 統合に必要な他のリソースを作成します。次のようなものがあります。

**CNAME**
* `<bucket-name>.<cos-endpoint>` の CNAME DNS レコードを `<bucket-name>` として作成します。
* 例えば、CIS ドメインが `foo.com` の場合、COS バケットの名前は `images` で、パブリック COS エンドポイントは `s3.us-west.objectstorage.uat.test.net` です。そこで CIS は CNAME を `images.foo.com` として作成し、それは `images.s3.us-west.objectstorage.uat.test.net` を指します。
「COS を使用してオーバーライドを解決」ページ・ルールが不要になった場合、CNAME はページ・ルールと一緒に手動で削除する必要があります。
{:note}

**ホスト・ヘッダーのオーバーライド**
* ホスト・ヘッダーのオーバーライドの設定は、ページ・ルールに一致する URI のホスト・ヘッダーを `<bucket-name>.<cos-endpoint>` に置き換えます。
* 前の例を使用した場合、ホスト・ヘッダーのオーバーライドの値は `images.s3.us-west.objectstorage.uat.test.net` に設定されます。


## ページ・ルールの削除
{: #cos-delete-page-rule}

「COS を使用してオーバーライドを解決」ページ・ルールが不要になった場合、CNAME はページ・ルールと一緒に_手動で_削除する必要があります。



## ページ・ルールの編集
{: #cos-edit-page-rule}

ページ・ルールを編集した後は、**「COS を使用してオーバーライドを解決」**はページ上に表示されなくなります。ただし、**「オーバーライドの解決」** `<bucket>.<domain>` および **「ホスト・ヘッダーのオーバーライド」** `<bucket>.<cos-endpoint>` によって、**「COS を使用してオーバーライドを解決」**が置き換えられます。

**「オーバーライドの解決」**を変更しても、新しい CNAME レコード (例えば `<updated-bucket>.<domain>`) は作成_されません_。これは、**「COS を使用してオーバーライドを解決」**を使用して初めてページ・ルールを作成するときにだけ行われます。バケットの CNAME レコードが自動で作成されるようにするには、[ページ・ルールの作成](#cos-create-page-rule)の手順に従ってください。
