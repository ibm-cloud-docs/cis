---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Glossary, load balancer, pool, health check

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Glossario
{:#glossary}

Questo glossario contiene le definizioni per i termini comuni che puoi incontrare mentre utilizzi il programma di bilanciamento del carico (Global Load Balancer - GLB).

## Programma di bilanciamento del carico
{:#glossary-load-balancer}

Un programma di bilanciamento del carico è un dispositivo che agisce come un proxy inverso e distribuisce il traffico di rete o dell'applicazione in un numero di server. I programmi di bilanciamento del carico vengono utilizzati per incrementare la capacità di sistema (il numero di utenti simultanei) e per migliorare l'affidabilità delle applicazioni. 

## Pool
{:#glossary-pool}

Un pool è un gruppo di server di origine a cui viene instradato il traffico in modo intelligente quando collegato a un GLB. Il numero minimo di server di origine disponibili per il pool per venire contrassegnato come integro, è configurabile dall'utente insieme al controllo di integrità da utilizzare. Il pool di origini può essere associato a una regione specifica o può essere reso disponibile per tutte le regioni.

## Controllo di integrità
{:#glossary-health-check}

Un controllo di integrità consente di acquisire informazioni dettagliate sulla disponibilità dei pool in modo che il traffico possa essere instradato solo ai pool integri. Questi controlli inviano periodicamente le richieste HTTP/HTTPS e monitorano le risposte. Possono essere configurati con codici di stato, timeout, intervalli personalizzati e altro ancora. Non appena un pool viene contrassegnato come non integro, il traffico sarà reinstradato in modo intelligente a un altro pool disponibile, se presente.

## Server di origine
{:#glossary-origin-servers}

Un server di origine elabora e risponde alle richieste in entrata dai client e di norma viene utilizzato con i server in cache. I server di origine eseguono uno o più programmi progettati per ascoltare ed elaborare le richieste Internet in entrata. La distanza fisica tra il server di origine e il client che effettua una richiesta, aggiunge latenza alla connessione, aumentando il tempo di caricamento. L'utilizzo dei server in cache riduce questa latenza. 


