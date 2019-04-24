---

copyright:
  years: 2018
lastupdated: "2018-03-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Especificaciones de API

Aquí se muestra cómo ver las especificaciones de API de CIS: 

1. Para ver API de CIS, vaya a la página [Especificación de API de CIS](https://console.bluemix.net/apidocs/2640-cloud-internet-services). 

2. En el menú de navegación izquierdo, seleccione entre la lista de API disponibles.


## Notas

1. Punto final de API: https://api.cis.cloud.ibm.com.

2. La cabecera **X-Auth-User-Token** es necesaria para cada llamada de API. Esta es la señal portadora para el usuario que se puede recuperar desde IAM (por ejemplo, utilizando el mandato "bx iam oauth-tokens").

3. El campo **crn** es también necesario en la vía de acceso para cada llamada de API. Este es el Cloud Resource Name (CRN) completo para una instancia de recursos de CIS que se está configurando (por ejemplo, el CRN para una instancia de recursos se puede recuperar de su nombre utilizando el mandato "bx resource service-instance <instance-name>"). El CRN debe ser un URL codificado en la llamada de API.

4. Las llamadas de API están limitadas por la velocidad. Se puede realizar un total de 100 llamadas de API en 1 minuto. Si se supera esta tasa, se bloquearán las entradas siguientes durante un periodo de tiempo.
