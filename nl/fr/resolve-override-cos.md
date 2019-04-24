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

# Outrepasser la résolution avec COS
{: #resolve-override-cos}

## Cas d'utilisation
{: #cos-use-cases}

Définissez la demande correspondant à la résolution de la règle de page en une ressource de compartiment Cloud Object Storage (COS). 


## Conditions préalables
{: #cos-prerequisites}

Les étapes suivantes supposent que vous disposez d'une instance COS existante et d'un compartiment avec un accès public. Pour plus d'informations sur l'accès public, reportez-vous à [Allowing public access](/docs/services/cloud-object-storage/iam?topic=cloud-object-storage-allowing-public-access).


## Etapes de création de règle de page 
{: #cos-create-page-rule}

* Accédez à **Performances->Règles de page**.
* Cliquez sur le bouton **Créer une règle**.
* Entrez la valeur souhaitée pour la correspondance d'URL. Par exemple, `*.foo.com/*`.
  * Notez que la correspondance d'URL doit correspondre à votre nom d'objet COS. 
  * Par exemple, si un objet appelé reports.txt se trouve sous le compartiment `my-bucket1`, ces deux correspondances d'URL sont valides :
    * `*.foo.com/*`
    * `*.foo.com/reports.txt`
* Utilisez le menu déroulant pour sélectionner **Outrepasser la résolution avec COS** dans la section **Performances**.
* Utilisez la liste déroulante **Instances Cloud Object Storage** pour sélectionner l'instance souhaitée.
* Utilisez la liste déroulante **Compartiment** pour sélectionner le compartiment souhaité.
* Pour créer la règle de page, cliquez sur le bouton **Provisionner 1 ressource**.


## Explication détaillée des concepts 
{: #cos-detail-concepts}

Lors de la création d'une règle de page **Outrepasser la résolution avec COS**, CIS crée automatiquement les autres ressources nécessaires à l'intégration de COS. Celles-ci incluent :

**CNAME**
* Un enregistrement DNS CNAME pour `<bucket-name>.<cos-endpoint>` en tant que `<bucket-name>`.
* Par exemple, si votre domaine CIS est `foo.com`, un compartiment COS est appelé `images` et le noeud final COS public est `s3.us-west.objectstorage.uat.test.net`, CIS crée un CNAME au format `images.foo.com` qui pointe vers `images.s3.us-west.objectstorage.uat.test.net`.
Si la règle de page Outrepasser la résolution avec COS n'est plus nécessaire, vous devez supprimer manuellement CNAME et la règle de page. {:note}

**Outrepasser l'en-tête d'hôte**
* Le paramètre Outrepasser l'en-tête d'hôte remplace l'en-tête de l'hôte pour l'URI correspondant à la règle de page par `<bucket-name>.<cos-endpoint>`.
* Dans l'exemple précédent, la valeur du paramètre Outrepasser l'en-tête d'hôte est définie sur `images.s3.us-west.objectstorage.uat.test.net`.


## Suppression de la règle de page 
{: #cos-delete-page-rule}

Si la règle de page Outrepasser la résolution avec COS n'est plus nécessaire, vous devez supprimer _manuellement_ CNAME et la règle de page. 


## Modification de la règle de page 
{: #cos-edit-page-rule}

Après la modification de la règle de page, le paramètre **Outrepasser la résolution avec COS** n'est plus affiché sur la page. Cependant, les paramètres **Outrepasser la résolution** `<bucket>.<domain>` et **Outrepasser l'en-tête d'hôte** `<bucket>.<cos-endpoint>` remplacent le paramètre **Outrepasser la résolution avec COS**.

La modification du paramètre **Outrepasser la résolution** _ne crée pas_ automatiquement d'enregistrement CNAME (par exemple, ` <updated-bucket>.<domain>`). Cette opération n'est effectuée que lors de la création initiale d'une règle de page à l'aide du paramètre **Outrepasser la résolution avec COS**. Pour créer automatiquement l'enregistrement CNAME pour le compartiment, appliquez la [Création d'étapes de règle de page](#cos-create-page-rule).
