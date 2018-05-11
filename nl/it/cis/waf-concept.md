---
copyright:
  years: 2018
lastupdated: "2018-03-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Concetti su WAF (Web Application Firewall) Q & A

WAF (Web Application Firewall) protegge dagli attacchi di livello ISO 7, che possono essere alcuni dei più complicati. Questo documento fornisce alcuni dettagli.

## Cosa è WAF (Web Application Firewall)?
Un WAF (Web Application Firewall) aiuta a proteggere le applicazioni web filtrando e monitorando il traffico HTTP tra un'applicazione web e internet. Un WAF è una difesa di livello 7 del protocollo ISO (nel [Modello OSI ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://en.wikipedia.org/wiki/OSI_model)), non è progettato per la difesa da tutti i tipi di attacco. 

Distribuendo WAF davanti a un'applicazione web è come posizionare uno scudo tra l'applicazione web e internet. Un server proxy proteggere un'identità della macchina client utilizzando un intermediario (per il traffico in uscita), ma un WAF è un tipo di proxy inverso che protegge il server dall'esposizione perché il traffico del client viene trasmesso tramite WAF prima di raggiungere il server (per il traffico in entrata).

## Quali tipi attacchi può evitare WAF?
Un WAF normalmente protegge le applicazioni web da attacchi come cross-site forgery, cross-site-scripting (XSS), file inclusion e SQL injection, insieme ad altri. Un WAF normalmente fa parte di una suite di strumenti, che insieme possono creare una difesa olistica da vari vettori di attacco.

## Come funziona WAF?

Un WAF funziona tramite una serie di regole spesso denominate politiche. Queste politiche mirano a proteggere dalle vulnerabilità nell'applicazione filtrando il traffico doloso. 

Il valore di un WAF è nella velocità e facilità con cui possono essere implementate le sue modifiche alla politica, consentendo quindi una risposta più veloce a vari vettori di attacco. Ad esempio, durante un [attacco DDoS ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://en.wikipedia.org/wiki/Denial-of-service_attack), il limite della frequenza può essere implementato modificando le politiche di WAF.
