---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIDR blocks, Whitelist Block Challenge, IBM Cloud Internet Services, security features

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Cómo IBM Cloud Internet Services (CIS) mantiene su trabajo seguro
{:#how-cis-keeps-your-work-secure}

IBM CIS es un servicio en la nube distribuido globalmente que bloquea las amenazas y limita los bots y los rastreadores abusivos, que pueden hacer perder el ancho de banda y los recursos del servidor. IBM CIS funciona como un proxy inverso HTTP(S) global y un proveedor de servicios DNS gestionado. El tráfico web se direcciona mediante nuestra red global inteligente para optimizar el rendimiento y la seguridad.

![security-graphic.png](images/security-graphic.png)

Aquí hay una visión general de características rápida:

## Características de seguridad
{:#cis-security-features}

 * Puede redirigir los [registros DNS](/docs/infrastructure/cis?topic=cis-dns-concepts#proxying-dns-records) o los [GLB](/docs/infrastructure/cis?topic=cis-global-load-balancer-glb-concepts) para utilizar las características de seguridad. Esto permite que el tráfico fluya a través de nuestros servidores y poder supervisar los datos.
### Cortafuegos de aplicaciones web (WAF)
{:#cis-web-application-firewall}

 * WAF se implementa a través de dos conjuntos de reglas: [OWASP](/docs/infrastructure/cis?topic=cis-owasp-rule-set-for-waf) y [CIS](/docs/infrastructure/cis?topic=cis-waf-settings#cis-rule-set-for-waf).
### Mitigación de DDoS ilimitado
{:#cis-unlimited-ddos-mitigation}

 * La mitigación de DDoS es normalmente un servicio costoso que puede crecer en costo cuando es atacado. Con CIS, se incluye la mitigación ilimitada de DDoS sin ningún coste adicional.

## Estándares de seguridad y plataforma
{:#security-standards-and-platform}

 * TLS (SHA2 y SHA1)
 * IPv6
 * HTTP/2 y SPDY

## DNS
{:#cis-dns}

 * Red anycast global
 * DNSSEC

## Ataques de red y mitigación
{:#network-attacks-and-mitigation}

Generalmente, vemos ataques que están en dos categorías

| Ataques de Capa 3 o de Capa 4 | Ataques de Capa 7 |
|------------------------------|-----------------|
|Estos ataques consisten en un desbordamiento de tráfico en ISO Capa 3 (la capa de red), como los desbordamientos de ICMP) o en la Capa 4 (la capa de transporte), como por ejemplo los desbordamientos de TCP SYN o los desbordamientos UDP reflejados) |Estos son ataques que envían solicitudes de ISO Capa 7 maliciosas (la capa de aplicación), como por ejemplo desbordamientos GET.  |
| Se ha bloqueado automáticamente en nuestros límites | Los manejamos con “Modalidad de defensa”, WAF, y los Valores de nivel de seguridad |

## Cortafuegos de IP
{:#cis-ip-firewall}

IBM Cloud Internet Services le ofrece varias herramientas para controlar el tráfico y permitirle proteger los dominios, los URL y los directorios de volúmenes de tráfico, de determinados grupos de solicitantes y, en particular, de las IP solicitantes. En esta sección se detallan las herramientas disponibles.

### Reglas de IP
{:#cis-ip-rules}

Las reglas de IP le permiten controlar el acceso a direcciones IP específicas, rangos de IP, países específicos, ASN específicos y ciertos bloques CIDR. Las acciones disponibles en las solicitudes entrantes son:
  * Lista blanca 
  * Bloqueo 
  * Desafío (Captcha) 
  * Desafío JavaScript(desafío IUAM)

Por ejemplo, si observa que una IP determinada está causando solicitudes maliciosas, puede bloquear ese usuario por dirección IP.

### Reglas de bloqueo de agente de usuario
{:#user-agent-blocking-rules}

Las reglas de bloqueo de agente de usuario le permiten llevar a cabo una acción en cualquier serie de agente de usuario que seleccione. Esta funcionalidad funciona como el Bloqueo de dominio que se ha descrito anteriormente, con la diferencia de que en el bloqueo se examina la serie de entrada del de agente de usuario en lugar de la IP. Puede elegir cómo manejar una solicitud coincidente con la misma lista de acciones que ha establecido en las reglas de IP (Bloqueo, Desafío y Desafío JS). Tenga presente que el bloqueo del agente de usuario se aplica a toda la zona. No se pueden especificar subdominios de la misma forma que se pueden especificar bloqueos de dominio.

Esta herramienta es útil para bloquear cualquier serie de agente de usuario que considere sospechosa. 

### Bloqueo de dominio
{:#cis-domain-lockdown}

El bloqueo de dominio le permite incluir en una lista blanca algunas direcciones IP específicas y algunos rangos de IP de forma que cualquier otra IP se considere en la lista negra. El bloqueo de dominio admite:

  * Subdominios específicos. Por ejemplo, puede permitir el acceso de la IP `1.2.3.4` al dominio `foo.example.com` y permitir el acceso de la IP `5.6.7.8` al dominio `bar.example.com`, sin permitir necesariamente lo contrario.
  * URL específicos. Por ejemplo, puede permitir el acceso de la IP `1.2.3.4` al directorio `example.com/foo/*` y de la IP `5.6.7.8`  al directorio `example.com/bar/*`, pero no necesariamente permitir lo contrario.
Esta funcionalidad resulta útil cuando necesita más granularidad en las reglas de acceso porque, con las reglas de IP, puede aplicar el bloqueo a todos los subdominios del dominio actual, o a todos los dominios de la cuenta, y no puede especificar URI.

### Superación del desafío
{:#cis-challenge-passage}

Este parámetro, que se encuentra en los valores de seguridad **Avanzados**, le permite control durante cuánto tiempo un visitante que ha superado un desafío o un desafío JavaScript puede tener acceso al sitio hasta presentarle un nuevo desafío. Esto se basa en la IP del visitante y, por lo tanto, no se aplica a los desafíos presentados por las reglas WAF, ya que se basan en una acción que el usuario realiza en el sitio.

### Comprobación de integridad del navegador
{:#cis-browser-integrity-check}

Este parámetro se encuentra en los valores de seguridad **Avanzados**. La comprobación de integridad del navegador busca cabeceras HTTP de las que normalmente abusan los emisores de spam. Deniega el acceso del tráfico con dichas cabeceras a su página. También bloquea o presenta un desafío a los visitantes que no tienen un agente de usuario, o que añadan un agente de usuario no estándar (esta táctica la utilizan normalmente los bots, los rastreadores o las API de abuso).
