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

# 源证书
{:#cis-origin-certificates}

源证书是 CIS 发布的免费 TLS 证书，用于加密源服务器与用户之间的流量。订购免费 TLS 证书以在源服务器上安装。

CIS 源证书仅在 CIS 中使用时有效。
{:note}

## 订购源证书
{:#cis-origin-certificates-ordering}

要订购源证书，请提供证书签名请求 (CSR) 或为 CIS 选择专用密钥类型以生成密钥和 CSR。

在证书保护的源上指定最多 100 个主机名（包括通配符）。通配符仅提供一个级别的覆盖。在相同证书上使用多个通配符可获取更广的覆盖范围（例如，`*.yourdomain.com` 和 `*.yoursubdomain.yourdomain.com`）。CIS 源证书不允许 IP 地址。

指定到期时间。缺省证书到期时间为 15 年。最短到期时间为 7 天。

仅当专用密钥和 CSR 由 CIS 生成时，专用密钥才会在订购证书后立即可用。

## 在服务器上安装源证书
{:#cis-origin-certificates-installing}

### Apache httpd
{:#cis-origin-certificates-installing-apache-httpd}
1. 订购源证书。
1. 将 PEM 格式的专用密钥和源证书复制到服务器上保留密钥和证书文件的目录中的单独文件。
1. 查找 Apache 配置文件。通常，文件名为 `httpd.conf` 或 `apache2.conf`，并且位置是 `/etc/httpd/` 或 `/etc/apache2/`。但是，配置文件可能有所不同，尤其是使用特殊界面来管理服务器时。请参阅 Apache 的 [DistrosDefaultLayout](https://wiki.apache.org/httpd/DistrosDefaultLayout) 以获取缺省安装布局的完整列表。命令以下命令是在 Linux 上搜索 SSL 配置文件的一种方法。
    ```
    grep -i -r "SSLCertificateFile" /etc/httpd/
    ```
1. 找到要配置的 <VirtualHost> 块。（可选）复制要通过 HTTP 和 HTTPS 提供的站点的现有非安全虚拟主机，因为每种类型的连接都需要一个虚拟主机。
1. 针对 SSL 配置 <VirtualHost> 块。以下示例表示 SSL 的简单配置。使用证书和专用密钥的文件名。`SSLCertificateFile` 是 OriginCA 证书文件名，而 `SSLCertificateKeyFile` 是 OriginCA 专用密钥文件名。
    ```
    <VirtualHost 192.168.0.1:443>
      DocumentRoot             /var/www/html2
      ServerName               www.mydomain.com
      SSLEngine                on
      SSLCertificateFile       /path/to/your_domain_name.crt
      SSLCertificateKeyFile    /path/to/your_private.key
    </VirtualHost>
    ```
1. 测试配置。在重新启动 Apache 之前，验证配置文件中是否没有任何错误。运行以下命令来测试配置。
    ```
    apachectl configtest
    ```
1. 重新启动 Apache。运行以下命令以使用 SSL 支持来重新启动 Apache。
    ```
    apachectl stop
    apachectl start
    ```

如果使用 `apache start` 无法装入 SSL 支持，请运行命令 `apachectl startssl`。如果 Apache 在使用 `apachectl startssl` 时仅启动 SSL 支持，那么建议调整 Apache 启动配置以在命令 `apachectl start` 中包含 SSL 支持。否则，在服务器重新引导时，您可能需要使用 `apachectl startssl` 手动重新启动 Apache。这通常涉及除去围绕配置的 `<IfDefine SSL>` 和 `</IfDefine SSL>` 标记。
{:note}

### NGINX
{:#cis-origin-certificates-installing-nginx}
1. 订购源证书。
1. 将 PEM 格式的专用密钥和源证书复制到服务器上保留密钥和证书文件的目录中的单独文件。
1. 更新 NGINX 虚拟主机文件。编辑 Web 站点的 NGINX 虚拟主机文件。以下示例表示 SSL 支持的服务器块。在服务器块中的侦听套接字上启用 `ssl` 参数以使站点通过 HTTP 和 HTTPS 可用。
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
1. 重新启动 NGINX。运行以下某个命令以重新启动 NGINX。
    ```
    sudo /etc/init.d/nginx restart
    sudo systemctl restart nginx
    ```

### Apache Tomcat
{:#cis-origin-certificates-installing-apache-tomcat}
1. 订购源证书。
1. 将 PKCS #7 格式 (cert.p7b) 的专用密钥和源证书复制到服务器上保留密钥和证书文件的目录中的单独文件。

    必须将 SSL 证书文件安装到相同密钥库，并且使用用于生成证书签名请求 (CSR) 的相同别名（或“服务器”）。如果 SSL 证书文件安装到其他密钥库，那么下一步中的安装将不起作用。
    {:note}

1. 安装证书。运行以下命令以将 SSL 证书文件安装到密钥库。
    ```
    keytool -import -trustcacerts -alias server -file cert.p7b -keystore your_site_name.jks
    ```
    将显示确认消息：**“Certificate reply was installed in keystore.”**如果系统要求信任该证书，请输入 **y** 或 **yes**。密钥库文件 (your_site_name.jks) 现已准备好用于 Tomcat 服务器。

1. 配置 SSL 连接器。配置 SSL 连接器以使 Tomcat 能够接受安全连接。
    1. 在文本编辑器中打开 Tomcat server.xml 文件。server.xml 文件通常位于 Tomcat 主目录的 conf 文件夹中。
    1. 确定要用于保护新密钥库的连接器。通常使用端口为 443 或 8443 的连接器。
    1. 除去可能围绕连接器的任何注释标记（`<!--` 和 `-->`）。
    1. 更新连接器配置中的正确密钥库文件名和密码。以下示例表示配置的 SSL 连接器块。
    ```
    <Connector port="443" maxHttpHeaderSize="8192" maxThreads="150" 
    minSpareThreads="25" maxSpareThreads="75" enableLookups="false" 
    disableUploadTimeout="true" acceptCount="100" scheme="https" 
    secure="true" SSLEnabled="true" clientAuth="false" sslProtocol="TLS" 
    keyAlias="server" keystoreFile="/home/user_name/your_site_name.jks" 
    keystorePass="your_keystore_password" />
    ```
    如果 Tomcat 版本早于 Tomcat 7，请将 `keystorePass` 更改为 `keypass`。
    {:note}
1. 保存 server.xml 文件。
1. 重新启动 Tomcat。

### Microsoft Internet Information Services (IIS) 7.0
{:#cis-origin-certificates-installing-ms-iis7}
1. 在 IIS 管理器中创建证书签名请求 (CSR) 并将其导出为 `.pem`。IIS 管理器位于管理工具下。
1. 使用 CSR 订购 CIS 源证书。
1. 将源证书复制到服务器的桌面。
1. 打开 IIS 管理器并选择**连接**下的服务器主机名。
1. 从中心菜单中的 IIS 部分中选择**服务器证书**。
1. 从“操作”菜单中选择操作**完成证书请求**。在**包含认证中心响应的文件名**下的**指定认证中心响应**页面上，单击 `...` 以浏览至复制到桌面的 `.cer` 证书文件，选择该文件，然后单击**打开**。
1. 输入证书的友好名称。友好名称用于标识证书。
1. 选择**确定**以完成服务器的证书安装。
1. 将证书绑定到 Web 站点。通过展开 IIS 管理器中**连接**下的菜单中服务器名称下的**站点**，选择 Web 站点。从“操作”菜单中的**编辑站点**下选择**绑定**。从“站点绑定”窗口中选择**添加**，然后提交以下信息。
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. 您的 Web 站点现已配置为接受安全连接。

### Microsoft Internet Information Services (IIS) 8.0 和 8.5
{:#cis-origin-certificates-installing-ms-iis8-8.5}

1. 在 IIS 管理器中创建证书签名请求 (CSR) 并将其导出为 `.pem`。IIS 管理器位于管理工具下。
1. 使用 CSR 订购 CIS 源证书。
1. 将源证书复制到服务器的桌面。
1. 打开 IIS 管理器并选择**连接**下的服务器主机名。
1. 从中心菜单中的 IIS 部分中选择**服务器证书**。
1. 从“操作”菜单中选择操作**完成证书请求**。在**包含认证中心响应的文件名**下的**指定认证中心响应**页面上，单击 `...` 以浏览至复制到桌面的 `.cer` 证书文件，选择该文件，然后单击**打开**。
1. 输入证书的友好名称。友好名称用于标识证书。
1. 选择**确定**以完成服务器的证书安装。
1. 将证书绑定到 Web 站点。通过展开 IIS 管理器中**连接**下的菜单中服务器名称下的**站点**，选择 Web 站点。从“操作”菜单中的**编辑站点**下选择**绑定**。从“站点绑定”窗口中选择**添加**，然后提交以下信息。
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. （可选）如果有多个站点使用绑定到相同 IP 地址的 SSL，那么配置 SSL 证书以使用“服务器名称指示”(SNI)。选择**需要服务器名称指示**框。
1. 您的 Web 站点现已配置为接受安全连接。

## 撤销源证书
{:#cis-origin-certificates-revoke}

删除 CIS 源证书。此过程无法撤销。

