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

# Certificats d'origine
{:#cis-origin-certificates}

Les certificats d'origine sont des certificats TLS gratuits émis par CIS qui chiffrent le trafic entre votre serveur d'origine et vos utilisateurs. Commandez des certificats TLS gratuits à installer sur votre serveur d'origine.

Les certificats d'origine CIS ne sont valables que pour une utilisation dans CIS.
{:note}

## Commande d'un certificat d'origine 
{:#cis-origin-certificates-ordering}

Pour commander un certificat d'origine, fournissez une Demande de signature de certificat (CSR) ou sélectionnez un type de clé privée pour CIS afin de générer une clé et une CSR. 

Spécifiez jusqu'à 100 noms d'hôte (y compris les caractères génériques) de votre origine protégée par le certificat. Les caractères génériques ne fournissent qu'un niveau de protection. Utilisez plusieurs caractères génériques sur le même certificat pour élargir la couverture (par exemple, `*.yourdomain.com` et `*.yoursubdomain.yourdomain.com`). Les certificats d'origine CIS n'autorisent pas les adresses IP. 

Spécifiez le délai d'expiration. Le délai d'expiration du certificat par défaut est de 15 ans. Le délai d'expiration le plus court est de sept jours. 

La clé privée ne sera disponible immédiatement après la commande d'un certificat que si la clé privée et la demande CSR ont été générées par CIS. 

## Installation d'un certificat d'origine sur votre serveur 
{:#cis-origin-certificates-installing}

### Apache httpd
{:#cis-origin-certificates-installing-apache-httpd}
1. Commandez un certificat d'origine. 
1. Copiez la clé privée et le certificat d'origine au format PEM dans des fichiers distincts, dans le répertoire de votre serveur où vous conservez les fichiers de clé et de certificat. 
1. Localisez votre fichier de configuration Apache. Généralement, les noms de fichier sont `httpd.conf` ou `apache2.conf` et les emplacements sont `/etc/httpd/` ou `/etc/apache2/`. Toutefois, votre fichier de configuration peut varier, notamment si vous utilisez une interface spéciale pour gérer votre serveur. Reportez-vous à la section [DistrosDefaultLayout](https://wiki.apache.org/httpd/DistrosDefaultLayout) d'Apache pour obtenir une liste complète des dispositions d'installation par défaut. La commande suivante permet de rechercher le fichier de configuration SSL sur linux.

```
    grep -i -r "SSLCertificateFile" /etc/httpd/
    ```
1. Localisez le bloc <VirtualHost> à configurer. Si vous le souhaitez, copiez l'hôte virtuel non sécurisé existant pour que votre site soit disponible via HTTP et HTTPS, car chaque type de connexion nécessite un hôte virtuel. 
1. Configurez le bloc <VirtualHost> pour SSL. L'exemple suivant représente une configuration simple pour SSL. Utilisez les noms de fichier pour votre certificat et votre clé privée. `SSLCertificateFile` est votre nom de fichier de certificat OriginCA et `SSLCertificateKeyFile` est votre nom de fichier de clé privée OriginCA.
    ```
    <VirtualHost 192.168.0.1:443>
      DocumentRoot             /var/www/html2
      ServerName               www.mydomain.com
      SSLEngine                on
      SSLCertificateFile       /path/to/your_domain_name.crt
      SSLCertificateKeyFile    /path/to/your_private.key
    </VirtualHost>
    ```
1. Testez votre configuration. Avant de redémarrer Apache, vérifiez qu'il n'y a pas d'erreur dans vos fichiers de configuration. Exécutez la commande suivante pour tester votre configuration.
    ```
    apachectl configtest
    ```
1. Redémarrez Apache. Exécutez les commandes suivantes pour redémarrer Apache avec la prise en charge de SSL.
```
    apachectl stop
    apachectl start
    ```

Si la prise en charge de SSL ne se charge pas avec `apache start`, exécutez la commande `apachectl startssl`. Si Apache ne démarre qu'avec une prise en charge SSL à l'aide d'`apachectl startssl`, il est recommandé d'ajuster la configuration de démarrage d'Apache pour inclure la prise en charge de SSL dans la commande `apachectl start`. Faute de quoi, en cas de redémarrage du serveur, vous devrez peut-être redémarrer manuellement Apache à l'aide de `apachectl startssl`. Cela implique généralement la suppression des balises `<IfDefine SSL>` et `</IfDefine SSL>` qui renferment votre configuration.
{:note}

### NGINX
{:#cis-origin-certificates-installing-nginx}
1. Commandez un certificat d'origine. 
1. Copiez la clé privée et le certificat d'origine au format PEM dans des fichiers distincts, dans le répertoire de votre serveur où vous conservez les fichiers de clé et de certificat. 
1. Mettez à jour votre fichier d'hôtes virtuels NGINX. Modifiez le fichier d’hôte virtuel NGINX pour votre site Web. L'exemple suivant représente un bloc serveur pour la prise en charge de SSL. Activez le paramètre `ssl` sur les sockets d’écoute du bloc serveur afin que votre site soit disponible via HTTP et HTTPS.
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
1. Redémarrez NGINX. Exécutez l’une des commandes suivantes pour redémarrer NGINX.
```
    sudo /etc/init.d/nginx restart
    sudo systemctl restart nginx
    ```

### Apache Tomcat
{:#cis-origin-certificates-installing-apache-tomcat}
1. Commandez un certificat d'origine. 
1. Copiez la clé privée et le certificat d'origine au format PKCS #7 (cert.p7b) dans des fichiers distincts, dans le répertoire de votre serveur où vous conservez les fichiers de clé et de certificat. 

    Vous devez installer le fichier de certificat SSL dans le même magasin de clés et sous le nom d'alias (ou "serveur") utilisé pour générer votre Demande de signature de certificat (CSR). L'installation à l'étape suivante ne fonctionnera pas si le fichier de certificat SSL est installé dans un magasin de clés différent.
    {:note}

1. Installez le certificat. Exécutez la commande suivante pour installer le fichier de certificat SSL sur votre magasin de clés.
    ```
    keytool -import -trustcacerts -alias server -file cert.p7b -keystore your_site_name.jks
    ```
    Un message de confirmation apparaît : **"Certificate reply was installed in keystore."** Entrez **y** or **yes** si vous êtes invité à faire confiance au certificat. Votre fichier de clés (your_site_name.jks) est maintenant prêt à être utilisé sur votre serveur Tomcat. 

1. Configurez votre connecteur SSL. Configurez un connecteur SSL pour que Tomcat puisse accepter les connexions sécurisées. 
    1. Ouvrez le fichier server.xml de Tomcat dans un éditeur de texte. Le fichier server.xml se trouve généralement dans le dossier conf du répertoire de base de Tomcat. 
    1. Identifiez le connecteur à utiliser pour sécuriser le nouveau magasin de clés. Un connecteur avec le port 443 ou 8443 est généralement utilisé. 
    1. Supprimez les balises de commentaire (`<!--` and `-->`) pouvant entourer le connecteur. 
    1. Mettez à jour le nom de fichier et le mot de passe du fichier de clés dans la configuration du connecteur.
    L'exemple suivant représente un bloc de connecteur SSL configuré.
```
    <Connector port="443" maxHttpHeaderSize="8192" maxThreads="150" 
    minSpareThreads="25" maxSpareThreads="75" enableLookups="false" 
    disableUploadTimeout="true" acceptCount="100" scheme="https" 
    secure="true" SSLEnabled="true" clientAuth="false" sslProtocol="TLS" 
    keyAlias="server" keystoreFile="/home/user_name/your_site_name.jks" 
    keystorePass="your_keystore_password" />
    ```
    Si votre version de Tomcat est antérieure à Tomcat 7, remplacez `keystorePass` par `keypass`.
    {:note}
1. Enregistrez votre fichier server.xml.
1. Redémarrez Tomcat.

### Microsoft Internet Information Services (IIS) 7.0
{:#cis-origin-certificates-installing-ms-iis7}
1. Créez une Demande de signature de certificat (CSR) dans le Gestionnaire des services Internet (IIS) et exportez-la au format `.pem`. Le Gestionnaire des services Internet (IIS) se trouve sous Outils d'administration. 
1. Commandez un certificat d'origine CIS à l'aide de votre demande CSR. 
1. Copiez le certificat d'origine sur le bureau de votre serveur. 
1. Ouvrez le Gestionnaire des services Internet (IIS) et sélectionnez le nom d’hôte de votre serveur sous **Connexions**.
1. Sélectionnez **Certificats de serveur** dans la section IIS du menu central.
1. Sélectionnez l'action **Terminer la demande de certificat** dans le menu Actions. Dans la page **Indiquer la réponse de l'autorité de certification** sous **Nom du fichier comportant la réponse de l'autorité de certification**, cliquez sur `...` pour rechercher le fichier de certificat `.cer` copié sur le bureau, sélectionnez le fichier, puis cliquez sur **Ouvrir**.
1. Entrez un nom convivial pour le certificat. Le nom convivial identifie le certificat. 
1. Sélectionnez **OK** pour terminer l'installation du certificat sur votre serveur. 
1. Liez le certificat à votre site Web. Sélectionnez votre site Web en développant **Sites** sous le nom de votre serveur dans le menu sous **Connexions** dans le Gestionnaire des services Internet (IIS). Sélectionnez **Liaisons** sous **Modifier le site ** dans le menu Actions. Sélectionnez **Ajouter** dans la fenêtre Liaisons de sites et soumettez les informations suivantes.
    ```
    Type              https
    Adresse IP        Toutes non attribuées
    Port              443
    Certificat SSL    nom_cert_convivial
    ```
1. Votre site Web est maintenant configuré pour accepter les connexions sécurisées. 

### Microsoft Internet Information Services (IIS) 8.0 et 8.5
{:#cis-origin-certificates-installing-ms-iis8-8.5}

1. Créez une Demande de signature de certificat (CSR) dans le Gestionnaire des services Internet (IIS) et exportez-la au format `.pem`. Le Gestionnaire des services Internet (IIS) se trouve sous Outils d'administration. 
1. Commandez un certificat d'origine CIS à l'aide de votre demande CSR. 
1. Copiez le certificat d'origine sur le bureau de votre serveur. 
1. Ouvrez le Gestionnaire des services Internet (IIS) et sélectionnez le nom d’hôte de votre serveur sous **Connexions**.
1. Sélectionnez **Certificats de serveur** dans la section IIS du menu central.
1. Sélectionnez l'action **Terminer la demande de certificat** dans le menu Actions. Dans la page **Indiquer la réponse de l'autorité de certification** sous **Nom du fichier comportant la réponse de l'autorité de certification**, cliquez sur `...` pour rechercher le fichier de certificat `.cer` copié sur le bureau, sélectionnez le fichier, puis cliquez sur **Ouvrir**.
1. Entrez un nom convivial pour le certificat. Le nom convivial identifie le certificat. 
1. Sélectionnez **OK** pour terminer l'installation du certificat sur votre serveur. 
1. Liez le certificat à votre site Web. Sélectionnez votre site Web en développant **Sites** sous le nom de votre serveur dans le menu sous **Connexions** dans le Gestionnaire des services Internet (IIS). Sélectionnez **Liaisons** sous **Modifier le site ** dans le menu Actions. Sélectionnez **Ajouter** dans la fenêtre Liaisons de sites et soumettez les informations suivantes.
    ```
    Type              https
    Adresse IP        Toutes non attribuées
    Port              443
    Certificat SSL    nom_cert_convivial
    ```
1. Configurez éventuellement votre certificat SSL pour utiliser une indication SNI (Server Name Indication) si plusieurs sites utilisant SSL sont liés à la même adresse IP. Cochez la case **Exiger l'indication de nom du serveur**.
1. Votre site Web est maintenant configuré pour accepter les connexions sécurisées. 

## Révocation d'un certificat d'origine 
{:#cis-origin-certificates-revoke}

Supprimez votre certificat d'origine CIS. Ce processus est irréversible.
