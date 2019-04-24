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

# Certificati di origine
{:#cis-origin-certificates}

I certificati di origine sono certificati TLS gratuiti emessi da CIS che codificano il traffico tra il tuo server di origine e i tuoi utenti. Ordina certificati TLS gratuiti da installare sul tuo server di origine. 

I certificati di origine CIS sono validi solo per l'utilizzo in CIS.
{:note}

## Ordinazione di un certificato di origine
{:#cis-origin-certificates-ordering}

Per ordinare un certificato di origine, fornisci una richiesta di firma del certificato (CSR) oppure seleziona un tipo di chiave privata affinché CIS generi una chiave e una CSR.

Specifica massimo 100 nomi host (inclusi i caratteri jolly) nella tua origine protetta dal certificato. I caratteri jolly forniscono solo un livello di copertura. Utilizza più caratteri jolly nello stesso certificato per una copertura più ampia (ad esempio, `*.yourdomain.com` e `*.yoursubdomain.yourdomain.com`). I certificati di origine CIS non consentono indirizzi IP. 

Specifica la scadenza. La scadenza predefinita del certificato è 15 anni. La scadenza più breve è sette giorni. 

La chiave privata sarà disponibile solo subito dopo aver ordinato un certificato se la chiave privata e CSR sono state generate da CIS.

## Installazione di un certificato di origine sul tuo server
{:#cis-origin-certificates-installing}

### Apache httpd
{:#cis-origin-certificates-installing-apache-httpd}
1. Ordina un certificato di origine.
1. Copia la chiave privata e il certificato di origine nel formato PEM in file separati nella directory sul tuo server in cui conservi la chiave e i file certificato.
1. Individua il tuo file di configurazione Apache. Di norma, i nomi file sono `httpd.conf` o `apache2.conf` e le ubicazioni sono `/etc/httpd/` o `/etc/apache2/`. Tuttavia, il tuo file di configurazione può essere diverso, specialmente se utilizzi un'interfaccia speciale per gestire il tuo server. Fai riferimento a [DistrosDefaultLayout](https://wiki.apache.org/httpd/DistrosDefaultLayout) di Apache per un elenco completo dei layout di installazione predefiniti. Il seguente comando è un modo per ricercare il file di configurazione SSL su linux.
    ```
    grep -i -r "SSLCertificateFile" /etc/httpd/
    ```
1. Individua il blocco <VirtualHost> da configurare. Facoltativamente, copia l'host virtuale non sicuro esistente affinché il tuo sito sia disponibile tramite HTTP e HTTPS poiché ciascun tipo di connessione richiede un host virtuale.
1. Configura il blocco <VirtualHost> per SSL. Il seguente esempio rappresenta una configurazione semplice per SSL. Utilizza i nomi file relativi al tuo certificato e alla tua chiave privata. `SSLCertificateFile` è il nome file del tuo certificato OriginCA e `SSLCertificateKeyFile` è il nome file della tua chiave privata OriginCA.
    ```
    <VirtualHost 192.168.0.1:443>
      DocumentRoot             /var/www/html2
      ServerName               www.mydomain.com
      SSLEngine                on
      SSLCertificateFile       /path/to/your_domain_name.crt
      SSLCertificateKeyFile    /path/to/your_private.key
    </VirtualHost>
    ```
1. Verifica la tua configurazione. Prima di riavviare Apache, verifica che non ci siano errori nei file di configurazione. Esegui il seguente comando per verificare la tua configurazione.
    ```
    apachectl configtest
    ```
1. Riavvia Apache. Esegui i seguenti comandi per riavviare Apache con il supporto SSL.
    ```
    apachectl stop
    apachectl start
    ```

Se il supporto SSL non viene caricato con `apache start`, esegui il comando `apachectl startssl`. Se Apache si avvia solo con il supporto SSL utilizzando `apachectl startssl`, ti consigliamo di modificare la configurazione di avvio di Apache in modo che includa il supporto SSL nel comando `apachectl start`. In caso contrario, in caso di riavvio del server, potresti dover riavviare manualmente Apache utilizzando `apachectl startssl`. Di norma, questo implica l'eliminazione delle tag `<IfDefine SSL>` e `</IfDefine SSL>` che racchiudono la tua configurazione.
{:note}

### NGINX
{:#cis-origin-certificates-installing-nginx}
1. Ordina un certificato di origine.
1. Copia la chiave privata e il certificato di origine nel formato PEM in file separati nella directory sul tuo server in cui conservi la chiave e i file certificato.
1. Aggiorna il tuo file degli host virtuali NGINX. Modifica il file dell'host virtuale NGINX per il tuo sito web. Il seguente esempio rappresenta un blocco di server per il supporto SSL. Abilita il parametro `ssl` sui socket in ascolto nel blocco di server affinché il tuo sito sia disponibile tramite HTTP e HTTPS.
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
1. Riavvia NGINX. Esegui uno dei seguenti comandi per riavviare NGINX.
    ```
    sudo /etc/init.d/nginx restart
    sudo systemctl restart nginx
    ```

### Apache Tomcat
{:#cis-origin-certificates-installing-apache-tomcat}
1. Ordina un certificato di origine.
1. Copia la chiave privata e il certificato di origine nel formato PKCS #7 (cert.p7b) in file separati nella directory sul tuo server dove conservi la chiave e i file certificato. 

    Devi installare il file certificato SSL nello stesso keystore e sotto lo stesso nome alias (o "server") che hai utilizzato per generare la tua richiesta di firma del certificato (CSR). Il passo successivo dell'installazione non funzionerà se il file certificato SSL viene installato in un keystore diverso.
    {:note}

1. Installa il certificato. Esegui il seguente comando per installare il file certificato SSL nel tuo keystore.
    ```
    keytool -import -trustcacerts -alias server -file cert.p7b -keystore your_site_name.jks
    ```
    Verrà visualizzato un messaggio di conferma: **"Certificate reply was installed in keystore."** Immetti **y** o **yes** se ti viene chiesto di rendere attendibile il certificato. Il tuo file keystore (your_site_name.jks) è ora pronto per essere utilizzato sul tuo server Tomcat.

1. Configura il tuo connettore SSL. Configura un connettore SSL affinché Tomcat sia in grado di accettare le connessioni sicure. 
    1. Apri il file server.xml di Tomcat in un editor di testo. Di norma, il file server.xml si trova nella cartella conf della directory home del tuo Tomcat. 
    1. Identifica il connettore da utilizzare per proteggere il nuovo keystore. Di norma viene utilizzato un connettore con la porta 443 o 8443.
    1. Rimuovi le tag di commento (`<!--` and `-->`) che potrebbero racchiudere il connettore. 
    1. Aggiorna il nome file keystore corretto e la password nella configurazione del tuo connettore.
    Il seguente esempio rappresenta un blocco connettore SSL configurato.
    ```
    <Connector port="443" maxHttpHeaderSize="8192" maxThreads="150" 
    minSpareThreads="25" maxSpareThreads="75" enableLookups="false" 
    disableUploadTimeout="true" acceptCount="100" scheme="https" 
    secure="true" SSLEnabled="true" clientAuth="false" sslProtocol="TLS" 
    keyAlias="server" keystoreFile="/home/user_name/your_site_name.jks" 
    keystorePass="your_keystore_password" />
    ```
    Se la versione del tuo Tomcat è precedente a Tomcat 7, modifica `keystorePass` con `keypass`.
    {:note}
1. Salva il tuo file server.xml.
1. Riavvia Tomcat.

### Microsoft Internet Information Services (IIS) 7.0
{:#cis-origin-certificates-installing-ms-iis7}
1. Crea una richiesta di firma del certificato (CSR) in IIS Manager ed esportala come `.pem`. IIS Manager si trova in Administrative Tools.
1. Ordina un certificato di origine CIS utilizzando la tua CSR.
1. Copia il certificato di origine sul desktop del tuo server.
1. Apri IIS Manager e seleziona il nome host del tuo server in **Connections**.
1. Seleziona **Server Certificates** dalla sezione IIS nel menu centrale. 
1. Seleziona l'azione **Complete Certificate Request** dal menu Actions. Nella pagina **Specify Certificate Authority Response** in **File name containing the certification authority's response**, fai clic `...` per passare al file certificato `.cer` che è stato copiato sul desktop, seleziona il file e fai clic su **Open**.
1. Immetti un nome descrittivo per il certificato. Il nome descrittivo identifica il certificato.
1. Seleziona **OK** per completare l'installazione del certificato nel tuo server.
1. Collega il certificato al tuo sito web. Seleziona il tuo sito web espandendo **Sites** sotto il nome del tuo server nel menu in **Connections** in IIS Manager. Seleziona **Bindings** in **Edit Site** dal menu Actions. Seleziona **Add** dalla finestra Site Bindings e inoltra le seguenti informazioni.
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. Ora il tuo sito web è configurato per accettare connessioni sicure. 

### Microsoft Internet Information Services (IIS) 8.0 e 8.5
{:#cis-origin-certificates-installing-ms-iis8-8.5}

1. Crea una richiesta di firma del certificato (CSR) in IIS Manager ed esportala come `.pem`. IIS Manager si trova in Administrative Tools.
1. Ordina un certificato di origine CIS utilizzando la tua CSR.
1. Copia il certificato di origine sul desktop del tuo server.
1. Apri IIS Manager e seleziona il nome host del tuo server in **Connections**.
1. Seleziona **Server Certificates** dalla sezione IIS nel menu centrale. 
1. Seleziona l'azione **Complete Certificate Request** dal menu Actions. Nella pagina **Specify Certificate Authority Response** in **File name containing the certification authority's response**, fai clic `...` per passare al file certificato `.cer` che è stato copiato sul desktop, seleziona il file e fai clic su **Open**.
1. Immetti un nome descrittivo per il certificato. Il nome descrittivo identifica il certificato.
1. Seleziona **OK** per completare l'installazione del certificato nel tuo server.
1. Collega il certificato al tuo sito web. Seleziona il tuo sito web espandendo **Sites** sotto il nome del tuo server nel menu in **Connections** in IIS Manager. Seleziona **Bindings** in **Edit Site** dal menu Actions. Seleziona **Add** dalla finestra Site Bindings e inoltra le seguenti informazioni.
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. Facoltativamente, configura il tuo certificato SSL per utilizzare SNI (Server Name Indication) se hai più siti che utilizzano SSL collegato allo stesso indirizzo IP. Seleziona la casella **Require Server Name Indication**.
1. Ora il tuo sito web è configurato per accettare connessioni sicure. 

## Revoca di un certificato di origine
{:#cis-origin-certificates-revoke}

Elimina il tuo certificato di origine CIS. Questo processo non può essere annullato. 
