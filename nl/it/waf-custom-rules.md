---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: WAF Custom Rules, Custom WAF Rules

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Regole personalizzate WAF
{:#waf-custom-rules}

Passa a Custom WAF Rules tramite **Security > Web Application Firewall > Custom rules**. Le regole WAF sono disponibili nei piani Enterprise e vengono create in base ai requisiti univoci di tale cliente e/o ai modelli di traffico del suo sito web. Ciò significa che puoi chiederci di bloccare virtualmente qualsiasi combinazione di caratteristiche di una richiesta.  

Le regole WAF personalizzate si adattano a situazioni in cui IBM WAF non ha ancora una regola attiva e l'aggressore utilizza uno specifico modello o agent utente destinato specificatamente per la struttura del tuo sito web. In queste situazioni, puoi creare una regola personalizzata per la tua proprietà web. 

## Richiedi una regola personalizzata
{:#request-a-custom-rule}

Per richiedere una regola, invia una email all'indirizzo wafsup@us.ibm.com con i requisiti della regola o i modelli di traffico.  

Fornisci più informazioni possibili, compreso: 
* Log di accesso che mostrano un campione di circa 100 presunte richieste dolose. 
* Una richiesta POST di esempio che include i dati POST (se le richieste hanno un corpo POST) per determinare se la richiesta contiene elementi che possiamo bloccare o in base ai quali attivare la regola. 
* Se desideri che le richieste vengano bloccate completamente oppure verificate in caso di potenziali falsi positivi. 
* I domini specifici a cui desideri che vengano applicate queste regole. 
* Se desideri che le regole vengano attivate o disattivate per impostazione predefinita. 

Una volta create le tue regole WAF personalizzate, devi abilitarle tutte affinché diventino effettive.
{:note}
