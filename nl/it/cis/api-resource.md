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

# Specifiche API 

Ecco come visualizzare le specifiche API CIS: 

1. Per visualizzare le API CIS, passa alla pagina [CIS API Spec](https://console.bluemix.net/apidocs/2640-cloud-internet-services). 

2. Dal menu di navigazione di sinistra, scegli dall'elenco di API disponibili.


## Note

1. Endpoint API: https://api.cis.cloud.ibm.com.

2. L'intestazione **X-Auth-User-Token** è obbligatoria per ogni chiamata API. Questo è il token di connessione dell'utente che può essere richiamato da IAM (ad esempio, utilizzando il comando "bx iam oauth-tokens").

3. Anche il campo **crn** è obbligatorio nel percorso di ogni chiamata API. Questo è il CRN (Cloud Resource Name) completo di un'istanza della risorsa CIS che sta venendo configurata (ad esempio, il CRN di un'istanza della risorsa può essere richiamato dal proprio nome utilizzando il comando "bx resource service-instance <instance-name>"). Il CRN deve essere codificato URL nella chiamata API.

4. Le chiamate API sono a frequenza limitata. Può essere effettuato un totale di 100 chiamate API in 1 minuto. Se questa frequenza viene superata, le successive chiamate saranno bloccate per un certo periodo di tempo.
