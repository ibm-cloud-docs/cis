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

# Certificados de origen
{:#cis-origin-certificates}

Los certificados de origen son certificados TLS libres emitidos por CIS que cifran el tráfico entre el servidor de origen y los usuarios. Solicite certificados TLS gratuitos para instalarlos en su servidor de origen.

Los certificados de origen de CIS sólo son válidos para utilizar en CIS.
{:note}

## Solicitud de un certificado de origen
{:#cis-origin-certificates-ordering}

Para solicitar un certificado de origen, haga una Solicitud de firma de certificado (CSR) o seleccione un tipo de clave privada para que CIS genere una clave y una CSR.

Especifique un máximo de 100 nombres de host (incluyendo comodines) en el origen que protege el certificado. Los comodines sólo proporcionan un nivel de cobertura. Utilice varios comodines en el mismo certificado para una cobertura más amplia (por ejemplo, `*.yourdomain.com` y `*.yoursubdomain.yourdomain.com`). Los certificados de origen de CIS no permiten direcciones IP.

Especifique la caducidad. La caducidad predeterminada de un certificado es de 15 años. La caducidad más corta es de siete días.

La clave privada sólo estará disponible inmediatamente después de solicitar un certificado si la clave privada y la CSR las ha generado CIS.

## Instalación de un certificado de origen en el servidor
{:#cis-origin-certificates-installing}

### Apache httpd
{:#cis-origin-certificates-installing-apache-httpd}
1. Solicite un certificado de origen.
1. Copie la clave privada y el certificado de origen en formato PEM en archivos separados en el directorio del servidor donde guarda los archivos de claves y de certificado.
1. Localice el archivo de configuración de Apache. Por lo general, los nombres de archivo son `httpd.conf` o `apache2.conf` y las ubicaciones son `/etc/httpd/` o `/etc/apache2/`. Sin embargo, el archivo de configuración puede variar, especialmente si se utiliza una interfaz especial para gestionar el servidor. Consulte la publicación [DistrosDefaultLayout](https://wiki.apache.org/httpd/DistrosDefaultLayout) de Apache para obtener una lista completa de los diseños de instalación predeterminados. El mandato siguiente es una forma de buscar el archivo de configuración SSL en linux. 
    ```
    grep -i -r "SSLCertificateFile" /etc/httpd/
    ```
1. Localice el bloque <VirtualHost> a configurar. Opcionalmente, copie el host virtual no seguro existente para que el sitio esté disponible a través de HTTP y de HTTPS, ya que cada tipo de conexión requiere un host virtual.
1. Configure el bloque <VirtualHost> para SSL. En el ejemplo siguiente se representa una configuración sencilla para SSL. Utilice los nombres de archivo del certificado y la clave privada. `SSLCertificateFile` es el nombre de archivo de certificado de su OriginCA y `SSLCertificateKeyFile` es el nombre de archivo de clave privada de su OriginCA.
    ```
    <VirtualHost 192.168.0.1:443>
      DocumentRoot             /var/www/html2
      ServerName               www.mydomain.com
      SSLEngine                on
      SSLCertificateFile       /path/to/your_domain_name.crt
      SSLCertificateKeyFile    /path/to/your_private.key
    </VirtualHost>
    ```
1. Pruebe la configuración. Antes de reiniciar Apache, verifique que no haya errores en los archivos de configuración. Ejecute el mandato siguiente para probar la configuración.
    ```
    apachectl configtest
    ```
1. Reinicie Apache. Ejecute los mandatos siguientes para reiniciar Apache con soporte de SSL.
    ```
    apachectl stop
    apachectl start
    ```

Si el soporte de SSL no se carga con `apache start`, ejecute el mandato `apachectl startssl`. Si Apache sólo se inicia con el soporte de SSL utilizando `apachectl startssl`, se recomienda ajustar la configuración de inicio de Apache para incluir el soporte SSL en el mandato `apachectl start`. De lo contrario, en caso de reinicio del servidor, es posible que se necesite reiniciar manualmente Apache utilizando `apachectl startssl`. Esto normalmente implica eliminar las etiquetas `<IfDefine SSL>` y `</IfDefine SSL>` que abren y cierran la configuración.
{:note}

### NGINX
{:#cis-origin-certificates-installing-nginx}
1. Solicite un certificado de origen.
1. Copie la clave privada y el certificado de origen en formato PEM en archivos separados en el directorio del servidor donde guarda los archivos de claves y de certificado.
1. Actualice el archivo de hosts virtuales NGINX. Edite el archivo de host virtual NGINX para el sitio web. En el ejemplo siguiente se representa un bloque de servidor para el soporte SSL. Habilite el parámetro `ssl` en los sockets de escucha en el bloque de servidor para que el sitio esté disponible a través de HTTP y HTTPS.
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
1. Reinicie NGINX. Ejecute uno de los mandatos siguientes para reiniciar NGINX.
    ```
    sudo /etc/init.d/nginx restart
    sudo systemctl restart nginx
    ```

### Apache Tomcat
{:#cis-origin-certificates-installing-apache-tomcat}
1. Solicite un certificado de origen.
1. Copie la clave privada y el certificado de origen en formato PKCS #7 format (cert.p7b) en archivos separados en el directorio del servidor donde guarda los archivos de claves y de certificado.

    Debe instalar el archivo de certificado SSL en el mismo almacén de claves y bajo el mismo nombre de alias (o, "servidor") que ha utilizado para generar la solicitud de firma de certificado (CSR). La instalación en el paso siguiente no funcionará si el archivo de certificado SSL está instalado en otro almacén de claves.
    {:note}

1. Instale el certificado. Ejecute el mandato siguiente para instalar el archivo de certificado SSL en el almacén de claves.
    ```
    keytool -import -trustcacerts -alias server -file cert.p7b -keystore your_site_name.jks
    ```
    Habrá un mensaje de confirmación: **"La respuesta de certificado se ha instalado en el almacén de claves."** Especifique **y** o **yes** si se le solicita que confíe en el certificado. El archivo de almacén de claves (your_site_name.jks) está ahora listo para ser utilizado en el servidor Tomcat.

1. Configure el conector SSL. Configure un conector SSL para que Tomcat pueda aceptar conexiones seguras.
    1. Abra el archivo server.xml de Tomcat en un editor de texto. El archivo server.xml se encuentra normalmente en la carpeta conf del directorio de inicio de Tomcat.
    1. Identifique el conector a utilizar para proteger el nuevo almacén de claves. Generalmente se utiliza un conector con el puerto 443 u 8443.
    1. Elimine cualquier etiqueta de comentario (`<!--` and `-->`) que pueda haber alrededor del conector.
    1. Actualice el nombre de archivo de almacén de claves y la contraseña correctos en la configuración del conector.
    En el ejemplo siguiente se representa un bloque de conector SSL configurado.
    ```
    <Connector port="443" maxHttpHeaderSize="8192" maxThreads="150" 
    minSpareThreads="25" maxSpareThreads="75" enableLookups="false" 
    disableUploadTimeout="true" acceptCount="100" scheme="https" 
    secure="true" SSLEnabled="true" clientAuth="false" sslProtocol="TLS" 
    keyAlias="server" keystoreFile="/home/user_name/your_site_name.jks" 
    keystorePass="your_keystore_password" />
    ```
    Si la versión de Tomcat es anterior a Tomcat 7, cambie `keystorePass` a `keypass`.
    {:note}
1. Guarde el archivo server.xml.
1. Reinicie Tomcat.

### Microsoft Internet Information Services (IIS) 7.0
{:#cis-origin-certificates-installing-ms-iis7}
1. Cree una solicitud de firma de certificado (CSR) en el gestor de IIS y expórtelo como `.pem`. El Gestor de IIS se encuentra en Herramientas administrativas.
1. Solicite un certificado de origen de CIS utilizando su CSR.
1. Copie el certificado de origen en el escritorio del servidor.
1. Abra Administrador de IIS y seleccione el nombre de host del servidor en **Conexiones**.
1. Seleccione **Certificados de servidor** en la sección de IIS, en el menú central.
1. Seleccione la acción **Completar solicitud de certificado** en el menú Acciones. En la página **Especificar respuesta de entidad emisora de certificados**, en **Nombre de archivo que contiene la respuesta de la entidad certificadora**, pulse `...` para examinar el archivo de certificado `.cer` que se ha copiado en el escritorio, seleccione el archivo y pulse **Abrir**.
1. Especifique un nombre descriptivo para el certificado. El nombre descriptivo identifica el certificado.
1. Seleccione **Aceptar** para finalizar la instalación del certificado en el servidor.
1. Enlace el certificado a su sitio web. Seleccione su sitio web expandiendo **Sitios** debajo del nombre del servidor, en el menú, en **Conexiones** en el Gestor de IIS. Seleccione **Enlaces** en **Editar sitio**, en el menú Acciones. Seleccione **Añadir** en la ventana Enlaces de sitio y envíe la información siguiente.
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. Su sitio web está ahora configurado para aceptar conexiones seguras.

### Microsoft Internet Information Services (IIS) 8.0 y 8.5
{:#cis-origin-certificates-installing-ms-iis8-8.5}

1. Cree una solicitud de firma de certificado (CSR) en el gestor de IIS y expórtelo como `.pem`. El Gestor de IIS se encuentra en Herramientas administrativas.
1. Solicite un certificado de origen de CIS utilizando su CSR.
1. Copie el certificado de origen en el escritorio del servidor.
1. Abra Administrador de IIS y seleccione el nombre de host del servidor en **Conexiones**.
1. Seleccione **Certificados de servidor** en la sección de IIS, en el menú central.
1. Seleccione la acción **Completar solicitud de certificado** en el menú Acciones. En la página **Especificar respuesta de entidad emisora de certificados**, en **Nombre de archivo que contiene la respuesta de la entidad certificadora**, pulse `...` para examinar el archivo de certificado `.cer` que se ha copiado en el escritorio, seleccione el archivo y pulse **Abrir**.
1. Especifique un nombre descriptivo para el certificado. El nombre descriptivo identifica el certificado.
1. Seleccione **Aceptar** para finalizar la instalación del certificado en el servidor.
1. Enlace el certificado a su sitio web. Seleccione su sitio web expandiendo **Sitios** debajo del nombre del servidor, en el menú, en **Conexiones** en el Gestor de IIS. Seleccione **Enlaces** en **Editar sitio**, en el menú Acciones. Seleccione **Añadir** en la ventana Enlaces de sitio y envíe la información siguiente.
    ```
    Type              https
    IP Address        All Unassigned
    Port              443
    SSL Certificate   your_cert_friendly_name
    ```
1. Opcionalmente, configure el certificado SSL para utilizar la Indicación de nombre de servidor (SNI - Server Name Indication) si tiene varios sitios utilizando SSL enlazado a la misma dirección IP.  Seleccionar el recuadro **Requerir indicación de nombre de servidor**.
1. Su sitio web está ahora configurado para aceptar conexiones seguras.

## Revocar un certificado de origen
{:#cis-origin-certificates-revoke}

Suprima el certificado de origen de CIS. Este proceso no se puede deshacer.
