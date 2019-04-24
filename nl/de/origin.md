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

# Ursprungszertifikate
{:#cis-origin-certificates}

Ursprungszertifikate sind kostenlose TLS-Zertifikate, die von CIS ausgestellt wurden und den Datenverkehr zwischen Ihrem Ursprungsserver und Ihren Benutzern verschlüsseln. Bestellen Sie kostenlose TLS-Zertifikate, die auf Ihrem Ursprungsserver installiert werden sollen.

CIS-Ursprungszertifikate sind nur zur Verwendung in CIS gültig.
{:note}

## Ursprungszertifikat bestellen
{:#cis-origin-certificates-ordering}

Stellen Sie eine Zertifikatssignieranforderung (CSR, Certificate Signing Request) bereit oder wählen Sie einen privaten Schlüsseltyp für CIS aus, um einen Schlüssel und eine Zertifikatssignieranforderung zu generieren, damit Sie ein Ursprungszertifikat bestellen können. 

Geben Sie bis zu 100 Hostnamen (einschließlich Platzhalterzeichen) in Ihrem Ursprung an, den das Zertifikat schützt. Platzhalter bieten eine Stufe der Abdeckung. Verwenden Sie mehrere Platzhalter in demselben Zertifikat, um eine größere Abdeckung zu erzielen (zum Beispiel `*.yourdomain.com` und `*.yoursubdomain.yourdomain.com`). CIS-Ursprungszertifikate lassen keine IP-Adressen zu. 

Geben Sie ein Ablaufdatum an. Das Standardablaufdatum für Zertifikate ist in 15 Jahren. Das kürzeste Ablaufdatum ist in sieben Tagen. 

Der private Schlüssel ist sofort nach der Bestellung eines Zertifikats verfügbar, wenn der private Schlüssel und die CSR von CIS generiert wurden. 

## Ursprungszertifikat auf Ihrem Server installieren
{:#cis-origin-certificates-installing}

### Apache httpd
{:#cis-origin-certificates-installing-apache-httpd}
1. Bestellen Sie ein Ursprungszertifikat. 
1. Kopieren Sie den privaten Schlüssel und das Ursprungszertifikat im PEM-Format in separate Dateien in dem Verzeichnis auf Ihrem Server, in dem Sie die Schüssel- und Zertifikatsdateien speichern. 
1. Suchen Sie Ihre Apache-Konfigurationsdatei. Normalerweise lauten die Dateinamen `httpd.conf` oder `apache2.conf` und die Positionen sind `/etc/httpd/` oder `/etc/apache2/`. Ihre Konfigurationsdatei kann jedoch insbesondere dann variieren, wenn Sie eine besondere Schnittstelle zur Verwaltung Ihres Servers verwenden. Eine vollständige Liste der Standardinstallationslayouts finden Sie im Apache-[DistrosDefaultLayout](https://wiki.apache.org/httpd/DistrosDefaultLayout). Der folgende Befehl ist eine Möglichkeit, nach SSL-Konfigurationsdateien unter Linux zu suchen.
    ```
    grep -i -r "SSLCertificateFile" /etc/httpd/
    ```
1. Suchen Sie den Block <VirtualHost> für die Konfiguration. Kopieren Sie optional den vorhandenen, nicht gesicherten, virtuellen Host für Ihre Site, damit diese über HTTP und HTTPS verfügbar ist, weil jeder Verbindungstyp einen virtuellen Host erfordert. 
1. Konfigurieren Sie den Block <VirtualHost> für SSL. Das folgende Beispiel zeigt eine einfache Konfiguration für SSL. Verwenden Sie Dateinamen für Ihr Zertifikat und Ihren privaten Schlüssel. `SSLCertificateFile` ist Ihr Ursprungs-CA-Zertifikatsdateiname und `SSLCertificateKeyFile` ist der Dateinamen Ihres privaten Ursprungs-CA-Schlüssels.
```
    <VirtualHost 192.168.0.1:443>
      DocumentRoot             /var/www/html2
      ServerName               www.mydomain.com
      SSLEngine                on
      SSLCertificateFile       /path/to/your_domain_name.crt
      SSLCertificateKeyFile    /path/to/your_private.key
    </VirtualHost>
```
1. Testen Sie Ihre Konfiguration. Bevor Sie Apache erneut starten, sollten Sie überprüfen, dass Ihre Konfigurationsdateien fehlerfrei sind. Führen Sie den folgenden Befehl aus, um Ihre Konfiguration zu testen.
```
    apachectl configtest
```
1. Starten Sie Apache erneut. Führen Sie die folgenden Befehle aus, um Apache mit der SSL-Unterstützung erneut zu starten.
```
    apachectl stop
    apachectl start
    ```

Wenn die SSL-Unterstützung nicht mit `apache start` geladen wird, führen Sie den Befehl `apachectl startssl` aus. Wenn der Apache nur mit der SSL-Unterstützung unter Verwendung von `apachectl startssl` gestartet wird, wird empfohlen, die Apache-Startkonfiguration so anzupassen, dass die SSL-Unterstützung im Befehl `apachectl start` eingeschlossen wird. Andernfalls kann es im Falle eines Serverneustarts erforderlich sein, den Apache mit dem Befehl `apachectl startssl` manuell erneut zu starten. Dies umfasst in der Regel auch das Entfernen der Tags `<IfDefine SSL>` und `</IfDefine SSL>`, die Ihre Konfiguration einschließen.
{:note}

### NGINX
{:#cis-origin-certificates-installing-nginx}
1. Bestellen Sie ein Ursprungszertifikat. 
1. Kopieren Sie den privaten Schlüssel und das Ursprungszertifikat im PEM-Format in separate Dateien in dem Verzeichnis auf Ihrem Server, in dem Sie die Schüssel- und Zertifikatsdateien speichern. 
1. Aktualisieren Sie Ihre virtuelle NGINX-Hostdatei. Bearbeiten Sie die virtuelle NGINX-Hostdatei für Ihre Website. Das folgende Beispiel stellt einen Serverblock für die SSL-Unterstützung dar. Aktivieren Sie den Parameter `ssl` an Listen-Sockets im Serverblock für Ihre Site, damit diese über HTTP und HTTPS verfügbar ist.
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
1. Starten Sie NGINX erneut. Führen Sie einen der folgenden Befehle aus, um NGINX erneut zu starten.
```
    sudo /etc/init.d/nginx restart
    sudo systemctl restart nginx
    ```

### Apache Tomcat
{:#cis-origin-certificates-installing-apache-tomcat}
1. Bestellen Sie ein Ursprungszertifikat. 
1. Kopieren Sie den privaten Schlüssel und das Ursprungszertifikat im PKCS #7-Format (cert.p7b) in separate Dateien in dem Verzeichnis auf Ihrem Server, in dem Sie die Schüssel- und Zertifikatsdateien speichern. 

    Sie müssen die SSL-Zertifikatsdatei in demselben Keystore und unter demselben Aliasnamen (oder "Server") installieren, die für die Generierung Ihrer Zertifikatssignieranforderung (CSR) verwendet wurden. Die Installation im nächsten Schritt kann nicht ausgeführt werden, wenn die SSL-Zertifikatsdatei in einem anderen Keystore installiert ist. {:note}

1. Installieren Sie das Zertifikat. Führen Sie den folgenden Befehl aus, um die SSL-Zertifikatsdatei in Ihrem Keystore zu installieren.
```
    keytool -import -trustcacerts -alias server -file cert.p7b -keystore your_site_name.jks
    ```
    Es wird eine Bestätigungsnachricht angezeigt, die besagt, dass die Zertifikatsantwort im Keystore installiert wurde: **"Certificate reply was installed in keystore."** Auf die Frage, ob Sie dem Zertifikat vertrauen, geben Sie **j** oder **Ja** ein. Ihre Keystore-Datei (your_site_name.jks) kann jetzt auf Ihrem Tomcat-Server verwendet werden. 

1. Konfigurieren Sie Ihren SSL-Connector. Konfigurieren Sie einen SSL-Connector, damit Tomcat sichere Verbindungen akzeptieren kann. 
    1. Öffnen Sie die Tomcat-Datei 'server.xml' in einem Texteditor. Die Datei 'server.xml' befindet sich normalerweise im Ordner 'conf' des Ausgangsverzeichnisses von Tomcat. 
    1. Geben Sie den Anschluss an, der zum Sichern des neuen Keystores verwendet werden soll. In der Regel wird ein Anschluss an Port 443 oder 8443 verwendet. 
    1. Entfernen Sie alle Kommentartags (`<!--` and `-->`), die den Anschluss möglicherweise umgeben. 
    1. Aktualisieren Sie den richtigen Keystore-Dateinamen und das richtige Kennwort in der Connectorkonfiguration. Das folgende Beispiel zeigt einen konfigurierten SSL-Connectorblock.
```
    <Connector port="443" maxHttpHeaderSize="8192" maxThreads="150" 
    minSpareThreads="25" maxSpareThreads="75" enableLookups="false" 
    disableUploadTimeout="true" acceptCount="100" scheme="https" 
    secure="true" SSLEnabled="true" clientAuth="false" sslProtocol="TLS" 
    keyAlias="server" keystoreFile="/home/user_name/your_site_name.jks" 
    keystorePass="your_keystore_password" />
    ```
    Wenn Ihre Tomcat-Version unter Tomcat 7 ist, ändern Sie `keystorePass` in `keypass`.
    {:note}
1. Speichern Sie Ihre Datei 'server.xml'. 
1. Starten Sie Tomcat erneut.

### Microsoft-Internetinformationsdienste (IIS) 7.0
{:#cis-origin-certificates-installing-ms-iis7}
1. Erstellen Sie eine Zertifikatssignieranforderung (CSR, Create a Certificate Signing Request) in IIS-Manager und exportieren Sie sie als `.pem`. Der IIS-Manager befindet sich unter Verwaltungstools.
1. Bestellen Sie ein CIS-Ursprungszertifikat mit Ihrer CSR.
1. Kopieren Sie das Ursprungszertifikat auf den Desktop Ihres Servers. 
1. Öffnen Sie IIS-Manager und wählen Sie den Hostnamen Ihres Servers unter **Verbindungen** aus.
1. Wählen Sie **Serverzertifikate** im IIS-Abschnitt im Zentrumsmenü aus. 
1. Wählen Sie die Aktion **Zertifikatsanforderung abschließen** im Aktionsmenü aus. Klicken Sie auf der Seite **Antwort der Zertifizierungsstelle angeben** unter **Dateiname mit der Antwort der Zertifizierungsstelle** auf `...`, um zur Zertifikatsdatei `.cer` zu blättern, die auf das Desktop kopiert wurde. Wählen Sie die Datei aus und klicken Sie auf **Öffnen**.
1. Geben Sie einen aussagekräftigen Namen für das Zertifikat an. Der aussagekräftiger Name identifiziert das Zertifikat. 
1. Wählen Sie **OK** aus, um die Zertifikatsinstallation auf Ihrem Server abzuschließen. 
1. Binden Sie das Zertifikat an Ihre Website. Wählen Sie Ihre Website durch Erweitern der **Sites** unter dem Namen Ihres Servers im Menü unter **Verbindungen** im IIS-Manager aus. Wählen Sie **Bindungen** unter **Site bearbeiten** im Aktionsmenü aus. Wählen Sie im Fenster mit den Sitebindungen **Hinzufügen** aus und übergeben Sie die folgenden Informationen.
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. Ihre Website ist jetzt so konfiguriert, dass sie sichere Verbindungen akzeptiert. 

### Microsoft-Internetinformationsdienste (IIS) 8.0 und 8.5
{:#cis-origin-certificates-installing-ms-iis8-8.5}

1. Erstellen Sie eine Zertifikatssignieranforderung (CSR, Create a Certificate Signing Request) in IIS-Manager und exportieren Sie sie als `.pem`. Der IIS-Manager befindet sich unter Verwaltungstools.
1. Bestellen Sie ein CIS-Ursprungszertifikat mit Ihrer CSR.
1. Kopieren Sie das Ursprungszertifikat auf den Desktop Ihres Servers. 
1. Öffnen Sie IIS-Manager und wählen Sie den Hostnamen Ihres Servers unter **Verbindungen** aus.
1. Wählen Sie **Serverzertifikate** im IIS-Abschnitt im Zentrumsmenü aus. 
1. Wählen Sie die Aktion **Zertifikatsanforderung abschließen** im Aktionsmenü aus. Klicken Sie auf der Seite **Antwort der Zertifizierungsstelle angeben** unter **Dateiname mit der Antwort der Zertifizierungsstelle** auf `...`, um zur Zertifikatsdatei `.cer` zu blättern, die auf das Desktop kopiert wurde. Wählen Sie die Datei aus und klicken Sie auf **Öffnen**.
1. Geben Sie einen aussagekräftigen Namen für das Zertifikat an. Der aussagekräftiger Name identifiziert das Zertifikat. 
1. Wählen Sie **OK** aus, um die Zertifikatsinstallation auf Ihrem Server abzuschließen. 
1. Binden Sie das Zertifikat an Ihre Website. Wählen Sie Ihre Website durch Erweitern der **Sites** unter dem Namen Ihres Servers im Menü unter **Verbindungen** im IIS-Manager aus. Wählen Sie **Bindungen** unter **Site bearbeiten** im Aktionsmenü aus. Wählen Sie im Fenster mit den Sitebindungen **Hinzufügen** aus und übergeben Sie die folgenden Informationen.
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. Optional konfigurieren Sie Ihr SSL-Zertifikat für die Verwendung von SNI (Server Name Indication), wenn Sie über mehrere Sites verfügen, die über SSL an dieselbe IP-Adresse gebunden sind. Wählen Sie das Feld **SNI anfordern** aus. 
1. Ihre Website ist jetzt so konfiguriert, dass sie sichere Verbindungen akzeptiert. 

## Ursprungszertifikat widerrufen
{:#cis-origin-certificates-revoke}

Löschen Sie Ihr CIS-Ursprungszertifikat. Dieser Prozess kann nicht rückgängig gemacht werden. 
