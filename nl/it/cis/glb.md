---

copyright:
  years: 2018
lastupdated: "2018-03-05"

---

# Concetti sul programma di bilanciamento del carico globale (GLB)

Questo documento contiene alcuni concetti e definizioni relative al programma di bilanciamento del carico globale (GLB) e come influisce sulla tua distribuzione IBM CIS. 

## Programma di bilanciamento del carico globale 

Il programma di bilanciamento del carico globale (GLB) gestisce il traffico tra le risorse del server ubicate in più regioni. GLB utilizza un pool che consente al traffico di essere distribuito a più origini. Questo fornisce molti vantaggi tra cui:

  * Ridurre il tempo di risposta
  * Elevata disponibilità tramite la ridondanza
  * Aumento della velocità effettiva del traffico

## Pool

Un pool è un gruppo di server di origine a cui viene instradato il traffico in modo intelligente quando collegato a un GLB. Il numero minimo di server di origine disponibili per il pool per venire contrassegnato come integro, è configurabile dall'utente insieme al controllo di integrità da utilizzare. Il pool di origini può essere associato a una regione specifica o può essere reso disponibile per tutte le regioni.

## Controllo di integrità

Un controllo di integrità consente di acquisire informazioni dettagliate sulla disponibilità dei pool in modo che il traffico possa essere instradato solo ai pool integri. Questi controlli inviano periodicamente le richieste HTTP/HTTPS e monitorano le risposte. Possono essere configurati con codici di stato, timeout, intervalli personalizzati e altro ancora. Non appena un pool viene contrassegnato come non integro, il traffico sarà reinstradato in modo intelligente a un altro pool disponibile, se presente.
