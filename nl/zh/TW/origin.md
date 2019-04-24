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

# 原點憑證
{:#cis-origin-certificates}

「原點憑證」是由 CIS 發出的免費 TLS 憑證，可將原點伺服器與使用者之間的資料流量加密。請訂購免費的 TLS 憑證以安裝在您的原點伺服器上。

「CIS 原點憑證」要用於 CIS 中才有效。
{:note}

## 訂購原點憑證
{:#cis-origin-certificates-ordering}

若要訂購原點憑證，請提供「憑證簽署要求 (CSR)」，或選取 CIS 的私密金鑰類型以產生金鑰及 CSR。

在憑證所保護的原點上最多指定 100 個主機名稱（包括萬用字元）。萬用字元只提供一層涵蓋面。在相同憑證上使用多個萬用字元可以有更廣泛的涵蓋面（例如 `*.yourdomain.com` 及 `*.yoursubdomain.yourdomain.com`）。CIS 原點憑證不允許使用 IP 位址。

請指定有效期限。預設憑證有效期限為 15 年。最短有效期限為七天。

如果私密金鑰及 CSR 是由 CIS 產生，則私密金鑰只有在訂購憑證之後才立即可用。

## 在伺服器上安裝原點憑證
{:#cis-origin-certificates-installing}

### Apache httpd
{:#cis-origin-certificates-installing-apache-httpd}
1. 訂購原點憑證。
1. 以 PEM 格式將私密金鑰及原點憑證複製到您在伺服器上保留金鑰及憑證檔之目錄中的個別檔案。
1. 找出 Apache 配置檔。通常檔名是 `httpd.conf` 或 `apache2.conf`，位置是 `/etc/httpd/` 或 `/etc/apache2/`。不過，您的配置檔可能會有所不同，尤其是當您使用特殊介面來管理伺服器時。如需預設安裝佈置的完整清單，請參閱 Apache 的 [DistrosDefaultLayout](https://wiki.apache.org/httpd/DistrosDefaultLayout)。下列指令是在 Linux 上搜尋 SSL 配置檔的方法之一。
    ```
    grep -i -r "SSLCertificateFile" /etc/httpd/
    ```
1. 找出要配置的 <VirtualHost> 區塊。您可以選擇性地複製現有未受保護的虛擬主機，讓您的網站可以透過 HTTP 及 HTTPS 來使用，因為每一種連線類型都需要一個虛擬主機。
1. 配置 SSL 的 <VirtualHost> 區塊。下列範例代表 SSL 的簡單配置。請使用憑證及私密金鑰的檔名。`SSLCertificateFile` 是 OriginCA 憑證檔名，`SSLCertificateKeyFile` 是 OriginCA 私密金鑰檔名。
    ```
    <VirtualHost 192.168.0.1:443>
      DocumentRoot             /var/www/html2
      ServerName               www.mydomain.com
      SSLEngine                on
      SSLCertificateFile       /path/to/your_domain_name.crt
      SSLCertificateKeyFile    /path/to/your_private.key
    </VirtualHost>
    ```
1. 測試您的配置。重新啟動 Apache 之前，請驗證配置檔中沒有任何錯誤。執行下列指令來測試您的配置。
    ```
    apachectl configtest
    ```
1. 重新啟動 Apache。執行下列指令來重新啟動 Apache 以及 SSL 支援。
    ```
    apachectl stop
    apachectl start
    ```

如果 SSL 支援未隨 `apache start` 載入，請執行 `apachectl startssl` 指令。如果只能使用 `apachectl startssl` 讓 Apache 在啟動時具有 SSL 支援，則建議調整 Apache 啟動配置，以便在 `apachectl start` 指令中包括 SSL 支援。否則，萬一伺服器重新開機，您可能需要使用 `apachectl startssl` 來手動重新啟動 Apache。這通常需要移除 `<IfDefine SSL>` 及 `</IfDefine SSL>` 標籤（其含括您的配置）。
{:note}

### NGINX
{:#cis-origin-certificates-installing-nginx}
1. 訂購原點憑證。
1. 以 PEM 格式將私密金鑰及原點憑證複製到您在伺服器上保留金鑰及憑證檔之目錄中的個別檔案。
1. 更新 NGINX 虛擬主機檔案。編輯您網站的 NGINX 虛擬主機檔案。下列範例代表 SSL 支援的伺服器區塊。在伺服器區塊的接聽 Socket 上啟用 `ssl` 參數，讓您的網站可以透過 HTTP 及 HTTPS 來使用。
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
1. 重新啟動 NGINX。執行下列其中一項指令來重新啟動 NGINX。
    ```
    sudo /etc/init.d/nginx restart
    sudo systemctl restart nginx
    ```

### Apache Tomcat
{:#cis-origin-certificates-installing-apache-tomcat}
1. 訂購原點憑證。
1. 以 PKCS #7 格式 (cert.p7b) 將私密金鑰及原點憑證複製到您在伺服器上保留金鑰及憑證檔之目錄中的個別檔案。

    您必須將 SSL 憑證檔安裝到相同的金鑰儲存庫，並使用您用來產生「憑證簽署要求 (CSR)」的相同別名（或 "server"）。如果 SSL 憑證檔是安裝到不同的金鑰儲存庫，則下一步的安裝將無效。
    {:note}

1. 安裝憑證。執行下列指令，將 SSL 憑證檔安裝到您的金鑰儲存庫。
    ```
    keytool -import -trustcacerts -alias server -file cert.p7b -keystore your_site_name.jks
    ```
    將會出現一則確認訊息：**"Certificate reply was installed in keystore."** 如果詢問您是否信任該憑證，請輸入 **y** 或 **yes**。您的金鑰儲存庫檔 (your_site_name.jks) 現在已備妥，可以在 Tomcat 伺服器上使用。

1. 配置「SSL 連接器」。配置「SSL 連接器」，讓 Tomcat 能夠接受安全連線。
    1. 在文字編輯器中開啟 Tomcat server.xml 檔案。server.xml 檔案通常位於 Tomcat 起始目錄的 conf 資料夾中。
    1. 識別用來保護新金鑰儲存庫安全的連接器。通常使用具有埠 443 或 8443 的連接器。
    1. 移除任何可能括住連接器的註解標籤（`<!--` 及 `-->`）。
    1. 在連接器配置中更新正確的金鑰儲存庫檔名及密碼。
    下列範例代表已配置的「SSL 連接器」區塊。
    ```
    <Connector port="443" maxHttpHeaderSize="8192" maxThreads="150"
    minSpareThreads="25" maxSpareThreads="75" enableLookups="false"
    disableUploadTimeout="true" acceptCount="100" scheme="https"
    secure="true" SSLEnabled="true" clientAuth="false" sslProtocol="TLS"
    keyAlias="server" keystoreFile="/home/user_name/your_site_name.jks"
    keystorePass="your_keystore_password" />
    ```
    如果您的 Tomcat 版本是 Tomcat 7 以前的版本，請將 `keystorePass` 變更為 `keypass`。
    {:note}
1. 儲存 server.xml 檔案。
1. 重新啟動 Tomcat。

### Microsoft Internet Information Services (IIS) 7.0
{:#cis-origin-certificates-installing-ms-iis7}
1. 在 IIS Manager 中建立「憑證簽署要求 (CSR)」，並將它匯出為 `.pem`。IIS Manager 位於「系統管理工具」下。
1. 使用 CSR 訂購「CIS 原點憑證」。
1. 將原點憑證複製到伺服器的桌面。
1. 開啟 IIS Manager，並在**連線**下選取您的伺服器主機名稱。
1. 從中央功能表的 IIS 區段中，選取**伺服器憑證**。
1. 從「動作」功能表中，選取**完成憑證要求**動作。在**指定憑證管理中心回應**頁面的**包含憑證管理中心回應的檔名**下，按一下 `...` 以瀏覽至複製到桌面的 `.cer` 憑證檔，並選取該檔案，然後按一下**開啟**。
1. 輸入憑證的一般名稱。一般名稱可識別該憑證。
1. 選取**確定**，以完成伺服器的憑證安裝。
1. 將憑證連結至您的網站。在 IIS Manager **連線**下的功能表中，展開您伺服器名稱下的**網站**，以選取您的網站。從「動作」功能表中選取**編輯網站**下的**連結**。從「網站連結」視窗中選取**新增**，並提交下列資訊。
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. 您的網站現在已配置為接受安全連線。

### Microsoft Internet Information Services (IIS) 8.0 及 8.5
{:#cis-origin-certificates-installing-ms-iis8-8.5}

1. 在 IIS Manager 中建立「憑證簽署要求 (CSR)」，並將它匯出為 `.pem`。IIS Manager 位於「系統管理工具」下。
1. 使用 CSR 訂購「CIS 原點憑證」。
1. 將原點憑證複製到伺服器的桌面。
1. 開啟 IIS Manager，並在**連線**下選取您的伺服器主機名稱。
1. 從中央功能表的 IIS 區段中，選取**伺服器憑證**。
1. 從「動作」功能表中，選取**完成憑證要求**動作。在**指定憑證管理中心回應**頁面的**包含憑證管理中心回應的檔名**下，按一下 `...` 以瀏覽至複製到桌面的 `.cer` 憑證檔，並選取該檔案，然後按一下**開啟**。
1. 輸入憑證的一般名稱。一般名稱可識別該憑證。
1. 選取**確定**，以完成伺服器的憑證安裝。
1. 將憑證連結至您的網站。在 IIS Manager **連線**下的功能表中，展開您伺服器名稱下的**網站**，以選取您的網站。從「動作」功能表中選取**編輯網站**下的**連結**。從「網站連結」視窗中選取**新增**，並提交下列資訊。
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. 如果您有多個網站使用連結到相同 IP 位址的 SSL，可選擇性地配置 SSL 憑證來使用「伺服器名稱指示 (SNI)」。請選取**需要伺服器名稱指示**方框。
1. 您的網站現在已配置為接受安全連線。

## 撤銷原點憑證
{:#cis-origin-certificates-revoke}

刪除「CIS 原點憑證」。此處理程序無法復原。
