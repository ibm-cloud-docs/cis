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

# Certificados de origem
{:#cis-origin-certificates}

Os Certificados de origem são certificados TLS gratuitos emitidos pelo CIS que criptografam o tráfego entre seu servidor de origem e seus usuários. Solicite certificados TLS grátis para instalar em seu servidor de origem.

Os Certificados de origem do CIS são válidos apenas para uso no CIS.
{:note}

## Solicitando um certificado de origem
{:#cis-origin-certificates-ordering}

Para solicitar um certificado de origem, forneça uma Solicitação de Assinatura de Certificado (CSR) ou selecione um tipo de chave privada para que o CIS gere uma chave e uma CSR.

Especifique até 100 nomes de host (incluindo curingas) em sua origem protegida pelo certificado. Os curingas fornecem apenas um nível de cobertura. Use diversos curingas no mesmo certificado para uma cobertura mais ampla (por exemplo, `*.yourdomain.com` e `*.yoursubdomain.yourdomain.com`). Os Certificados de Origem do CIS não permitem endereços IP.

Especifique a expiração. A expiração do certificado padrão ocorre após 15 anos. A expiração mais curta é de sete dias.

A chave privada somente estará disponível imediatamente após a solicitação de um certificado se a chave privada e a CSR tiverem sido geradas pelo CIS.

## Instalando um certificado de origem em seu servidor
{:#cis-origin-certificates-installing}

### Apache httpd
{:#cis-origin-certificates-installing-apache-httpd}
1. Solicite um certificado de origem.
1. Copie a chave privada e o certificado de origem no formato PEM em arquivos separados no diretório em seu servidor no qual você mantém os arquivos de chave e de certificado.
1. Localize seu arquivo de configuração do Apache. Geralmente, os nomes de arquivos são `httpd.conf` ou `apache2.conf` e os locais são `/etc/httpd/` ou `/etc/apache2/`. No entanto, seu arquivo de configuração pode variar, especialmente se você utilizar uma interface especial para gerenciar seu servidor. Consulte o [DistrosDefaultLayout](https://wiki.apache.org/httpd/DistrosDefaultLayout) do Apache para obter uma lista completa de layouts de instalação padrão. O comando a seguir é uma maneira de procurar o arquivo de configuração SSL no Linux.
    ```
    grep -i -r "SSLCertificateFile" /etc/httpd/
    ```
1. Localize o bloco <VirtualHost > a ser configurado. Opcionalmente, copie o host virtual não seguro existente para que seu site fique disponível por meio de HTTP e HTTPS, porque cada tipo de conexão requer um host virtual.
1. Configure o bloco <VirtualHost > para SSL. O exemplo a seguir representa uma configuração simples para SSL. Use os nomes de arquivos para seu certificado e chave privada. `SSLCertificateFile` é o nome do arquivo de seu certificado de OriginCA e `SSLCertificateKeyFile` é o nome do arquivo da chave privada de OriginCA.
    ```
    <VirtualHost 192.168.0.1:443>
      DocumentRoot             /var/www/html2
      ServerName               www.mydomain.com
      SSLEngine                on
      SSLCertificateFile       /path/to/your_domain_name.crt
      SSLCertificateKeyFile    /path/to/your_private.key
    </VirtualHost>
    ```
1. Teste sua configuração. Antes de reiniciar o Apache, verifique se não há erros em seus arquivos de configuração. Execute o comando a seguir para testar sua configuração.
    ```
    apachectl configtest
    ```
1. Reinicie o Apache. Execute os comandos a seguir para reiniciar o Apache com o suporte SSL.
    ```
    apachectl stop
    apachectl start
    ```

Se o suporte SSL não for carregado com `apache start`, execute o comando `apachectl startssl`. Se o Apache for iniciado somente com o suporte SSL, usando `apachectl startssl`, recomenda-se ajustar a configuração de inicialização do Apache para incluir o suporte SSL no comando `apachectl start`. Caso contrário, no caso de uma reinicialização do servidor, pode ser necessário reiniciar manualmente o Apache usando `apachectl startssl`. Isso geralmente envolve remover as tags `<IfDefine SSL>` e `</IfDefine SSL>` que delimitam sua configuração.
{:note}

### NGINX
{:#cis-origin-certificates-installing-nginx}
1. Solicite um certificado de origem.
1. Copie a chave privada e o certificado de origem no formato PEM em arquivos separados no diretório em seu servidor no qual você mantém os arquivos de chave e de certificado.
1. Atualize o arquivo de hosts virtuais NGINX. Edite o arquivo de host virtual do NGINX para seu website. O exemplo a seguir representa um bloco do servidor para o suporte SSL. Ative o parâmetro `ssl` em soquetes de recebimento no bloco do servidor para que seu site fique disponível por meio de HTTP e HTTPS.
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
1. Reinicie o NGINX. Execute um dos comandos a seguir para reiniciar o NGINX.
    ```
    sudo /etc/init.d/nginx restart
    sudo systemctl restart nginx
    ```

### Apache Tomcat
{:#cis-origin-certificates-installing-apache-tomcat}
1. Solicite um certificado de origem.
1. Copie a chave privada e o certificado de origem no formato PKCS #7 (cert.p7b) em arquivos separados no diretório em seu servidor no qual você mantém os arquivos de chave e de certificado.

    Você deve instalar o arquivo de Certificado SSL no mesmo keystore e sob o mesmo nome de alias (ou, "servidor") que você utilizou para gerar seu Certificate Signing Request (CSR). A instalação na próxima etapa não funcionará se o arquivo do certificado SSL estiver instalado em um keystore diferente.
    {:note}

1. Instale o certificado. Execute o comando a seguir para instalar o arquivo do certificado SSL em seu keystore.
    ```
    keytool -import -trustcacerts -alias server -file cert.p7b -keystore your_site_name.jks
    ```
    Haverá uma mensagem de confirmação: **"A resposta do certificado foi instalada no keystore".** Insira **y** ou **yes** se solicitado a confiar no certificado. Seu arquivo keystore (your_site_name.jks) agora está pronto para ser usado em seu Servidor Tomcat.

1. Configure seu Conector SSL. Configure um Conector SSL para que o Tomcat seja capaz de aceitar conexões seguras.
    1. Abra o arquivo server.xml do Tomcat em um editor de texto. O arquivo server.xml é geralmente localizado na pasta conf do diretório inicial do seu Tomcat.
    1. Identifique o conector a ser usado para proteger o novo keystore. Um conector com a porta 443 ou 8443 é geralmente usado.
    1. Remova quaisquer tags de comentário (`<!--` and `-->`) que possam estar em torno do conector.
    1. Atualize o nome do arquivo e a senha corretos do keystore na configuração de seu conector.
    O exemplo a seguir representa um bloco do Conector SSL configurado.
    ```
    <Connector port="443" maxHttpHeaderSize="8192" maxThreads="150" 
    minSpareThreads="25" maxSpareThreads="75" enableLookups="false" 
    disableUploadTimeout="true" acceptCount="100" scheme="https" 
    secure="true" SSLEnabled="true" clientAuth="false" sslProtocol="TLS" 
    keyAlias="server" keystoreFile="/home/user_name/your_site_name.jks" 
    keystorePass="your_keystore_password" />
    ```
    Se a versão de seu Tomcat for anterior ao Tomcat 7, mude `keystorePass` para `keypass`.
    {:note}
1. Salve seu arquivo server.xml.
1. Reinicie o Tomcat.

### Microsoft Internet Information Services (IIS) 7.0
{:#cis-origin-certificates-installing-ms-iis7}
1. Crie uma Certificate Signing Request (CSR) no IIS Manager e exporte-a como `.pem`. O IIS Manager está localizado em Ferramentas Administrativas.
1. Solicite um Certificado de origem do CIS usando sua CSR.
1. Copie o certificado de origem na área de trabalho de seu servidor.
1. Abra o IIS Manager e selecione o nome do host do seu servidor em **Conexões**.
1. Selecione **Certificados do servidor** na seção IIS do menu central.
1. Selecione a ação **Concluir solicitação de certificado** no menu Ações. Na página **Especificar resposta da autoridade de certificação**, em **Nome do arquivo que contém a resposta da autoridade de certificação**, clique em `...` para procurar o arquivo de certificado `.cer` que foi copiado para a área de trabalho, em seguida, selecione o arquivo e clique em **Abrir**.
1. Insira um nome fácil para o certificado. O nome fácil identifica o certificado.
1. Selecione **OK** para concluir a instalação do certificado em seu servidor.
1. Ligar o certificado ao seu website. Selecione seu website expandindo **Sites** no nome do seu servidor, no menu em **Conexões** no IIS Manager. Selecione **Ligações** em **Editar site** no menu Ações. Selecione **Incluir** na janela Ligações de site e envie as informações a seguir.
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. Agora, seu website está configurado para aceitar conexões seguras.

### Microsoft Internet Information Services (IIS) 8.0 e 8.5
{:#cis-origin-certificates-installing-ms-iis8-8.5}

1. Crie uma Certificate Signing Request (CSR) no IIS Manager e exporte-a como `.pem`. O IIS Manager está localizado em Ferramentas Administrativas.
1. Solicite um Certificado de origem do CIS usando sua CSR.
1. Copie o certificado de origem na área de trabalho de seu servidor.
1. Abra o IIS Manager e selecione o nome do host do seu servidor em **Conexões**.
1. Selecione **Certificados do servidor** na seção IIS do menu central.
1. Selecione a ação **Concluir solicitação de certificado** no menu Ações. Na página **Especificar resposta da autoridade de certificação**, em **Nome do arquivo que contém a resposta da autoridade de certificação**, clique em `...` para procurar o arquivo de certificado `.cer` que foi copiado para a área de trabalho, em seguida, selecione o arquivo e clique em **Abrir**.
1. Insira um nome fácil para o certificado. O nome fácil identifica o certificado.
1. Selecione **OK** para concluir a instalação do certificado em seu servidor.
1. Ligar o certificado ao seu website. Selecione seu website expandindo **Sites** no nome do seu servidor, no menu em **Conexões** no IIS Manager. Selecione **Ligações** em **Editar site** no menu Ações. Selecione **Incluir** na janela Ligações de site e envie as informações a seguir.
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. Opcionalmente, configure seu certificado SSL para usar a Indicação de Nome do Servidor (SNI), caso tenha diversos sites usando o limite SSL para o mesmo endereço IP.  Selecione a caixa **Solicitar a indicação de nome do servidor**.
1. Agora, seu website está configurado para aceitar conexões seguras.

## Revogando um certificado de origem
{:#cis-origin-certificates-revoke}

Exclua seu Certificado de origem do CIS. Não é possível desfazer esse processo.
