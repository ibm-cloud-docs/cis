---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-29"

keywords: IBM Cloud Internet Services, IBM CIS application, Authoritative DNS servers

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# IBM Cloud Internet Services (CIS) 入門
{:#getting-started}

IBM Cloud Internet Services (CIS) は、Cloudflare を採用しており、お客様のワークフローを強化するために、[セキュリティー](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-for-optimal-security)、[信頼性](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability)、[パフォーマンス](/docs/infrastructure/cis?topic=cis-manage-your-cis-deployment-for-best-performance)という 3 つの主要な機能を提供します。IBM CIS アプリケーションを開くと、画面左側のナビゲーション・バーに各機能の領域が表示されます。

どの機能についても、IBM CIS では、お客様固有のニーズに合わせて個々のフィーチャーをチューニングできます。フィーチャーの例を次に示します。

 * 権威 DNS サーバー
 * グローバルおよびローカルのロード・バランシング
 * Web アプリケーション・ファイアウォール (WAF)
 * DDoS 防御
 * キャッシュ・ルールとページ・ルール


## 始める前に
{:#before-you-begin}

IBM CIS を使用するには、まず [IBMid](https://www.ibm.com/account/reg/us-en/signup?formid=urx-19776) が必要です。 次に、好みに応じて IBM Cloud アカウントまたは新しい [IBM Cloud Internet Services ポータル](https://{DomainName}/catalog/services/internet-services)を使用して、サービスを注文できます。

IBM Cloud Internet Services を使用するためのアカウントの取得方法がわからない場合は、利用を開始するための詳細な手順を、[IBM 営業担当員にお問い合わせください](https://{DomainName}/cloud/support)。

既存の Softlayer アカウントがある場合は、IBMid に[そのアカウントをリンク](https://{DomainName}/docs/account?topic=account-unifyingaccounts)できます。 

## プロセスの概要
{:#process-overview}

ほんのいくつかの手順を実行するだけで、インターネット・トラフィックに IBM CIS を使用できるようになります。

 * IBM Cloud ダッシュボードから IBM CIS アプリケーションを開きます。
 * 管理するドメインを追加します。
 * IBM 提供のネーム・サーバーをお客様の DNS 情報に構成します。
 * チュートリアルに従って、または他の機能をセットアップして、IBM CIS の使用準備を進めます。

### 手順 1: IBM CIS アプリケーションを開きます。
{:#open-cis-application}

[IBM Cloud ダッシュボード](https://{DomainName}/catalog/)を開きます。 次に、ダッシュボードの左側のナビゲーション・バーで**「インフラストラクチャー」->「ネットワーク」**カテゴリーを選択して、IBM CIS アプリケーション・アイコンに移動します。 画面のほぼ中央に表示されるアイコンをクリックして、IBM Cloud Internet Services アプリケーションを開きます。 

![カタログ](images/catalog-cis-tile.png)

**「概要」画面**

IBM CIS アプリケーションが起動すると、IBM CIS の**「概要」**画面が表示されます。UI 表示の左の領域には**「セキュリティー」**、**「信頼性」**、**「パフォーマンス」**タブがあります。

**どのプランを選択すればよいか?**

以下の 4 つのプランから選択できます。 
* **エンタープライズ使用量** 
* **エンタープライズ・パッケージ** 
* **標準プラン** 
* **無料トライアル** 

**無料トライアル**は 30 日後に期限切れになります。この時点で、**標準プラン**か**エンタープライズ・プラン**にアップグレードできます。1 つの**標準**インスタンスで 1 つのドメインを管理できます。1 つのアカウント内にご希望の数だけ**標準**サービス・インスタンスを作成でき、それぞれが 1 つのドメインを管理します。 

**エンタープライズ・プラン**を使用すると、1 つのサービス・インスタンス内で複数のドメインを管理できます。**「概要」**画面で**「作成」**ボタンを選択して、アカウントのプロビジョニングを開始します。

**無料トライアル**は 1 アカウントにつき 1 インスタンスに制限されています。
{:note}

**プロビジョニングの開始**

IBM CIS アプリケーションの最初の画面が表示されます。ここで**「ドメインの追加 (Add Domain)」**ボタンを選択して開始します。


### 手順 2. ドメインを追加して構成します。
{:#add-configure-your-domain}

ウェルカム・ページから**「始める」**を選択して、CIS のセットアップを開始します。

![入門](images/overview-setup-step1.png)

次に、Web サービスを保護してパフォーマンスを向上させるために、まず、ドメインまたはサブドメインを入力します。

DNS ゾーンを指定してください。 これらのドメインまたはサブドメインのネームサーバーは、ドメインのレジストラーまたは DNS プロバイダーで構成できます。 CNAME は使用しないでください。
{:note}

![入門](images/overview-setup-step2.png)

「概要」画面に、ドメインの状態が`「保留中」`と表示されます。 手順 4 を完了するまで、ドメインは`「保留中」`のままです。

ドメインが追加されたら、IBM CIS インスタンスは削除できなくなります。 インスタンスを削除するには、まずインスタンスからドメインを削除してください。
{:note}

### ステップ 3. DNS レコードをセットアップします (オプション)。
{:#setup-your-dns-records}

ドメインのトラフィックを CIS に移行する前に、CIS 内に DNS レコードをインポートまたは再作成しておくことを強く推奨します。このステップはスキップするように選択できますが、お使いの DNS レコードが CIS 内で適切に構成されない場合、Web サイトの一部がアクセス不能になる可能性があります。

現在の DNS からエクスポートしたレコードをアップロードすることによってインポートするか、DNS レコードを手動で作成します。レコードをインポートするには、**「レコードのインポート」**を選択します。

![入門](images/overview-setup-step3.png)

終了した場合や、このステップをスキップする場合は、**「次のステップ」**を選択します。

### 手順 4. レジストラーまたは既存の DNS プロバイダーにネーム・サーバーを構成します。
{:#configure-your-name-servers-with-the-registrar-or-existing-dns-provider}

IBM CIS の利点を活用するには、リストされたネーム・サーバーを使用するように、レジストラーまたはドメイン・ネーム・プロバイダーを構成します。 ドメイン (例: `example.com`) を委任する場合は、リストされたネーム・サーバーを、レジストラー管理のドメイン設定 (レジストラーの Web ポータルなど) に構成します。 ドメインのレジストラーが不明な場合は、https://whois.icann.org/ で検索できます。 サブドメイン (例: `subdomain.example.com`) を別の DNS プロバイダーから委任する場合は、リストされた各ネーム・サーバーのネーム・サーバー (NS) レコードを追加する必要があります。 プロバイダーによる詳細な指示については、Cloudflare のパートナーが執筆した [Managing DNS Records ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://support.cloudflare.com/hc/en-us/articles/360019093151-Managing-DNS-records-in-Cloudflare){:new_window} を参照してください。

お客様がレジストラーまたは DNS プロバイダーを構成してから、その変更が反映されるまでに最大で 24 時間かかる可能性があります。 指定のネームサーバーがドメインまたはサブドメインに対して正しく構成されたことを IBM が確認すると、ドメインのステータスが`「保留中」`から`「アクティブ」`に変わります。 ネームサーバーを構成した後に、`「概要」`ページの「ネーム・サーバーの再チェック (Recheck name servers)」リンクをクリックすると、ドメインのアクティブ化が早まる可能性があります (このチェックは 1 時間に一度だけ実行できます)。

60 日以内にドメインを`「アクティブ」`状態に移行しなければなりません。移行しないと、ドメインと構成データは削除されます。
{:note}

![入門](images/overview-setup-step4.png)

### 手順 5. IBM Cloud Internet Services がアプリケーション、ホスト名、または Web サイトのドメイン情報を解決することを確認します。
{:#ensure-cis-is-resolving-domain-info}

始めに、左側のナビゲーション・バーから**「信頼性」**タブを選択し、**「DNS」**オプションを選択します。 必ず、適切な _DNS レコード_ を追加してください。 自動入力される **A レコード**および任意の **AAAA** または **MX** エントリーを追加します。 レジストラーの委任が完了する前にこれらのレコードを追加しておかないと、IBM Cloud Internet Services は、インターネットに公開されているアプリケーションのドメイン情報を解決できません。

![入門](images/dns-records.png)

### 手順 6. この間に、IBM CIS の他の機能やフィーチャーの管理を開始できます。
{:#manage-other-cis-functions}

他の機能やフィーチャーの管理について詳しくは、[段階的な手順](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cloud-internet-services-cis-deployment)を参照してください。
