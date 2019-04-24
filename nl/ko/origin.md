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

# 오리진 인증서
{:#cis-origin-certificates}

오리진 인증서는 오리진 서버와 사용자 간 트래픽을 암호화하는, CIS에서 발행한 무료 TLS 인증서입니다. 오리진 서버에 설치할 무료 TLS 인증서를 주문하십시오.

CIS 오리진 인증서는 CIS에서 사용하는 경우에만 유효합니다.
{:note}

## 오리진 인증서 주문
{:#cis-origin-certificates-ordering}

오리진 인증서를 주문하려면 인증서 서명 요청(CSR)을 제공하거나 CIS의 개인 키 유형을 선택하여 키 및 CSR을 생성하십시오.

오리진에서 인증서가 보호하는 최대 100개의 호스트 이름(와일드카드 포함)을 지정하십시오. 와일드카드는 한 레벨의 적용 범위만 제공합니다. 적용 범위를 넓히기 위해 동일한 인증서에 여러 와일드카드를 사용하십시오(예: `*.yourdomain.com` 및 `*.yoursubdomain.yourdomain.com`). CIS 오리진 인증서는 IP 주소를 허용하지 않습니다.

만기를 지정하십시오. 기본 인증서의 만기는 15년입니다. 가장 짧은 만기는 7일입니다.

개인 키는 개인 키 및 CSR이 CIS에서 생성된 경우 인증서를 주문한 직후에만 사용 가능합니다.

## 서버에 오리진 인증서 설치
{:#cis-origin-certificates-installing}

### Apache httpd
{:#cis-origin-certificates-installing-apache-httpd}
1. 오리진 인증서를 주문합니다.
1. 키 및 인증서 파일을 보관하는 서버의 디렉토리에 대한 별도의 파일로 PEM 형식의 개인 키 및 오리진 인증서를 복사합니다.
1. Apache 구성 파일을 찾습니다. 일반적으로 파일 이름은 `httpd.conf` 또는 `apache2.conf`이며 위치는 `/etc/httpd/` 또는 `/etc/apache2/`입니다. 하지만 구성 파일은 특히 특수 인터페이스를 사용하여 서버를 관리하는 경우 다를 수 있습니다. 기본 설치 레이아웃의 전체 목록은 Apache의 [DistrosDefaultLayout](https://wiki.apache.org/httpd/DistrosDefaultLayout)을 참조하십시오. 다음 명령은 Linux에서 SSL 구성 파일을 검색하는 방법 중 하나입니다.
    ```
    grep -i -r "SSLCertificateFile" /etc/httpd/
    ```
1. 구성할 <VirtualHost> 블록을 찾습니다. 각 연결 유형에 가상 호스트가 필요하므로 HTTP 및 HTTPS를 통해 사용 가능한 사이트의 기존 비보안 가상 호스트를 복사합니다.
1. SSL의 <VirtualHost> 블록을 구성합니다. 다음 예제는 SSL에 대한 간단한 구성을 나타냅니다. 인증서 및 개인 키의 파일 이름을 사용합니다. `SSLCertificateFile`은 OriginCA 인증서 파일 이름이고 `SSLCertificateKeyFile`은 OriginCA 개인 키 파일 이름입니다.
    ```
    <VirtualHost 192.168.0.1:443>
      DocumentRoot             /var/www/html2
      ServerName               www.mydomain.com
      SSLEngine                on
      SSLCertificateFile       /path/to/your_domain_name.crt
      SSLCertificateKeyFile    /path/to/your_private.key
    </VirtualHost>
    ```
1. 구성을 테스트합니다. Apache를 다시 시작하기 전에 구성 파일에 오류가 없는지 확인합니다. 다음 명령을 실행하여 구성을 테스트합니다.
    ```
    apachectl configtest
    ```
1. Apache를 다시 시작합니다. 다음 명령을 실행하여 SSL 지원을 통해 Apache를 다시 시작합니다.
    ```
    apachectl stop
    apachectl start
    ```

SSL 지원이 `apache start`를 사용하여 로드되지 않는 경우, `apachectl startssl` 명령을 실행하십시오. Apache가 `apachectl startssl`을 사용하여 SSL 지원을 통해서만 시작되는 경우 `apachectl start` 명령에 SSL 지원을 포함하도록 Apache 시작 구성을 조정하는 것이 좋습니다. 그렇지 않으면 서버가 다시 부팅되는 경우 `apachectl startssl`을 사용하여 Apache를 수동으로 다시 시작해야 합니다. 여기에는 일반적으로 구성을 둘러싸는 `<IfDefine SSL>` 및 `</IfDefine SSL>` 태그 제거가 포함됩니다.
{:note}

### NGINX
{:#cis-origin-certificates-installing-nginx}
1. 오리진 인증서를 주문합니다.
1. 키 및 인증서 파일을 보관하는 서버의 디렉토리에 대한 별도의 파일로 PEM 형식의 개인 키 및 오리진 인증서를 복사합니다.
1. NGINX 가상 호스트 파일을 업데이트합니다. 웹 사이트의 NGINX 가상 호스트 파일을 편집합니다. 다음 예제는 SSL 지원을 위한 서버 블록을 나타냅니다. HTTP 및 HTTPS를 통해 사용 가능한 사이트의 서버 블록에 있는 청취 소켓에 `ssl` 매개변수를 사용하십시오.
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
1. NGINX를 다시 시작합니다. NGINX를 다시 시작하려면 다음 명령 중 하나를 실행합니다.
    ```
    sudo /etc/init.d/nginx restart
    sudo systemctl restart nginx
    ```

### Apache Tomcat
{:#cis-origin-certificates-installing-apache-tomcat}
1. 오리진 인증서를 주문합니다.
1. 키 및 인증서 파일을 보관하는 서버의 디렉토리에 대한 별도의 파일로 PKCS #7 형식(cert.p7b)의 개인 키 및 오리진 인증서를 복사합니다.

    인증서 서명 요청(CSR)을 생성하는 데 사용한 것과 동일한 별명 이름(또는 "서버")으로 동일한 키 저장소에 SSL 인증서 파일을 설치해야 합니다. SSL 인증서 파일이 다른 키 저장소에 설치된 경우 다음 단계의 설치는 작동하지 않습니다.
    {:note}

1. 인증서를 설치합니다. 다음 명령을 실행하여 키 저장소에 SSL 인증서 파일을 설치합니다.
    ```
    keytool -import -trustcacerts -alias server -file cert.p7b -keystore your_site_name.jks
    ```
    다음과 같은 확인 메시지가 표시됩니다. **"인증서 응답이 키 저장소에 설치되었습니다."** 인증서를 신뢰하도록 요청되는 경우 **y** 또는 **yes**를 입력하십시오. 키 저장소 파일(your_site_name.jks)을 이제 Tomcat 서버에서 사용할 수 있습니다.

1. SSL 커넥터를 구성합니다. Tomcat이 보안 연결을 허용할 수 있도록 SSL 커넥터를 구성합니다.
    1. 텍스트 편집기에서 Tomcat server.xml 파일을 엽니다. server.xml 파일은 일반적으로 Tomcat 홈 디렉토리의 conf 폴더에 있습니다.
    1. 새 키 저장소에 보안을 설정하는 데 사용할 커넥터를 식별합니다. 일반적으로 포트가 443 또는 8443인 커넥터가 사용됩니다.
    1. 커넥터를 둘러싸는 주석 태그(`<!--` and `-->`)를 제거합니다.
    1. 커넥터 구성에서 올바른 키 저장소 파일 이름과 비밀번호를 업데이트합니다.
    다음 예제는 구성된 SSL 커넥터 블록을 나타냅니다.
    ```
    <Connector port="443" maxHttpHeaderSize="8192" maxThreads="150" 
    minSpareThreads="25" maxSpareThreads="75" enableLookups="false" 
    disableUploadTimeout="true" acceptCount="100" scheme="https" 
    secure="true" SSLEnabled="true" clientAuth="false" sslProtocol="TLS" 
    keyAlias="server" keystoreFile="/home/user_name/your_site_name.jks" 
    keystorePass="your_keystore_password" />
    ```
    Tomcat 버전이 Tomcat 7 이전인 경우 `keystorePass`에서 `keypass`로 변경하십시오.
    {:note}
1. server.xml 파일을 저장합니다.
1. Tomcat을 다시 시작합니다.

### Microsoft IIS(Internet Information Services) 7.0
{:#cis-origin-certificates-installing-ms-iis7}
1. IIS 관리자에서 인증서 서명 요청(CSR)을 작성하고 이를 `.pem`으로 내보냅니다. IIS 관리자는 관리 도구에 있습니다.
1. CSR을 사용하여 CIS 오리진 인증서를 주문합니다.
1. 서버의 데스크탑에 오리진 인증서를 복사합니다.
1. IIS 관리자를 열고 **연결**에서 서버의 호스트 이름을 선택합니다.
1. 중앙 메뉴의 IIS 섹션에서 **서버 인증서**를 선택합니다.
1. 조치 메뉴에서 **완전한 인증서 요청** 조치를 선택합니다. **인증 기관 응답 지정** 페이지의 **인증 기관의 응답이 포함된 파일 이름**에서 `...`를 클릭하여 데스크탑에 복사된 `.cer` 인증서 파일을 찾아보고 파일을 선택한 다음 **열기**를 클릭합니다.
1. 알아보기 쉬운 인증서 이름을 입력합니다. 알아보기 쉬운 이름은 인증서를 식별합니다.
1. **확인**을 선택하여 서버에 대한 인증서 설치를 완료합니다.
1. 웹 사이트에 인증서를 바인드합니다. IIS 관리자에서 **연결** 아래 메뉴의 서버 이름 아래에 있는 **사이트**를 펼쳐 웹 사이트를 선택합니다. 조치 메뉴에서 **사이트 편집** 아래에 있는 **바인딩**을 선택합니다. 사이트 바인딩 창에서 **추가**를 선택하고 다음 정보를 제출합니다.
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. 이제 웹 사이트는 보안 연결을 허용하도록 구성됩니다.

### Microsoft IIS(Internet Information Services) 8.0 및 8.5
{:#cis-origin-certificates-installing-ms-iis8-8.5}

1. IIS 관리자에서 인증서 서명 요청(CSR)을 작성하고 이를 `.pem`으로 내보냅니다. IIS 관리자는 관리 도구에 있습니다.
1. CSR을 사용하여 CIS 오리진 인증서를 주문합니다.
1. 서버의 데스크탑에 오리진 인증서를 복사합니다.
1. IIS 관리자를 열고 **연결**에서 서버의 호스트 이름을 선택합니다.
1. 중앙 메뉴의 IIS 섹션에서 **서버 인증서**를 선택합니다.
1. 조치 메뉴에서 **완전한 인증서 요청** 조치를 선택합니다. **인증 기관 응답 지정** 페이지의 **인증 기관의 응답이 포함된 파일 이름**에서 `...`를 클릭하여 데스크탑에 복사된 `.cer` 인증서 파일을 찾아보고 파일을 선택한 다음 **열기**를 클릭합니다.
1. 알아보기 쉬운 인증서 이름을 입력합니다. 알아보기 쉬운 이름은 인증서를 식별합니다.
1. **확인**을 선택하여 서버에 대한 인증서 설치를 완료합니다.
1. 웹 사이트에 인증서를 바인드합니다. IIS 관리자에서 **연결** 아래 메뉴의 서버 이름 아래에 있는 **사이트**를 펼쳐 웹 사이트를 선택합니다.조치 메뉴에서 **사이트 편집** 아래에 있는 **바인딩**을 선택합니다. 사이트 바인딩 창에서 **추가**를 선택하고 다음 정보를 제출합니다.
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. 동일한 IP 주소에 바인드된 SSL을 사용하는 사이트가 여러 개 있는 경우 선택적으로 SNI(Server Name Indication)를 사용하도록 SSL 인증서를 구성합니다. **서버 이름 표시 요구** 상자를 선택합니다.
1. 이제 웹 사이트는 보안 연결을 허용하도록 구성됩니다.

## 오리진 인증서 취소
{:#cis-origin-certificates-revoke}

CIS 오리진 인증서를 삭제하십시오. 이 프로세스는 실행 취소할 수 없습니다.
