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

# API-Spezifikationen

Im Folgenden wird erläutert, wie Sie die CIS-API-Spezifikationen anzeigen können:  

1. Zum Anzeigen der CIS-APIs navigieren Sie zur Seite mit den [CIS-API-Spezifikationen](https://console.bluemix.net/apidocs/2640-cloud-internet-services).  

2. Treffen Sie im linken Navigationsmenü in der Liste von verfügbaren APIs eine Auswahl. 


## Anmerkungen

1. API-Endpunkt: https://api.cis.cloud.ibm.com.

2. Der Header **X-Auth-User-Token** ist für jeden API-Aufruf erforderlich. Dabei handelt es sich um das Trägertoken für den Benutzer, das aus IAM abgerufen werden kann (z. B. mit dem Befehl 'bx iam oauth-tokens'). 

3. Das Feld **crn** muss ebenfalls im Pfad für jeden API-Aufruf angegeben werden. Dies ist der vollständige Cloudressourcenname (CRN) für eine CIS-Ressourceninstanz, die gerade konfiguriert wird (z. B. kann der CRN für eine Ressourceninstanz mithilfe des Befehls 'bx resource service-instance <instanzame>' aus seinem Namen abgeleitet werden). Der CRN muss im API-Aufruf URL-codiert sein. 

4. API-Aufrufe sind gedrosselt. Insgesamt können 100 API-Aufrufe in einer Minute ausgeführt werden. Wird diese Rate überschritten, werden nachfolgende Aufrufe für einen bestimmten Zeitraum blockiert. 
