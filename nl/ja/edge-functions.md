---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: edge functions beta, edge functions

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# エッジ機能 (ベータ版)
{: #edge-functions}

CIS エッジ機能を使用すると、サーバーレス実行環境を利用して、インフラストラクチャーを構成したり保守したりせずに新しいアプリケーションを作成したり既存のアプリケーションを変更したりできます。エッジ機能を定義してクラウドのエッジにアップロードし、要求が起点に達する前に処理することができます。CIS エッジ機能を使用して、HTTP 要求と応答を変更したり、並行要求を行ったり、クラウドのエッジから応答を生成したりできます。

## エッジ機能の働き方
{: #how-edge-functions-work}

エッジ機能は**アクション**を URI と、定義済みのドメインに基づいて関連付けます。この関連付けは**トリガー**と呼ばれます。自分のサイトへの着信要求は、クラウドのエッジでインターセプトされ、自分のアカウントまたはドメイン内のトリガーと突き合わされます。要求の URL がトリガーの URI と一致している場合は、そのトリガーに関連付けられているアクションが実行されます。

エッジ機能は、最新の Web ブラウザーで使用できる [Service Worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) 上でモデル化され、可能な限り同じ API を使用します。

Service Worker API を使用すると、自分のサイトに対する要求をインターセプトできます。JavaScript での要求の処理が始まると、自分のサイトか他者のサイトに任意の数の二次要求を行い、最終的にご希望の応答を訪問者に戻すように選択することもできます。

エッジ機能は、標準的な Service Worker とは違って、ユーザーのブラウザーではなく CIS エッジ・サーバー上で稼働します。したがって、悪意のあるクライアントが迂回できないトラステッド環境でコードが実行されることを信頼できます。また、ユーザーが Service Worker をサポートしている最新のブラウザーを使用している必要もなくなります。全くブラウザーではない API クライアントから要求をインターセプトすることもできます。

内部的に、エッジ機能は Google Chrome ブラウザーでも使用されている V8 JavaScript エンジンを使用して、弊社のインフラストラクチャー上のワーカーを実行します。V8 は JavaScript コードを超高速のマシン・コードに動的にコンパイルするので、パフォーマンスが非常に高くなります。コードをマイクロ秒単位で実行できるようになり、弊社のエッジで 1 秒あたり数千のスクリプトを実行できるようになります。

エッジ機能は V8 を使用する一方で、Node.js は使用しません。ワーカー内で使用可能な JavaScript API が直接実装されています。直接 V8 と連動すると、コードの実行効率が上がり、顧客とインフラストラクチャーを安全に保つのに必要なセキュリティー管理が備えられます。


## アクション
{: #edge-functions-actions}

アクションは JavaScript で書かれ、イベント・リスナーがトリガー・イベントに応答する必要があります。アクションは、トリガーで使用されなければトラフィックに影響しません。

### エンタープライズ・プランと標準プランの比較
{: #edge-functions-enterprise-v-standard-plans}

標準プランには最大で 1 つのアクションがあります。ドメインと同じ名前がアクションに割り当てられます。別のファイルをアップロードしてアクションを置換したり、コード・エディターを使用してアクションを更新したりすることもできます。別のファイルをアップロードすると、既存のアクションが削除されます。

エンタープライズ・プランは、無制限の数のスクリプトをアップロードできます。固有の名前を付けることができます。

### アクションの作成
{: #edge-functions-create-actions}

コード・エディターを使用してアクションを追加するには、**「作成」**を選択します。エンタープライズ・プランでは、アクションの名前を入力します。標準プランでは、名前は編集できず、ドメインの名前に設定されます。Javascript コードの追加後に、**「保存」**を選択してアクションを作成します。

### アクションのアップロード
{: #edge-functions-upload-actions}

JavaScript ファイルをアップロードするには、**「アップロード」**ボタンを使用します。エンタープライズ・プランでは、アクションの名前はファイルの名前です。標準プランでは、アクション名はドメインの名前に設定されます。

既存のアクションと同じ名前のアクションをアップロードしたり作成したりすると、既存のアクションは上書きされます。この動作が発生しないようにするには、アップロードの前にアクション・ファイルの名前を変更するか、作成中にテキスト入力で固有の名前を入力してください。
{:note}

### アクションの編集
{: #edge-functions-edit-actions}

アクションを選択すると、エディター内でそのアクションが開かれ、変更できるようになります。変更を保存するたびに、アクションがクラウドのエッジにアップロードされます。更新後に、**「保存」**を選択します。アクションが使用中の場合、変更は即時に有効になります。 

### アクションの削除
{: #edge-functions-delete-actions}

アクションを削除するには、**「アクション」**テーブル内の**「削除」**アイコンをクリックします。使用中のアクションを削除することはできません。アクションを削除するには、最初にトリガーから削除します。**「使用 (Uses)」**列に、このアクションと関連付けられているトリガーの数が表示されます。削除すると、元に戻すことはできません。


### トリガーの関連付け
{: #edge-functions-associated-triggers}

トリガーを追加して、アクションと関連付けます。

### エッジ機能の既知の制限
{: #edge-functions-known-limitations}

既存のアクションと同じ名前のアクションをアップロードするとします。既存のアクションは上書きされます。この動作が発生しないようにするには、アップロードの前にアクション・ファイルの名前を変更してください。


## トリガー
{: #triggers}

### トリガーについて
{: #about-triggers}

トリガー (ルート) は、アクションにルーティングするドメイン・トラフィックを判別します。トリガーは特定の URL パターンを、アカウント上のドメインに基づいて、事前定義済みのアクションに関連付けます。URL にはドメインが含まれていなければなりませんが、ワイルドカードをドメインに対する接頭部として含めたりパスの末尾に含めたりできます。パターン上にパスが指定されていないと、暗黙的に `/` が追加されます。URL パターンに中置のワイルドカードや照会パラメーターを含めることはできません。

トリガーを追加するには、ドメインを追加しなければなりません。アクションが関連付けられていないトリガーを追加することもできます。

### トリガーの追加
{: #add-triggers}

**「トリガー」**タブに移動し、**「トリガーの追加」**をクリックします。URL パターンを入力し、既存のアクションのリストからアクションを選択します。 

アクションの場合、**「エッジ機能の回避 (Avoid Edge Functions)」**を選択することもできます。 選択すると、トリガーのパスはアクティブな状態のままですが、エッジ機能のアクションを使用することは避けます。例えば、`my-function` と呼ばれるアクションと、パスが `beta.cistest-load.com/*` のトリガーがあるとします。パス `beta.cistest-load.com/data` がアクション `my-function` を使用しないようにする必要がある場合は、パスが `beta.cistest-load.com/data` でオプションが **「エッジ機能の回避 (Avoid Edge Functions)」**の別のトリガーを作成します。こうすると、パス `beta.cistest-load.com/data` はアクティブな状態のままで、アクション `my-function` を使用しなくなります。

### トリガーの編集
{: #edit-triggers}

トリガーを更新するには、選択したトリガーに関するテーブル行内のメニュー・オプションを使用します。更新後に、**「保存」**を選択します。

### トリガーの削除
{: #delete-triggers}

トリガーを削除するには、選択したトリガーに関するテーブル行内のメニュー・オプションを使用します。このアクションを元に戻すことはできません。


## ユース・ケース
{: #edge-functions-use-cases-examples}

以下の例はデモンストレーション専用で、実動での使用は想定していません。
{:important}
* [A/B テスト](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#ab-testing)
* [応答ヘッダーの追加](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#add-response-header)
* [複数の要求の集約](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#aggregate-multiple-requests)
* [条件付きルーティング](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#conditional-routing)
* [ホット・リンクの保護](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#hot-link-protection)
* [起点のない応答](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#originless-responses)
* [Post 要求](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#post-requests)
* [Cookie の設定](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#setting-cookies)
* [署名済み要求](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#signed-requests)
* [応答のストリーミング](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#streaming-responses)
