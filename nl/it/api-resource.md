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

# Specifiche API
{:#api-specs}

Ecco come visualizzare le specifiche API CIS: 

1. Per visualizzare le API CIS, passa alla pagina [API Docs](/apidocs/). 

2. Dal menu di navigazione di sinistra, controlla la casella Networking per filtrare le API.

3. Scegli dall'elenco delle API CIS (Cloud Internet Services) disponibili.


## Note
{:#api-notes}

1. Endpoint API: `https://api.cis.cloud.ibm.com`.

2. L'intestazione **X-Auth-User-Token** è obbligatoria per ogni chiamata API. Questa intestazione è il token di connessione dell'utente che può essere richiamato da IAM (ad esempio, utilizzando il comando `ibmcloud iam oauth-tokens`).

3. Anche il campo **crn** è obbligatorio nel percorso di ogni chiamata API. Questo campo contiene il CRN (Cloud Resource Name) completo di un'istanza della risorsa CIS che viene configurata. (Ad esempio, il CRN di un'istanza della risorsa può essere richiamato dal suo nome utilizzando il comando `ibmcloud resource service-instance <instance-name>`). Il CRN deve essere codificato URL nella chiamata API.

4. Le chiamate API sono a frequenza limitata. Può essere effettuato un totale di 100 chiamate API in 1 minuto. Se questa frequenza viene superata, le chiamate successive vengono bloccate per un periodo di tempo. 
