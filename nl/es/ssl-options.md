---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: TLS Options, secure connection, Automatic HTTPS

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Opciones de TLS
{:#cis-tls-options}

Las opciones de TLS le permiten controlar si los visitantes pueden examinar el sitio web sobre una conexión segura, y cuando lo hagan, cómo se conectará CIS a su servidor de origen.

## Reescritura automática de HTTPS
{:#automatic-https-rewrite}

La reescritura automática de HTTPS ayudan a arreglar contenido mixto cambiando “http” a “https” para todos los recursos o enlaces en su sitio web que se pueden servir con HTTPS. Este valor se encuentra en la página **Avanzado** de la configuración de seguridad.

## Modalidades de cifrado TLS
{:#tls-encryption-modes}

Estas opciones están listadas en el orden de menos seguras (Desactivado) a más seguras (Firmado por una entidad emisora de certificados de extremo a extremo). 
 * Desactivado (no recomendado)
 * Cliente a extremo (extremo a origen no cifrado, los certificados autofirmados no están admitidos) 
 * Extremo a extremo flexible (los certificados de extremo a origen pueden ser autofirmados) 
 * Firmado por una entidad emisora de certificados de extremo a extremo (valor predeterminado y recomendado)
 * Extracción de origen sólo HTTPS (sólo Empresa)

### Desactivado 
{:#tls-encryption-modes-off}
No hay ninguna conexión segura entre el visitante y CIS, y no hay ninguna conexión segura entre CIS y el servidor web. Los visitantes solo pueden ver el sitio web mediante HTTP, y cualquier visitante que intente conectarse utilizando HTTPS recibirá un `HTTP 301 Redirect` en la versión HTTP sin formato del sitio web.

### Cliente a extremo
{:#tls-encryption-modes-client-to-edge}

Una conexión segura entre el visitante y CIS, pero ninguna conexión segura entre CIS y el servidor web. No es necesario tener un certificado TLS en el servidor web, pero sus visitantes seguirán viendo el sitio como habilitado para HTTPS. Esta opción no está recomendada si tiene cualquier información confidencial en el sitio web. Este valor solo funcionará para el puerto 443 al 80. Solo debería utilizarse como último recurso si no puede configurar TLS en su propio servidor web. Es _menos seguro_ que cualquier otra opción (incluso “Desactivado”), y podría causar problemas cuando decida cambiar fuera de ella.

### Extremo a extremo flexible
{:#tls-encryption-modes-end-to-end-flexible}

Una conexión segura entre el visitante y CIS, y una conexión segura (pero no autenticada) entre CIS y el servidor web. Debe tener el servidor configurado para responder a conexiones HTTPS, con al menos un certificado firmado automáticamente. La autenticidad del certificado no está verificada: desde el punto de vista de CIS (cuando conectamos a su servidor web de origen), es el equivalente de ignorar este mensaje de error. Mientras que la dirección del servidor web de origen sea correcta en los valores de DNS, sabrá que estamos conectando al servidor web, y no alguna otra persona.

### Firmado por una entidad emisora de certificados de extremo a extremo
{:#tls-encryption-modes-end-to-end-ca-signed}

Valor predeterminado y recomendado. Una conexión segura entre el visitante y CIS, y una conexión segura y autenticada entre CIS y el servidor web. Debe tener el servidor configurado para responder a conexiones HTTPS, con un certificado TLS válido. Este certificado debe estar firmado por una entidad emisora de certificados, tener una fecha de caducidad en el futuro, y responder al nombre de dominio de la solicitud (nombre de host). Le recomendamos que siga utilizando este modo TLS para unas mejores prácticas de seguridad, a menos que entienda las amenazas de seguridad potenciales de cambiar a uno de los modos menos estrictos.

### Extracción de origen de sólo HTTPS
{:#tls-encryption-modes-origin-only-pull}

*Sólo Empresa.* Esta modalidad tiene los mismos requisitos de certificado que la modalidad Firmado por una entidad emisora de certificados de extremo a extremo, y también actualiza todas las conexiones entre CIS y el servidor web de origen de HTTP a HTTPS, incluso si el contenido original solicitado es sobre HTTP.

## Versión de TLS mínima
{:#minimum-tls-version}

Esto establece la versión de TLS mínima para el tráfico que intenta conectarse a su sitio. De forma predeterminada, está definido en 1,0. Las versiones de TLS más altas proporcionan seguridad adicional, pero es posible que no estén soportadas por todos los navegadores. Esto podría dar como resultado que algunos clientes no puedan conectarse a su sitio.
