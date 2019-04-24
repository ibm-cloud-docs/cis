---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: API Specs, CIS APIs

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Especificaciones de API
{:#api-specs}

Aquí se muestra cómo ver las especificaciones de API de CIS: 

1. Para ver las API de CIS, vaya a la página [Documentos de API](/apidocs/). 

2. En el menú de navegación izquierdo, seleccione el recuadro Redes para filtrar las API.

3. Elija en la lista de las API disponibles de Cloud Internet Services.


## Notas
{:#api-notes}

1. Punto final de API: `https://api.cis.cloud.ibm.com`.

2. Se necesita la cabecera **X-Auth-User-Token** para cada llamada de API. Esta cabecera es la señal portadora para el usuario que se puede recuperar desde IAM (por ejemplo, utilizando el mandato `ibmcloud iam oauth-tokens`).

3. El campo **crn** es también necesario en la vía de acceso para cada llamada de API. Este campo contiene el Cloud Resource Name (CRN) completo para una instancia de recursos de CIS que se está configurando. (Por ejemplo, el CRN para una instancia de recursos se puede recuperar de su nombre utilizando el mandato `ibmcloud resource service-instance <instance-name>`). El CRN debe ser un URL codificado en la llamada de API.

4. Las llamadas de API están limitadas por la velocidad. Se puede realizar un total de 100 llamadas de API en 1 minuto. Si se supera esta tasa, se bloquean las entradas siguientes durante un periodo de tiempo.
