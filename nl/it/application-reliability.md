---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain Input information, IBM Cloud Internet Services, Global Load balancing

subcollection: cis

---


{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Miglioramento dell'affidabilità e della scalabilità dell'applicazione con il bilanciamento del carico globale da IBM Cloud Internet Services
{:#improving-application-reliability-and-scalability-with-global-load-balancing-from-ibm-cloud-internet-services}

Se hai un sito web di e-commerce o stai ospitando un'applicazione che deve essere accessibile ai tuoi utenti finali in qualsiasi momento, è probabile che tu sia interessato alla disponibilità e alle prestazioni 24*7 della tua applicazione.  

Le funzionalità di bilanciamento del carico globale disponibili con IBM Cloud Internet Services (CIS) possono migliorare l'affidabilità e la scalabilità delle tue applicazioni mentre viene offerta l'esperienza migliore possibile all'utente finale. Questa guida fornisce una procedura per la configurazione del bilanciamento del carico globale.   

## Cosa otterrai
{:#what-you-accomplish}

In questa guida dettagliata imparerai come eseguire una configurazione simile a quella illustrata di seguito. 

<img src="images/reliability1.png" alt="immagine" style="width: 300px;"/>

In questo esempio, le risorse dell'applicazione vengono distribuite in due ubicazioni di data center, una in Stati Uniti Ovest e una in Stati Uniti Costa Est. Gli utenti finali possono accedere a questa applicazione da tutto il mondo.  

Attività  | Descrizione
------------- | -------------
[Crea un'istanza CIS](/docs/infrastructure/cis?topic=cis-create-your-ibm-cloud-internet-services-cis-instance) | Inizia creando la tua istanza di IBM Cloud Internet Services (CIS) utilizzando il portale del cliente IBM. |
[Immetti le informazioni sul tuo dominio](/docs/infrastructure/cis?topic=cis-input-information-about-your-domain) | Immetti le informazioni sul dominio che vuoi proteggere e per cui vuoi fornire il bilanciamento del carico globale. 
[Avvio della configurazione del programma di bilanciamento del carico globale](/docs/infrastructure/cis?topic=cis-begin-global-load-balancer-configuration) | Avvia la configurazione del tuo programma di bilanciamento del carico globale. 
[Identifica le tue risorse dell'applicazione](/docs/infrastructure/cis?topic=cis-identify-your-application-resources) | Identifica le risorse della tua applicazione, come i pool di origini e i meccanismi del controllo di integrità. 
[Definisci il programma di bilanciamento del carico globale](/docs/infrastructure/cis?topic=cis-define-the-global-load-balancer) | Definisci la configurazione del tuo programma di bilanciamento del carico globale specificando un nome host, aggiungendo e modificando i tuoi pool di origini e definendo ulteriori regole per controllare come viene servito il traffico ai client. 
