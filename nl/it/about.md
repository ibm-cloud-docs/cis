---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Caching, IBM Cloud Internet Services, Web Application Firewall

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 

# Informazioni su IBM Cloud Internet Services (CIS)
{:#about-ibm-cloud-internet-services-cis}

IBM Cloud Internet Services (CIS), con tecnologia Cloudflare, fornisce un servizio internet veloce, altamente performante e sicuro per i clienti che eseguono i loro business su IBM Cloud.    

IBM CIS ti fa iniziare velocemente stabilendo dei valori predefiniti, che puoi modificare facilmente utilizzando l'API o la IU. Questi sono alcuni dei parametri modificati più comunemente:

 * **Impostazioni DNS**: puoi utilizzare IBM CIS per ospitare la tua DNS o puoi creare record CNAME.
 * **Impostazioni di crittografia (TLS)**: il valore predefinito è la modalità `flexible`, che codifica la connessione tra il tuo host e il server edge di IBM CIS ma non codifica la comunicazione tra il server edge di IBM CIS e il server di origine.

## WAF (Web Application Firewall)
{:#about-waf}

IBM CIS fornisce la funzionalità WAF (Web Application Firewall), che esamina il traffico web alla ricerca di attività sospetta. Può filtrare il traffico illegale automaticamente - in base alle serie di regole - per cercare le richieste web basate su POST e GET. Puoi utilizzare varie serie di regole per determinare quale traffico bloccare, contestare o lasciar passare. Il nostro WAF può bloccare spam del commento, attacchi di cross-site scripting e SQL injection.

Puoi abilitare o disabilitare WAF a tua discrezione. Ti consigliamo di lasciarlo sempre attivo.

## Protezione da attacchi DDoS
{:#ddos-protection}

IBM CIS fornisce la protezione DDoS che si pone tra il tuo sito web e gli aggressori, indipendentemente dalla durata o dalla dimensione dell'attacco.

## Bilanciamento del carico
{:#about-load-balancing}

Il bilanciamento del carico di IBM CIS funziona al livello di DNS autorevole. Incorpora i controlli di integrità avanzati per monitorare l'integrità delle origini e modificare dinamicamente le risposte DNS. In aggiunta, puoi configurare le politiche geografiche per il bilanciamento del carico globale (GLB).

### Controlli di integrità
{:#about-health-checks}

I controlli di integrità del bilanciamento del carico sono eseguiti su URL specifici tramite richieste HTTP o HTTPS periodiche e sono configurati con codici di stato, timeout e intervalli personalizzabili. Quando un server di origine viene contrassegnato come non integro, i visitatori vengono allontanati per evitare degli errori, utilizzando le nostre veloci rotte di failover.
 
### Politiche geografiche per il bilanciamento del carico globale (GLB)
{geo-policies-and-glb}

Le politiche geografiche ti forniscono il controllo dei server di origine a cui viene indirizzato un client selezionato, in base all'ubicazione geografica di tale client. Ad esempio, potresti configurare le tue politiche geografiche in modo che i visitatori in Europa siano inviati all'origine europea più vicina del tuo sito web o della tua applicazione, i visitatori U.S. siano inviati a un'origine nord americana e così via.

## Memorizzazione nella cache
{:#about-caching}

La memorizzazione nella cache è un modo per memorizzare il contenuto web statico più vicino ai tuoi visitatori del sito, migliorando significativamente le prestazioni del sito web. Il nostro ambiente di distribuzione globale permette ai proprietari del contenuto web una esperienza uniforme, in tutto il mondo.  
 
## Codifica con TLS
{:#encryption-with-tls}

Codifica la comunicazione a/da il tuo sito web utilizzando TLS (Transport Layer Security). Possono essere necessarie fino a 24 ore dopo che il sito web diviene attivo per l'emissione dei tuoi nuovi certificati.

Puoi trovare ulteriori informazioni su TLS nelle nostre [FAQ](/docs/infrastructure/cis?topic=cis-faq).
