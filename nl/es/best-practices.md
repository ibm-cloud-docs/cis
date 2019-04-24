---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Best practices, CIS setup

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Mejores prácticas para la configuración de CIS
{:#best-practices-for-cis-setup}

Dado que IBM CIS está posicionado en el borde de la red, deberá realizar algunos pasos para garantizar una integración fluida con los servicios de CIS. Estas son algunas de las mejores prácticas recomendadas para integrar CIS con sus servidores de origen. 

Puede realizar estos pasos antes o después de cambiar su DNS y de activar nuestro servicio de proxy. Estas recomendaciones permiten a IBM CIS conectarse a sus servidores de origen correctamente. Le ayudarán a evitar problemas con el tráfico de la API o HTTPS, y ayudarán a sus registros a capturar las direcciones IP correctas de sus clientes, en lugar de las direcciones IP de CIS de protección.

Esto es lo que necesitará configurar:

 * Mejor práctica 1: Restaurar las IP de origen de sus clientes
 * Mejor práctica 2: Incorporar direcciones IP de CIS
 * Mejor práctica 3: Asegurarse de que la configuración de seguridad no interfiera con el tráfico de la API
 * Mejor práctica 4: Configurar los valores de seguridad tan estrictamente como sea posible
 
## Mejor práctica 1: Saber cómo restaurar las IP de origen de sus clientes
{:#best-practice-know-how-to-restore-origininating-ip}

Como proxy inverso, proporcionamos la IP de origen en estas cabeceras:

  * `CF-Connecting-IP`
  * `X-Forwarded-For`
  * `True-Client-IP` (opcional)

Puede restaurar las direcciones IP de usuario utilizando una variedad de herramientas, para infraestructuras como Apache, Windows IIS y NGINX.

## Mejor práctica 2: Incorporar direcciones IP de CIS para facilitar la integración
{:#best-practice-incorporate-cis-ip-addresses}

Estos son los dos pasos que se realizarán:

  * Eliminar cualquier limitación de velocidad de direcciones IP de CIS
  * Configurar los ACL para permitir solo direcciones IP de CIS y otras partes de confianza

Puede encontrar la lista actualizada de rangos de IP para IBM CIS [en esta ubicación](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses).

## Mejor práctica 3: Revisar la configuración de seguridad para asegurarse de que no interfiera con el tráfico de API
{:#best-practice-review-security-settings-interference}

IBM CIS normalmente acelera el tráfico de API eliminando la sobrecarga de conexión. Sin embargo, la postura de seguridad predeterminada puede interferir con muchas llamadas de API. Le recomendamos realizar algunas acciones para evitar la interferencia con el tráfico de API una vez que el proceso mediante proxy esté activo.

 * Desactive la configuración de seguridad de forma selectiva, utilizando las características **Reglas de página**.
   * Cree una Regla de página con el patrón de URL de la API, como `api.example.com`
   * Añada los siguientes comportamientos de reglas:
     * Seleccione **Nivel de seguridad** en **Esencialmente desactivado**
     * Seleccione **TLS** en **Desactivado**
     * Seleccione **Comprobación de seguridad del navegador** en **Desactivado**
   * Seleccione **Suministro de recursos**

 * Como alternativa, puede desactivar **Cortafuegos de aplicaciones web** globalmente desde la página Seguridad.

| *¿Qué hace la Comprobación de integridad del navegador?* | 
|------------------------------------------------|
| *La comprobación de integridad del navegador busca cabeceras HTTP de las que normalmente abusan los emisores de spam. Deniega el acceso del tráfico con dichas cabeceras a su página. También bloquea a los visitantes que no tienen un agente de usuario, o que añadan un agente de usuario no estándar (esta táctica la utilizan normalmente los bots, los rastreadores o las API de abuso).* |

## Mejor práctica 4: Configurar los valores de seguridad tan estrictamente como sea posible
{:#best-practice-configure-stict-security-settings}

CIS proporciona algunas opciones para cifrar el tráfico. Como proxy inverso, cerraremos las conexiones TLS a sus centros de datos y abriremos una nueva conexión TLS a sus servidores de origen. Para su terminación con CIS, puede cargar un certificado personalizado de su cuenta, puede utilizar un certificado comodín proporcionado para usted mediante CIS, o ambos.

### Carga de un certificado personalizado
{:#strict-upload-custom-cert}
 
Puede cargar su clave pública y privada al crear un dominio Enterprise. Si carga su propio certificado, obtendrá compatibilidad inmediata con tráfico cifrado, y mantendrá el control sobre su certificado (por ejemplo, un certificado Validación ampliada (EV)). Recuerde que será responsable de gestionar el certificado si carga un certificado personalizado. Por ejemplo, IBM CIS no realizará el seguimiento de las fechas de caducidad del certificado. 
 
### Como alternativa, utilice un certificado suministrado por CIS
{:#strict-utilize-cert-cis-provisioned}
 
IBM CIS ha colaborado con varias entidades emisoras de certificados (CAs) para proporcionar certificados comodín de dominio para nuestros clientes, de forma predeterminada. Podría ser necesaria la verificación manual para configurar estos certificados, y su equipo de soporte puede ayudarle a realizar estos pasos adicionales.
 
### Cambie el valor de TLS a **Firmado por una entidad emisora de certificados de extremo a extremo**
{:#strict-change-tls-setting}
 
La mayoría de nuestros clientes Enterprise utilizan la configuración de seguridad Firmado por una entidad emisora de certificados de extremo a extremo. Un valor **Firmado por una entidad emisora de certificados de extremo a extremo** requiere un certificado firmado por una entidad emisora de certificados válido instalado en el servidor web. La fecha de caducidad del certificado debe estar en el futuro, y debe tener una coincidencia de *nombre de host* o de *SAN (Subject Alternative Name)*.

