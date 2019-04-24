---

copyright:
  years: 2019
lastupdated: "2019-03-28"

keywords: Cloudant database, CORS, cross-origin resource sharing, host header

subcollection: cis

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"} 
{:note: .note}


# Acceda a su base de datos Cloudant a través de IBM Cloud Internet Services
{: #access-cloudant-through-cis}

Siga estos pasos para acceder a la base de datos Cloudant a través de IBM Cloud Internet Services (CIS).

## Antes de empezar
{: #access-cloudant-through-cis-begin}

Estas instrucciones presuponen que ya ha añadido un dominio a CIS tal como se describe en la página [Cómo empezar](/docs/infrastructure/cis?topic=cis-getting-started-with-ibm-cloud-internet-services-cis-).

### Paso 1: Añada su dominio de CIS al Intercambio de recursos de origen cruzado (CORS)
{: #access-cloudant-through-cis-step1}

* Vaya a la base de datos Cloudant y abra la página `Acccount` -> `CORS`.
* Añada su dominio de CIS al campo de entrada de dominios de origen. Por ejemplo, `https://cloudant.test.foo.com`.

### Paso 2. Configure CIS para que apunte a la base de datos Cloudant
{: #access-cloudant-through-cis-step2}

* Vaya al panel de control de CIS y cree un equilibrador de carga o un registro de DNS que apunte al nombre de host de su base de datos Cloudant. Por ejemplo, `https://cloudant.test.foo.com` -> `111-222-333-444-555-test.cloudant.com`.
* Habilite `proxy` para el registro de DNS o el equilibrador de carga.


### Paso 3. Cree una regla de página para establecer Host Header Override (sustitución de cabecera de host)
{: #access-cloudant-through-cis-step3}

* En el panel de instrumentos de CIS, vaya a `Performance` -> `Page Rules`.
* Cree una regla de página para el URL deseado, por ejemplo, `https://cloudant.test.foo.com/*`.
* Seleccione el valor de Comportamiento de regla `Host Header Override`.
* Defínala con el nombre de host de la base de datos Cloudant, por ejemplo `111-222-333-444-555-test.cloudant.com`.

Para obtener más información sobre Cloudant, consulte la [documentación de Cloudant](/docs/services/Cloudant?topic=cloudant-getting-started-with-cloudant).
