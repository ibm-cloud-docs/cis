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

# Resolve Override with COS
{: #resolve-override-cos}

## Casi di utilizzo
{: #cos-use-cases}

Metti in corrispondenza la richiesta con la regola della pagina Resolve in una risorsa bucket COS (Cloud Object Storage). 


## Prerequisiti
{: #cos-prerequisites}

I seguenti passi presuppongono che tu abbia un'istanza COS esistente e un bucket con accesso pubblico. Per informazioni sull'accesso pubblico, vedi [Consentire l'accesso pubblico](/docs/services/cloud-object-storage/iam?topic=cloud-object-storage-allowing-public-access).


## Passi di creazione della regola della pagina
{: #cos-create-page-rule}

* Passa a **Performance->Page Rules**.
* Fai clic sul pulsante **Create rule**.
* Immetti il valore desiderato per la corrispondenza dell'URL. Ad esempio, `*.foo.com/*`.
  * Tieni presente che la corrispondenza dell'URL deve corrispondere al tuo nome oggetto COS. 
  * Ad esempio, se hai un oggetto denominato reports.txt nel bucket `my-bucket1`, devono essere valide entrambe le corrispondenze dell'URL riportate di seguito: 
    * `*.foo.com/*`
    * `*.foo.com/reports.txt`
* Utilizza l'elenco a discesa per selezionare **Resolve Override with COS** nella sezione **Performance**. 
* Utilizza l'elenco a discesa **Cloud Object Storage Instance** per selezionare l'istanza desiderata. 
* Utilizza l'elenco a discesa **Bucket** per selezionare il bucket desiderato.
* Per creare la regola della pagina, fai clic sul pulsante **Provision 1 Resource**. 


## Spiegazione dettagliata dei concetti
{: #cos-detail-concepts}

Quando crei una regola della pagina **Resolve Override with COS**, CIS creerà automaticamente le altre risorse necessarie per l'integrazione COS. Queste includono:

**CNAME**
* Un record DNS CNAME per `<bucket-name>.<cos-endpoint>` come `<bucket-name>`.
* Ad esempio, se il tuo dominio CIS è `foo.com`, hai un bucket COS denominato `images` e il tuo endpoint COS pubblico è `s3.us-west.objectstorage.uat.test.net`, CIS creerà un CNAME `images.foo.com` che punta a `images.s3.us-west.objectstorage.uat.test.net`.
Se la regola della pagina Resolve Override with COS non è più necessaria, CNAME deve essere eliminato manualmente insieme alla regola della pagina.
{:note}

**Host Header Override**
* L'impostazione Host Header Override sostituirà l'intestazione host per l'URI che corrisponde alla regola della pagina in `<bucket-name>.<cos-endpoint>`.
* Utilizzando l'esempio precedente, il valore di Host Header Override verrà impostato su `images.s3.us-west.objectstorage.uat.test.net`.


## Eliminazione della regola della pagina
{: #cos-delete-page-rule}

Se la regola della pagina Resolve Override with COS non è più necessaria, CNAME deve essere eliminato _manualmente_ insieme alla regola della pagina.


## Modifica della regola della pagina
{: #cos-edit-page-rule}

Una volta modificata la regola della pagina, **Resolve Override with COS** non verrà più visualizzato nella pagina. Tuttavia, **Resolve Override** `<bucket>.<domain>` e **Host Header Override** `<bucket>.<cos-endpoint>` sostituiranno **Resolve Override with COS**.

Apportare modifiche a **Resolve Override** _non_ creerà automaticamente un nuovo record CNAME (ad esempio, `<updated-bucket>.<domain>`). Questa operazione viene effettuata solo dopo la creazione iniziale di una regola della pagina utilizzando **Resolve Override with COS**. Per creare automaticamente il record CNAME per il bucket, segui i passi di [creazione della regola della pagina](#cos-create-page-rule).
