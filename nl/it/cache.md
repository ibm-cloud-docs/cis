---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

# Concetti della memorizzazione nella cache

Questo documento contiene alcuni concetti e definizioni relative alla memorizzazione nella cache e come influisce sulla tua distribuzione IBM CIS. 

## Cosa è la memorizzazione nella cache?

La memorizzazione nella cache è il processo di archiviazione dei file nei tuoi server perimetrali, che effettuiamo allo scopo di migliorare il tempo di risposta quando presentiamo questi file ai clienti. Archiviando i file vicino ai clienti, possiamo diminuire il tempo impiegato dai file di fluire nella rete, normalmente chiamato **latenza**.

Per impostazione predefinita, memorizziamo nella cache i **file statici**, che includono molti tipi di file di testo e immagine (file non HTML). Per impostazione predefinita non memorizziamo nella cache i file HTML perché non li consideriamo statici; tuttavia, è possibile memorizzarli nella cache [utilizzando la funzione Page Rules](using-page-rules.html).

I file memorizzati nella cache hanno un tempo di scadenza specifico, **TTL (Time to Live)** dopo cui vengono eliminati dalla cache. È anche possibile eliminare i file dalla cache manualmente. Dopo aver rimosso i file dalla cache, CIS ritorna al suo server di origine per ricaricare i tuoi file e aggiornare la cache con le ultime versioni.

Una spiegazione dettagliata delle impostazioni della cache e delle tue opzioni di memorizzazione nella cache può essere trovata nell'[esercitazione Memorizzazione nella cache e regole della pagina](caching-with-page-rules.html).
