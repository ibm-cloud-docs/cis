---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIS origin certificates, ordering cis origin certificate 

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:note: .note}

# 起点証明書
{:#cis-origin-certificates}

起点証明書は CIS によって発行される無料の TLS 証明書で、起点サーバーからユーザーまでのトラフィックを暗号化します。 無料の TLS 証明書を注文して起点サーバーにインストールしてください。

CIS 起点証明書は、CIS で使用する場合にのみ有効です。
{:note}

## 起点証明書の注文
{:#cis-origin-certificates-ordering}

起点証明書を注文するには、証明書署名要求 (CSR) を入力するか、鍵と CSR を生成するための CIS の秘密鍵のタイプを選択します。

証明書の保護対象の起点にあるホスト名 (ワイルドカードを含む) を最大 100 件指定します。ワイルドカードは、適用範囲の 1 つのレベルのみを表します。より広い適用範囲を表すようにするには、同じ証明書で複数のワイルドカードを使用します (例えば `*.yourdomain.com` と `*.yoursubdomain.yourdomain.com` など)。CIS 起点証明書には、IP アドレスは指定できません。

有効期限を指定します。証明書のデフォルトの有効期限は 15 年です。最短の有効期限は 7 日です。

証明書を注文してすぐに秘密鍵が使用できるようになるのは、秘密鍵および CSR が CIS によって生成された場合のみです。

## サーバーへの起点証明書のインストール
{:#cis-origin-certificates-installing}

### Apache httpd
{:#cis-origin-certificates-installing-apache-httpd}
1. 起点証明書を注文します。
1. 秘密鍵と起点証明書を、鍵と証明書のファイルを保管するサーバー上のディレクトリーにある個別のファイルに、PEM 形式でコピーします。
1. Apache 構成ファイルを見つけます。通常、ファイル名は `httpd.conf` または `apache2.conf` で、場所は `/etc/httpd/` または `/etc/apache2/` です。ただしこれは、構成ファイルによって異なります (特にサーバーの管理に特別なインターフェースを使用している場合など)。デフォルトのインストール配置の完全なリストについては、Apache の [DistrosDefaultLayout](https://wiki.apache.org/httpd/DistrosDefaultLayout) を参照してください。以下のコマンドは、Linux 上で SSL 構成ファイルを見つける方法の 1 つです。
    ```
    grep -i -r "SSLCertificateFile" /etc/httpd/
    ```
1. 構成する <VirtualHost> ブロックを見つけます。オプションで、使用しているサイトの既存の非セキュアな仮想ホストが HTTP および HTTPS から使用できるようにコピーします。接続の各タイプには仮想ホストが必要なためです。
1. SSL 用に <VirtualHost> ブロックを構成します。以下の例は、シンプルな SSL の構成を表しています。ご使用の証明書と秘密鍵のファイル名を使用してください。`SSLCertificateFile` は、OriginCA 証明書のファイル名で、`SSLCertificateKeyFile` は OriginCA 秘密鍵のファイル名です。
    ```
    <VirtualHost 192.168.0.1:443>
      DocumentRoot             /var/www/html2
      ServerName               www.mydomain.com
      SSLEngine                on
      SSLCertificateFile       /path/to/your_domain_name.crt
      SSLCertificateKeyFile    /path/to/your_private.key
    </VirtualHost>
    ```
1. 構成をテストします。Apache を再始動する前に、構成ファイルにエラーがないことを確認します。以下のコマンドを実行して、構成をテストします。
    ```
    apachectl configtest
    ```
1. Apache を再始動します。以下のコマンドを実行し、SSL サポートを有効にして Apache を再始動します。
    ```
    apachectl stop
    apachectl start
    ```

SSL サポートが `apache start` でロードされない場合、コマンド `apachectl startssl` を実行します。SSL サポートが有効な Apache が `apachectl startssl` を使用した場合にのみ始動する場合、`apachectl start` コマンドに SSL サポートが含まれるように Apache 始動構成を調整することを推奨します。そうしないと、サーバーのリブートを行う際に、`apachectl startssl` を使用して手動で Apache を再始動する必要が生じる場合があります。これには通常、構成を囲んでいる `<IfDefine SSL>` と `</IfDefine SSL>` の各タグを削除する必要が発生します。
{:note}

### NGINX
{:#cis-origin-certificates-installing-nginx}
1. 起点証明書を注文します。
1. 秘密鍵と起点証明書を、鍵と証明書のファイルを保管するサーバー上のディレクトリーにある個別のファイルに、PEM 形式でコピーします。
1. NGINX 仮想ホスト・ファイルを更新します。ご使用の Web サイト用に NGINX 仮想ホスト・ファイルを編集します。以下の例は、SSL サポート用のサーバー・ブロックを表しています。サーバー・ブロックにある listen ソケットの `ssl` パラメーターを有効にして、ご使用のサイトが HTTP および HTTPS で使用できるようにします。
    ```
    server {
      listen    80;
      listen    443;

      ssl       on;
      ssl_certificate         /path/to/your_certificate.pem;
      ssl_certificate_key     /path/to/your_private.key;
      location / {
        root    /home/www/public_html/yourdomain.com/public/;
        index   index.html;
      }
    }
    ```
1. NGINX を再始動します。以下のコマンドのいずれかを実行して NGINX を再始動します。
    ```
    sudo /etc/init.d/nginx restart
    sudo systemctl restart nginx
    ```

### Apache Tomcat
{:#cis-origin-certificates-installing-apache-tomcat}
1. 起点証明書を注文します。
1. 秘密鍵と起点証明書を、鍵と証明書ファイルを保管するサーバー上のディレクトリーにある個別のファイルに PKCS #7 形式 (cert.p7b) でコピーします。

    SSL 証明書ファイルを、証明書署名要求 (CSR) を生成する際に使用したものと同じ鍵ストアと同じ別名 (あるいは「server」) の下にインストールする必要があります。次のステップのインストール作業は、SSL 証明書ファイルが別の鍵ストアにインストールされている場合は機能しません。
    {:note}

1. 証明書をインストールします。以下のコマンドを実行して、SSL 証明書ファイルを鍵ストアにインストールします。
    ```
    keytool -import -trustcacerts -alias server -file cert.p7b -keystore your_site_name.jks
    ```
    次の確認メッセージが表示されます。**「証明書の応答が鍵ストアにインストールされました (Certificate reply was installed in keystore)」**。証明書を信頼するかどうか尋ねられたら、**y** または **yes** を入力します。これで、鍵ストア・ファイル (your_site_name.jks) が Tomcat サーバー上で使用できるようになりました。

1. SSL コネクターを構成します。Tomcat がセキュア接続を受け入れるようにするには、SSL コネクターを構成します。
    1. Tomcat の server.xml ファイルをテキスト・エディターで開きます。server.xml ファイルは通常、Tomcat のホーム・ディレクトリーの conf フォルダーにあります。
    1. 新しい鍵ストアを保護するために使用するコネクターを識別します。通常は、ポート 443 または 8443 のコネクターが使用されます。
    1. コネクターを囲んでいるタグ (`&#x3C;!--` および `--&#x3E;`) があれば、すべて削除します。
    1. コネクターで構成した正しい鍵ストアのファイル名とパスワードを更新します。
    以下の例は、構成済みの SSL コネクター・ブロックを表しています。
    ```
    <Connector port="443" maxHttpHeaderSize="8192" maxThreads="150" 
    minSpareThreads="25" maxSpareThreads="75" enableLookups="false" 
    disableUploadTimeout="true" acceptCount="100" scheme="https" 
    secure="true" SSLEnabled="true" clientAuth="false" sslProtocol="TLS" 
    keyAlias="server" keystoreFile="/home/user_name/your_site_name.jks" 
    keystorePass="your_keystore_password" />
    ```
    ご使用の Tomcat のバージョンが Tomcat 7 より前の場合、`keystorePass` を `keypass` に変更します。
    {:note}
1. server.xml ファイルを保存します。
1. Tomcat を再始動します。

### Microsoft Internet Information Services (IIS) 7.0
{:#cis-origin-certificates-installing-ms-iis7}
1. IIS マネージャーで証明書署名要求 (CSR) を作成し、`.pem` としてエクスポートします。IIS マネージャーは管理ツールの下にあります。
1. CSR を使用して CIS 起点証明書を注文します。
1. 起点証明書を、サーバーのデスクトップにコピーします。
1. IIS マネージャーを開き、**「接続」**の下でサーバーのホスト名を選択します。
1. 中央メニューの IIS セクションから、**「サーバー証明書」**を選択します。
1. 「操作」メニューから、**「証明書の要求の完了」**を選択します。**「証明機関の応答を指定します」**ページの**「証明機関の応答が含まれるファイルの名前」**の下の`「...」`をクリックして、デスクトップにコピーした `.cer` 証明書ファイルの場所に移動し、ファイルを選択して**「開く」**をクリックします。
1. 証明書の分かりやすい名前を入力します。分かりやすい名前は、証明書を識別するための名前です。
1. **「OK」**を選択して、サーバーでの証明書のインストール作業を終了します。
1. 証明書を Web サイトにバインドします。IIS マネージャーの**「接続」**の下にあるメニューで、サーバー名の下の**「サイト」**を展開して、対象の Web サイトを選択します。「操作」メニューから、**「サイトの編集」**の下の**「バインド」**を選択します。「サイト バインド」ウィンドウで**「追加」**を選択して、以下の情報をサブミットします。
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. これで、ご使用の Web サイトがセキュア接続を受け入れるように構成されました。

### Microsoft Internet Information Services (IIS) 8.0 および 8.5
{:#cis-origin-certificates-installing-ms-iis8-8.5}

1. IIS マネージャーで証明書署名要求 (CSR) を作成し、`.pem` としてエクスポートします。IIS マネージャーは管理ツールの下にあります。
1. CSR を使用して CIS 起点証明書を注文します。
1. 起点証明書を、サーバーのデスクトップにコピーします。
1. IIS マネージャーを開き、**「接続」**の下でサーバーのホスト名を選択します。
1. 中央メニューの IIS セクションから、**「サーバー証明書」**を選択します。
1. 「操作」メニューから、**「証明書の要求の完了」**を選択します。**「証明機関の応答を指定します」**ページの**「証明機関の応答が含まれるファイルの名前」**の下の`「...」`をクリックして、デスクトップにコピーした `.cer` 証明書ファイルの場所に移動し、ファイルを選択して**「開く」**をクリックします。
1. 証明書の分かりやすい名前を入力します。分かりやすい名前は、証明書を識別するための名前です。
1. **「OK」**を選択して、サーバーでの証明書のインストール作業を終了します。
1. 証明書を Web サイトにバインドします。IIS マネージャーの**「接続」**の下にあるメニューで、サーバー名の下の**「サイト」**を展開して、対象の Web サイトを選択します。「操作」メニューから、**「サイトの編集」**の下の**「バインド」**を選択します。「サイト バインド」ウィンドウで**「追加」**を選択して、以下の情報をサブミットします。
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. オプションで、同じ IP アドレスにバインドされた SSL を使用する複数のサイトがある場合は、Server Name Indication (SNI) を使用するように SSL 証明書を構成します。**「サーバー名表示を要求する」**ボックスを選択します。
1. これで、ご使用の Web サイトがセキュア接続を受け入れるように構成されました。

## 起点証明書の取り消し
{:#cis-origin-certificates-revoke}

CIS 起点証明書を削除します。このプロセスは取り消せません。
