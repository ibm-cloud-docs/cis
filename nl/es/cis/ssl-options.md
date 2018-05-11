---
copyright:
  years: 2018
lastupdated: "2018-02-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Opciones de TLS
Las opciones de TLS le permiten controlar si los visitantes pueden examinar el sitio web sobre una conexión segura, y cuando lo hagan, cómo se conectará CIS a su servidor de origen.

Estas opciones están listadas en el orden de menos seguras (Desactivado) a más seguras (Firmado por una entidad emisora de certificados de extremo a extremo). 

Modalidades de cifrado TLS:

 * Desactivado (no recomendado)
 * Cliente a extremo (extremo a origen no cifrado, los certificados autofirmados no están admitidos) 
 * Extremo a extremo flexible (el extremo a Certificados de origen puede ser firmado automáticamente) 
 * Firmado por una entidad emisora de certificados de extremo a extremo (recomendado)

## Desactivado 
No hay ninguna conexión segura entre el visitante y CIS, y no hay ninguna conexión segura entre CIS y el servidor web. Los visitantes solo pueden ver el sitio web mediante HTTP, y cualquier visitante que intente conectarse utilizando HTTPS recibirá un `HTTP 301 Redirect` en la versión HTTP sin formato del sitio web.

## Cliente a extremo
Una conexión segura entre el visitante y CIS, pero ninguna conexión segura entre CIS y el servidor web. No es necesario tener un certificado TLS en el servidor web, pero sus visitantes seguirán viendo el sitio como habilitado para HTTPS. Esta opción no está recomendada si tiene cualquier información confidencial en el sitio web. Este valor solo funcionará para el puerto 443 al 80. Solo debería utilizarse como último recurso si no puede configurar TLS en su propio servidor web. Es _menos seguro_ que cualquier otra opción (incluso “Desactivado”), y podría causar problemas cuando decida cambiar fuera de ella.

## Extremo a extremo flexible
Una conexión segura entre el visitante y CIS, y una conexión segura (pero no autenticada) entre CIS y el servidor web. Deberá tener el servidor configurado para responder a conexiones HTTPS, con al menos un certificado firmado automáticamente. La autenticidad del certificado no está verificada: desde el punto de vista de CIS (cuando conectamos a su servidor web de origen), es el equivalente de ignorar este mensaje de error. Mientras que la dirección del servidor web de origen sea correcta en los valores de DNS, sabrá que estamos conectando al servidor web, y no alguna otra persona.

## Firmado por una entidad emisora de certificados de extremo a extremo
Recomendado. Una conexión segura entre el visitante y CIS, y una conexión segura y autenticada entre CIS y el servidor web. Deberá tener el servidor configurado para responder a conexiones HTTPS, con un certificado TLS válido. Este certificado debe estar firmado por una entidad emisora de certificados, tener una fecha de caducidad en el futuro, y responder al nombre de dominio de la solicitud (nombre de host).
