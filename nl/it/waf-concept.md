---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Web Application Firewall Concepts, web application firewall

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Concetti su WAF (Web Application Firewall) Q & A
{:#waf-q-and-a}

WAF (Web Application Firewall) protegge dagli attacchi di livello ISO 7, che possono essere alcuni dei più complicati. Questo documento fornisce alcuni dettagli.

## Cosa è WAF (Web Application Firewall)?
{:#what-is-a-waf}

Un WAF (Web Application Firewall) aiuta a proteggere le applicazioni web filtrando e monitorando il traffico HTTP tra un'applicazione web e internet. Un WAF è una difesa di livello 7 del protocollo ISO (nel [Modello OSI ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://en.wikipedia.org/wiki/OSI_model)), non è progettato per la difesa da tutti i tipi di attacco. 

Distribuendo WAF davanti a un'applicazione web è come posizionare uno scudo tra l'applicazione web e internet. Un server proxy proteggere un'identità della macchina client utilizzando un intermediario (per il traffico in uscita), ma un WAF è un tipo di proxy inverso che protegge il server dall'esposizione perché il traffico del client viene trasmesso tramite WAF prima di raggiungere il server (per il traffico in entrata).

## Quali tipi attacchi può evitare WAF?
{:#what-types-of-attacks-can-waf-prevent}

Un WAF normalmente protegge le applicazioni web da attacchi come cross-site forgery, cross-site-scripting (XSS), file inclusion e SQL injection, insieme ad altri. Un WAF normalmente fa parte di una suite di strumenti, che insieme possono creare una difesa olistica da vari vettori di attacco.

## Come funziona WAF?
{:#how-does-waf-work}

Un WAF funziona tramite una serie di regole spesso denominate politiche. Queste politiche mirano a proteggere dalle vulnerabilità nell'applicazione filtrando il traffico doloso. 

Il valore di un WAF è nella velocità e facilità con cui possono essere implementate le sue modifiche alla politica, consentendo quindi una risposta più veloce a vari vettori di attacco. Ad esempio, durante un [attacco DDoS ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://en.wikipedia.org/wiki/Denial-of-service_attack), il limite della frequenza può essere implementato modificando le politiche di WAF.

## Quali sono i vantaggi chiave di IBM Cloud CIS Web Application Firewall?
{:#key-benefits-of-cis-waf}

IBM Cloud CIS WAF costituisce un modo facile per configurare, gestire e personalizzare le regole di sicurezza per proteggere le tue applicazioni web dalle minacce web comuni. Vedi il seguente elenco per le funzioni chiave: 

 * **Facile configurazione**: CIS WAF fa parte del nostro servizio complessivo e sono necessari pochi minuti per configurarlo. Una volta reindirizzato a noi il tuo DNS, puoi passare a WAF e configurare le regole di cui hai bisogno. 

 * **Notifica dettagliata** nella notifica sono presenti informazioni dettagliate, ad esempio, le minacce bloccate dalla regola o dal gruppo di regole.  
