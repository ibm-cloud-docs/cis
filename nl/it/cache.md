---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM CIS deployment, query strings, HTML files

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Concetti della memorizzazione nella cache
{:#caching-concepts}

Questo documento contiene alcuni concetti e definizioni relative alla memorizzazione nella cache e come influisce sulla tua distribuzione IBM CIS.

## Cosa è la memorizzazione nella cache?
{:#what-is-caching}

La memorizzazione nella cache è il processo di archiviazione dei file nei tuoi server edge, che effettuiamo allo scopo di migliorare il tempo di risposta quando presentiamo questi file ai clienti. Archiviando i file vicino ai clienti, possiamo diminuire il tempo impiegato dai file di fluire nella rete, normalmente chiamato **latenza**.

I file memorizzati nella cache hanno un tempo di scadenza specifico, **TTL (Time to Live)** dopo cui vengono eliminati dalla cache. È anche possibile eliminare i file dalla cache manualmente. Dopo aver rimosso i file dalla cache, CIS ritorna al suo server di origine per ricaricare i tuoi file e aggiornare la cache con le ultime versioni.

Una spiegazione dettagliata delle impostazioni della cache e delle tue opzioni di memorizzazione nella cache può essere trovata nell'[esercitazione Memorizzazione nella cache e regole della pagina](/docs/infrastructure/cis?topic=cis-use-page-rules-with-caching).

### Quale contenuto viene memorizzato nella cache?
{:#what-content-is-cached}

Per impostazione predefinita, memorizziamo nella cache i **file statici**, che includono molti tipi di file di testo e immagine (file non HTML). Ciò include solo i file provenienti dai tuoi siti web e non da risorse di terze parti derivanti da siti di social networking, ecc. Inoltre, al momento non memorizziamo nella cache con tipo MIME.

### Come memorizzo nella cache i file HTML? 
{:#how-do-i-cache-html}

Per impostazione predefinita, non memorizziamo nella cache i file HTML perché non li consideriamo statici; tuttavia, se un HTML statico può essere chiaramente distinto da un HTML dinamico, è possibile memorizzare nella cache i file HTML [utilizzando la funzione Page Rules](/docs/infrastructure/cis?topic=cis-use-page-rules).


## Query String Sort
{:#query-string-sorting}

**Solo Enterprise** CIS tratta gli URL che hanno stringhe di query in ordini diversi come file separati nella cache. Ciò significa che se un utente richiede:

`/video/123456?title=0&byline=0&portrait=0&color=987654`

E un altro utente richiede:

`/video/123456?byline=0&color=987654&portrait=0&title=0`

CIS torna all'origine, anche se abbiamo il file nella nostra cache.

Query String Sort ordina le stringhe di query _prima_ prima che vengano cercati riscontri nella nostra cache, determinando una frequenza di riscontri cache più elevata. Abilita Query String Sort utilizzando l'interruttore nella pagina **Caching**.

## Serve Stale Content
{:#serve-stale-content-caching}

Mantiene una versione limitata del sito online se il server si arresta. Anche se il contenuto è scaduto, CIS continuerà a fornire il contenuto memorizzato nella cache agli utenti quando i server di origine sono offline.
