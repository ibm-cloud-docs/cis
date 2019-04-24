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

# API-Spezifikationen
{:#api-specs}

Im Folgenden wird erläutert, wie Sie die CIS-API-Spezifikationen anzeigen können: 

1. Navigieren Sie zur Seite [API-Dokumente](/apidocs/), um die CIS-APIs anzuzeigen.  

2. Überprüfen Sie im linken Navigationsmenü das Feld für den Netzbetrieb, um die APIs zu filtern. 

3. Wählen Sie aus der Liste der verfügbaren Cloud Internet Services-APIs aus.


## Anmerkungen
{:#api-notes}

1. API-Endpunkt: `https://api.cis.cloud.ibm.com`.

2. Der Header **X-Auth-User-Token** ist für jeden API-Aufruf erforderlich. Dieser Header ist das Trägertoken für den Benutzer, das vom IAM (zum Beispiel mithilfe des Befehls `ibmcloud iam oauth-tokens`) abgerufen werden kann.

3. Das Feld **crn** muss ebenfalls im Pfad für jeden API-Aufruf angegeben werden. Dieses Feld enthält den vollständigen CRN (Cloud Resource Name) für eine CIS-Ressourceninstanz, die konfiguriert wird. (Die CRN für eine Ressourceninstanz kann beispielsweise mit dem Befehl `ibmcloud resource service-instance <instance-name>` von ihrem Namen abgerufen werden.) Der CRN muss im API-Aufruf URL-codiert sein.

4. API-Aufrufe sind gedrosselt. Insgesamt können 100 API-Aufrufe in einer Minute ausgeführt werden. Wenn diese Rate überschritten wird, werden nachfolgende Aufrufe für eine bestimmte Zeitdauer blockiert. 
