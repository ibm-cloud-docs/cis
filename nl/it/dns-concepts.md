---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain name system, DNS servers, match domain names, DNS Concepts

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}


# Concetti su DNS
{:#dns-concepts}

Questo documento contiene alcuni concetti e definizioni relativi al DNS (domain name system) di internet e come influenza la tua distribuzione di IBM Cloud Internet Services (CIS). 

Il DNS (Domain Name System) è alla base del web che utilizziamo tutti i giorni. Funziona in modo trasparente in background, convertendo i nomi del sito web leggibili dall'utente in leggibili dal computer, gli indirizzi IP che seguono [le linee guida internet RFC 1918 per IPv4 e RFC 4193 per IPv6](https://en.wikipedia.org/wiki/Private_network). In breve, i server DNS mettono in corrispondenza i nomi del dominio, come `ibm.com`, con i rispettivi indirizzi IP associati, che la maggior parte delle persone non ha bisogno di conoscere. 

Il sistema DNS ricerca queste informazioni su indirizzo IP e nome host in una rete di server DNS collegati in internet, in modo simile a come le persone potrebbero cercare un luogo utilizzando un elenco telefonico o una cartina.

## Server dei nomi
{:#dns-concepts-nameservers}

Un **server dei nomi** implementa i servizi che forniscono le risposte alle query in un servizio della directory. Traduce gli identificativi host o web basati sul testo e significativi in indirizzi IP.

La **Delega del server dei nomi** avviene quando un server dei nomi di un dominio riceve una richiesta di record del dominio secondario e risponde con il riferimento del server dei nomi al server delegato. Questa funzionalità ti consente di decentralizzare la gestione di un dominio di grandi dimensioni (come `ibm.com`).

Un **server dei nomi del dominio personalizzato** ti consente di utilizzare i server del provider DNS con il nome di riferimento personalizzato del tuo dominio. Ad esempio, puoi definire il tuo server dei nomi per essere `ns1.cloud.ibm.com` invece di `ns1.acme.com`.

## DNS protetto
{:#dns-concepts-secure-dns}

**DNSSec** è una tecnologia per 'firmare' digitalmente i dati DNS in modo da assicurarti che siano validi. Per eliminare la vulnerabilità da internet, DNSSec deve essere distribuito in ogni fase della ricerca, dalla zona root al nome del dominio finale (ad esempio, www.icann.org).

## Flattening del CNAME del record root
{:#dns-concepts-root-record-cname-flattening}

IBM CIS supporta una funzione denominata "flattening del CNAME." Utilizzando questo metodo, i record root possono superare la limitazione IETF RFC relativa al fatto che se un record root è un CNAME, non può avere altri record per tale dominio. I server CIS autorevoli possono superare questa limitazione restituendo record A corrispondenti alla destinazione CNAME invece di restituire il CNAME stesso, nascondendo effettivamente il CNAME. Questa tecnica consente ad altri record, come ad esempio i record MX, di essere aggiunti al dominio, anche se il record root è un CNAME.

## Record DNS con proxy
{:#dns-concepts-proxying-dns-records}

IBM CIS supporta la capacità di scegliere se un record è con proxy o meno. Quando un record è con proxy, significa che il suo traffico verrà eseguito direttamente tramite IBM CIS. Al momento, i record con i tipi **A**, **AAAA** o **CNAME** possono essere con proxy.
