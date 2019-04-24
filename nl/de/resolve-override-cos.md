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

# Überschreibung mit COS auflösen
{: #resolve-override-cos}

## Anwendungsfälle
{: #cos-use-cases}

Sorgen Sie dafür, dass die Anforderung, die mit der Seitenregel übereinstimmt, in eine COS-Bucketressource (COS, Cloud Object Storage, Cloudobjektspeicher) aufgelöst wird. 


## Voraussetzungen
{: #cos-prerequisites}

Die folgenden Schritte setzen voraus, dass Sie über eine vorhandene COS-Instanz und ein Bucket mit öffentlichem Zugriff verfügen. Informationen zu öffentlichem Zugriff finden Sie unter [Öffentlichen Zugriff ermöglichen](/docs/services/cloud-object-storage/iam?topic=cloud-object-storage-allowing-public-access).


## Schritte beim Erstellen einer Seitenregel
{: #cos-create-page-rule}

* Navigieren Sie zu **Leistung -> Seitenregeln**.
* Klicken Sie auf die Schaltfläche **Regel erstellen**.
* Geben Sie den gewünschten Wert für den URL-Abgleich ein. Beispiel: `*.foo.com/*`.
  * Beachten Sie, dass der URL-Abgleich mit Ihrem COS-Objektnamen übereinstimmen muss. 
  * Beispiel: Wenn Sie ein Objekt mit dem Namen 'reports.txt' unter dem Bucket `my-bucket1` haben, dann sind beide URL-Übereinstimmungen gültig. 
    * `*.foo.com/*`
    * `*.foo.com/reports.txt`
* Verwenden Sie das Dropdown-Menü, um **Überschreibung mit COS auflösen** im Abschnitt **Leistung** auszuwählen. 
* Verwenden Sie das Dropdown-Menü **Cloud Object Storage-Instanz**, um die gewünschte Instanz auszuwählen.  
* Verwenden Sie das Dropdown-Menü **Bucket**, um das gewünschte Bucket auszuwählen. 
* Klicken Sie auf die Schaltfläche **1 Ressource bereitstellen**, um eine Seitenregel zu erstellen. 


## Ausführliche Erläuterung der Konzepte
{: #cos-detail-concepts}

Beim Erstellen einer Seitenregel **Überschreibung mit COS auflösen** erstellt CIS automatisch die anderen erforderlichen Ressourcen für die COS-Integration. Dazu gehören: 

**CNAME**
* Ein CNAME DNS-Datensatz für `<bucket-name>.<cos-endpoint>` als `<bucket-name>`.
* Wenn Ihre CIS-Domäne beispielsweise `foo.com` lautet, Sie über ein COS-Bucket mit dem Namen `images` verfügen und Ihr öffentlicher COS-Endpunkt `s3.us-west.objectstorage.uat.test.net` ist, dann wird CIS einen CNAME als `images.foo.com` erstellen, der auf `images.s3.us-west.objectstorage.uat.test.net` verweist.
Wenn die Seitenregel 'Überschreibung mit COS auflösen' nicht mehr benötigt wird, sollte der CNAME manuell zusammen mit der Seitenregel gelöscht werden.
{:note}

**Überschreibung des Host-Headers**
* Die Einstellung 'Überschreiben des Host-Headers' ersetzt den Host-Header für die URI, die mit der Seitenregel übereinstimmt, durch `<bucket-name>.<cos-endpoint>`.
* Wenn Sie das vorherige Beispiel verwenden, wird der Wert für das Überschreiben des Host-Headers auf `images.s3.us-west.objectstorage.uat.test.net` gesetzt.


## Seitenregel löschen 
{: #cos-delete-page-rule}

Wenn die Seitenregel 'Überschreibung mit COS auflösen' nicht mehr benötigt wird, sollte der CNAME _manuell_ zusammen mit der Seitenregel gelöscht werden.


## Seitenregel bearbeiten
{: #cos-edit-page-rule}

Nach dem Bearbeiten der Seitenregel, wird **Überschreibung mit COS auflösen** nicht mehr auf der Seite angezeigt. Aber **Überschreibung auflösen**`<bucket>.<domain>` und **Überschreibung des Host-Headers**`<bucket>.<cos-endpoint>` ersetzen **Überschreibung mit COS auflösen**.

Wenn Sie Änderungen an **Überschreibung auflösen** vornehmen, wird _nicht_ automatisch ein neuer CNAME-Datensatz erstellt (zum Beispiel: `<updated-bucket>.<domain>`. Dies erfolgt erst bei der Ersterstellung einer Seitenregel mit **Überschreibung mit COS auflösen**. Führen Sie die Schritte unter [Seitenregel erstellen](#cos-create-page-rule) aus, um den CNAME-Datensatz für das Bucket automatisch zu erstellen.
