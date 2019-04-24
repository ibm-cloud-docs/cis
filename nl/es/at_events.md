---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM Cloud Internet Services, CIS Activity Tracker events

subcollection: cis

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Sucesos de {{site.data.keyword.cloudaccesstrailshort}} de CIS
{: #at_events}

Utilice el servicio {{site.data.keyword.cloudaccesstrailfull}} para realizar el seguimiento de cómo los usuarios y las aplicaciones interactúan con IBM Cloud Internet Services (CIS) en {{site.data.keyword.cloud}}.
{:shortdesc}

El servicio {{site.data.keyword.cloudaccesstrailfull_notm}} registra las actividades iniciadas por el usuario que cambian el estado de un servicio en {{site.data.keyword.cloud_notm}}. Para obtener más información, consulte [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla).




## Lista de sucesos: dominios DNS
{: #events_dns_domain}

En la tabla siguiente puede ver una lista de las acciones que están relacionadas con dominios DNS y que generan un suceso:

|Acción|Descripción|
|---|---|  
|internet-svcs.zones.create|Crear un dominio DNS.|
|internet-svcs.zones.update|Actualizar un dominio DNS.|
|internet-svcs.zones.delete|Suprimir un dominio DNS.|
|internet-svcs.zones.activation_check.update|Realizar la comprobación de activación de un dominio DNS.|
|internet-svcs.zones.dnssec.update|Habilitar o inhabilitar DNSSEC para un dominio DNS.|

## Lista de sucesos: registros DNS
{: #events_dns_record}

En la tabla siguiente puede ver una lista de las acciones que están relacionadas con registros DNS y que generan un suceso:

|Acción|Descripción|
|---|---|  
|internet-svcs.zones.dns_records.create|Crear un registro DNS.|
|internet-svcs.zones.dns_records.update|Actualizar un registro DNS.|
|internet-svcs.zones.dns_records.delete|Suprimir un registro DNS.|
|internet-svcs.zones.dns_records_bulk.create|Importar registros de DNS del archivo de zona.|


## Lista de sucesos: equilibradores de carga
{: #events_load_balancers}

En la tabla siguiente puede ver una lista de las acciones que están relacionadas con equilibradores de carga y que generan un suceso:

|Acción|Descripción|
|---|---|  
|internet-svcs.zones.load_balancers.create|Crear un equilibrador de carga global.|
|internet-svcs.zones.load_balancers.update|Actualizar un equilibrador de carga global.|
|internet-svcs.zones.load_balancers.delete|Suprimir un equilibrador de carga global.|
|internet-svcs.load_balancers.monitors.create|Crear un supervisor de estado.|
|internet-svcs.load_balancers.monitors.update|Actualizar un supervisor de estado.|
|internet-svcs.load_balancers.monitors.delete|Suprimir un supervisor de estado.|
|internet-svcs.load_balancers.pools.create|Cree una agrupación de equilibrador de carga global.|
|internet-svcs.load_balancers.pools.update|Actualizar una agrupación de equilibrador de carga global.|
|internet-svcs.load_balancers.pools.delete|Suprimir una agrupación de equilibrador de carga global.|


## Lista de sucesos: depuración de la memoria caché
{: #events_cache}

En la tabla siguiente puede ver una lista de las acciones que están relacionadas con la depuración de la memoria caché y que generan un suceso:

|Acción|Descripción|
|---|---|  
|internet-svcs.zones.purge_cache.purge_all.update|Purgar todos los activos almacenados en memoria caché de un dominio del servidor edge.|
|internet-svcs.zones.purge_cache.purge_by_urls.update|Purgar los activos almacenados en memoria caché por URL del servidor edge.|
|internet-svcs.zones.purge_cache.purge_by_cache_tags.update|Purgar los activos almacenados en memoria caché por etiquetas de memoria caché del servidor edge.|
|internet-svcs.zones.purge_cache.purge_by_hosts.update|Purgar los activos almacenados en memoria caché por nombres de host del servidor edge.|


## Lista de sucesos: reglas de página
{: #events_page_rules}

En la tabla siguiente puede ver una lista de las acciones que están relacionadas con reglas de página y que generan un suceso:

|Acción|Descripción|
|---|---|  
|internet-svcs.zones.pagerules.create|Crear una regla de página.|
|internet-svcs.zones.pagerules.update|Actualizar una regla de página.|
|internet-svcs.zones.pagerules.delete|Suprimir una regla de página.|


## Lista de sucesos: cortafuegos
{: #events_firewalls}

En la tabla siguiente puede ver una lista de las acciones que están relacionadas con cortafuegos y que generan un suceso:

|Acción|Descripción|
|---|---|  
|internet-svcs.zones.firewall.waf.packages.groups.update|Habilita o inhabilita un grupo de conjuntos de reglas WAF.|
|internet-svcs.zones.firewall.waf.packages.rules.update|Habilitar o inhabilitar una regla WAF.|
|internet-svcs.zones.firewall.access_rules.rules.create|Crear una regla de cortafuegos de IP a nivel de dominio.|
|internet-svcs.zones.firewall.access_rules.rules.update|Actualizar una regla de cortafuegos de IP a nivel de dominio.|
|internet-svcs.zones.firewall.access_rules.rules.delete|Suprimir una regla de cortafuegos de IP a nivel de dominio.|
|internet-svcs.firewall.access_rules.rules.create|Crear una regla de cortafuegos de IP a nivel de instancia.|
|internet-svcs.firewall.access_rules.rules.update|Actualizar una regla de cortafuegos de IP a nivel de instancia.|
|internet-svcs.firewall.access_rules.rules.delete|Suprimir una regla de cortafuegos de IP a nivel de instancia.|
|internet-svcs.zones.rate_limits.create|Crear una regla de limitación de velocidad.|
|internet-svcs.zones.rate_limits.update|Actualizar una regla de limitación de velocidad.|
|internet-svcs.zones.rate_limits.delete|Suprimir una regla de limitación de velocidad.|
|internet-svcs.zones.ua_rules.create|Crear una regla de bloqueo de agente de usuario.|
|internet-svcs.zones.ua_rules.update|Actualizar una regla de bloqueo de agente de usuario.|
|internet-svcs.zones.ua_rules.delete|Suprimir una regla de bloqueo de agente de usuario.|
|internet-svcs.zones.firewall.lockdowns.create|Crear una regla de bloqueo de dominio.|
|internet-svcs.zones.firewall.lockdowns.update|Actualizar una regla de bloqueo de dominio.|
|internet-svcs.zones.firewall.lockdowns.delete|Suprimir una regla de bloqueo de dominio.|

## Lista de sucesos: direccionamiento
{: #events_routing}

En la tabla siguiente puede ver una lista de las acciones que están relacionadas con el direccionamiento y que generan un suceso:

|Acción|Descripción|
|---|---|  
|internet-svcs.zones.routing.smart_routing.update	|Habilitar o inhabilitar el direccionamiento inteligente.|
|internet-svcs.zones.routing.tiered_caching.update	|Habilitar o inhabilitar el almacenamiento en memoria caché en niveles.|

## Lista de sucesos: paquetes de certificados
{: #events_certificate_packs}

En la tabla siguiente puede ver una lista de las acciones que están relacionadas con paquetes de certificados y que generan un suceso:

|Acción|Descripción|
|---|---|  
|internet-svcs.zones.ssl.certificate_packs.create|Solicitar un certificado dedicado.|
|internet-svcs.zones.ssl.certificate_packs.delete|Suprimir un certificado dedicado.|


## Lista de sucesos: certificados personalizados
{: #events_custom_certificate}

En la tabla siguiente puede ver una lista de las acciones que están relacionadas con certificados personalizados y que generan un suceso:

|Acción|Descripción|
|---|---|  
|internet-svcs.zones.custom_certificates.create|Cargar un certificado personalizado.|
|internet-svcs.zones.custom_certificates.update|Actualizar un certificado personalizado.|
|internet-svcs.zones.custom_certificates.delete|Suprimir un certificado personalizado.|


## Lista de sucesos: valores
{: #events_settings}

En la tabla siguiente puede ver una lista de las acciones que están relacionadas con la configuración de valores y que generan un suceso:

|Acción|Descripción|
|---|---|  
|internet-svcs.zones.settings.cache_level.update|Cambiar el nivel de almacenamiento en memoria caché.|
|internet-svcs.zones.settings.browser_cache_ttl.update|Cambiar el TTL de la memoria caché del navegador.|
|internet-svcs.zones.settings.development_mode.update|Habilitar o inhabilitar la modalidad de desarrollo.|
|internet-svcs.zones.settings.security_level.update|Cambiar el nivel de seguridad.|
|internet-svcs.zones.settings.ssl.update|Cambiar el valor de SSL.|
|internet-svcs.zones.settings.tls_1_2_only.update|Habilitar o inhabilitar el soporte de TLS 1.2.|
|internet-svcs.zones.settings.waf.update|Habilitar o inhabilitar el cortafuegos de aplicaciones web.|
|internet-svcs.zones.settings.cname_flattening.update|Cambiar el valor de simplificación de CNAME.|
|internet-svcs.zones.settings.always_online.update|Habilitar o inhabilitar Servir contenido obsoleto para el dominio.|
|internet-svcs.zones.settings.sort_query_string_for_cache.update|Habilitar o inhabilitar ordenación de argumentos de consulta al consultar contenido en la memoria caché.|
|internet-svcs.zones.settings.tls_1_3.update|Cambiar el valor de TLS 1.3.|
|internet-svcs.zones.settings.automatic_https_rewrites.update|Habilitar o inhabilitar las reescrituras HTTPS automáticas.
|internet-svcs.zones.settings.opportunistic_encryption.update|Habilitar o inhabilitar el cifrado oportunista.|


## Dónde buscar los sucesos
{: #ui}

Los sucesos de {{site.data.keyword.cloudaccesstrailshort}} están disponibles en el **dominio de la cuenta** de {{site.data.keyword.cloudaccesstrailshort}} disponible en la región de {{site.data.keyword.cloud_notm}} donde se han generado los sucesos.



## Información adicional
{: #info}

Si al supervisar lo sucesos de {{site.data.keyword.cloudaccesstrailshort}} generados por IBM Cloud Internet Services (CIS) identifica una solicitud de API para la que necesita información adicional, consulte el campo requestData del suceso. Abra una incidencia de soporte e incluya el valor del campo **X-CORRELATION-ID**, disponible en requestData.
