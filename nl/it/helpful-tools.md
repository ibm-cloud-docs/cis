---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Helpful tools, whois, IPv4

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Strumenti utili per la gestione della tua distribuzione CIS
{:#helpful-tools-for-managing-your-cis-deployment}

Esistono alcuni strumenti di gestione del sistema unix di dominio pubblico che possono essere utili nella gestione della tua distribuzione IBM CIS.

## Strumenti sysadmin
{:#cis-sysadmin-tools}

 * whois (strumento di identificazione del dominio)
 * dig (strumento DNS)
 * curl (strumento HTTP e HTTPS)
 * netcat (strumento IP e porta)
 * traceroute (strumento di rete)

## Strumenti commerciali per la verifica remota e esterna
{:#commercial-tools-for-external-and-remote-testing}

 * GTMetrix (http)
 * Web page test (http)
 * WhatsMyDNS (strumento DNS)
 * G Suite Toolbox (DNS e HTTP)

## Strumenti per la ricerca dei log e della cronologia
{:#tools-for-looking-at-logs-and-history}

 * File di archivio HTTP (file HAR)


### Utilizzo di `whois`
{:#using-whois}

`whois` è uno strumento della riga di comando unix che puoi utilizzare per ricercare le informazioni sulla funzione di registrazione di un nome del dominio o un indirizzo IP selezionato, ad esempio, i server autorevoli forniti del dominio o il proprietario di un indirizzo IP particolare.

Esempi:

`whois example.com`

`whois 8.8.8.8`

### Utilizzo di `dig`
{:#using-dig}

`dig` è uno strumento della riga di comando unix che può eseguire le query DNS e controllare i record DNS di un dominio specifico. È simile a `nslookup`.

Lo schema di questo comando è: dig <recordtype. <domainname> <options>

**Esempi:**

`dig example.com`

`dig my.example.com`

`dig example.com +trace`

`dig NS example.com`

`dig example.com @ns.example.com`

### Utilizzo di `cURL`
{:#using-curl}

`cURL` è uno strumento della riga di comando unix che ti permette di trasmettere i dati utilizzando la sintassi dell'URL. Viene comunemente utilizzato per effettuare le richieste HTTP o per confrontare le risposte del server.

Lo schema per questo comando è: `curl -option1 -option2 http://example.com/url`

**Esempi:**

`curl -svo /dev/null http://www.example.com`

`curl -svo /dev/null -A “USER_AGENT_STRING” http://www.example.com`

`curl -svo /dev/null -H “host: www.example.com” http://ORIGIN_IP`

`curl -svo /dev/null -H https://www.example.com --resolve www.example.com:443:ORIGIN_IP`

### Utilizzo di `mtr` e `traceroute`
{:#using-mtr-and-traceroute}

MTR e `traceroute` sono strumenti di un comando unix che ti permette di misurare le prestazioni o la latenza insieme a un percorso di rete specifico per un server di destinazione o un host specifico.

**Esempi:**

`mtr -rwc 20 example.com -T -4`
`mtr -rwc 20 8.8.8.8 -T -6`

`traceroute example.com -T -4`

`traceroute 8.8.8.8 -T -6`

| Opzione | Definizione |
|---------|-----------|
| -c | Sets the number of pings sent |
| -T | Forces a TCP traceroute (normally ICMP) |
| -4 | Forces the use of IPv4 |
| -6 | Forces the use of IPv6 |

### Generazione di un file HAR
{:#generating-a-har-file}

Un file HAR è una registrazione delle richieste HTTP da un browser web. I browser come ad esempio Chrome hanno una sezione degli strumenti per sviluppatori che ti aiuta a creare un file HAR.
