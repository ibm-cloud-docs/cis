---

copyright:
  years: 2019
lastupdated: "2019-03-28"

keywords: resolve override, Cloud Object Storage, bucket resource

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Resolver sustitución con COS
{: #resolve-override-cos}

## Casos prácticos
{: #cos-use-cases}

Haga que la solicitud que coincida con la regla de página se resuelva en un recurso de contenedor de Cloud Object Storage (COS).


## Requisitos previos
{: #cos-prerequisites}

En los pasos siguientes se presupone que tiene una instancia de COS existente y un contenedor con acceso público. Para obtener información sobre el acceso público, consulte [Cómo permitir el acceso público](/docs/services/cloud-object-storage/iam?topic=cloud-object-storage-allowing-public-access).


## Cree pasos de regla de página
{: #cos-create-page-rule}

* Vaya a **Rendimiento->Reglas de página**.
* Pulse el botón **Crear regla**.
* Especifique el valor deseado para la coincidencia de URL. Por ejemplo, `*.foo.com/*`.
  * Tenga en cuenta que la coincidencia de URL debe coincidir con el nombre del objeto COS.
  * Por ejemplo, si tiene un objeto denominado reports.txt en el contenedor `my-bucket1`, estas dos coincidencias de URL serían válidas:
    * `*.foo.com/*`
    * `*.foo.com/reports.txt`
* Utilice el desplegable para seleccionar **Resolver sustitución con COS** en la sección **Rendimiento**.
* Utilice el desplegable **Instancia de Cloud Object Storage** para seleccionar la instancia deseada.
* Utilice el desplegable **Contenedor** para seleccionar el contenedor deseado.
* Para crear la regla de página, pulse el botón **Suministrar 1 recurso**.


## Explicación detallada de los conceptos
{: #cos-detail-concepts}

Al crear una regla de página **Resolver sustitución con COS**, CIS creará automáticamente los otros recursos necesarios para la integración en COS. Entre estos se incluye:

**CNAME**
* Un registro de DNS CNAME para `<bucket-name>.<cos-endpoint>` como `<bucket-name>`.
* Por ejemplo, si el dominio de CIS es `foo.com`, tiene un contenedor de COS denominado `images` y su punto final público de COS es `s3.us-west.objectstorage.uat.test.net` CIS creará un CNAME `images.foo.com` que apunte a `images.s3.us-west.objectstorage.uat.test.net`.
Si la regla de página Resolver sustitución con COS ya no es necesaria, el CNAME debe suprimirse manualmente junto con la regla de página.
{:note}

**Sustituir cabecera de host**
* El parámetro Sustituir cabecera de host sustituye la cabecera de host por el URI que coincide con la regla de página `<bucket-name>.<cos-endpoint>`.
* Utilizando el ejemplo anterior, el valor de Sustituir cabecera de host se establecerá en `images.s3.us-west.objectstorage.uat.test.net`.


## Supresión de la regla de página
{: #cos-delete-page-rule}

Si la regla de página Resolver sustitución con COS ya no es necesaria, el CNAME debe suprimirse _manualmente_ junto con la regla de página.


## Edición de la regla de página
{: #cos-edit-page-rule}

Después de editar la regla de página, **Resolver sustitución con COS** dejará de aparecer en la página. No obstante, **Resolver sustitución** `<bucket>.<domain>` y **Sustituir cabecera de host** `<bucket>.<cos-endpoint>` sustituirán a **Resolver sustitución con COS**.

Si se hacen cambios en **Resolver sustitución** _no_ creará automáticamente un nuevo registro CNAME (por ejemplo, `<updated-bucket>.<domain>`). Esto sólo se hace al crear inicialmente una regla de página que utiliza **Resolver sustitución con COS**. Para crear automáticamente el registro CNAME para el contenedor, siga los pasos de [Crear regla de página](#cos-create-page-rule).
