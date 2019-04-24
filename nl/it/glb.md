---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: origin server, pool implementation, origin servers

subcollection: cis

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"} 
{:note: .note}

# Concetti sul programma di bilanciamento del carico globale (GLB)
{:#global-load-balancer-glb-concepts}

Questo documento contiene alcuni concetti e definizioni relative al programma di bilanciamento del carico globale (GLB) e come influisce sulla tua distribuzione IBM CIS.

## Programma di bilanciamento del carico globale
{:#global-load-balancer-cis}

Il programma di bilanciamento del carico globale (GLB) gestisce il traffico tra le risorse del server ubicate in più regioni. Il server di origine può servire tutto il contenuto di un sito web, a condizione che il traffico web non vada oltre le funzionalità di elaborazione del server e la latenza non sia un problema primario. GLB utilizza un'implementazione _pool_ che consente la distribuzione del traffico a più origini. Questa funzionalità del pool offre molti vantaggi: 

  * Riduce il tempo di risposta
  * Crea una disponibilità più elevata tramite la ridondanza
  * Aumenta la velocità effettiva del traffico

GLB instrada il traffico al pool con la priorità più elevata, distribuendo il carico tra i suoi server di origine. Vedi la sezione _Pool_ riportata di seguito per informazioni su come viene distribuito il traffico all'interno di un pool. Se il pool primario diventa non disponibile, il traffico viene instradato automaticamente al pool successivo nell'elenco in base alla priorità. 

Se i pool sono configurati per regioni specifiche, per prima cosa il traffico proveniente da tali regioni viene inviato ai pool per la regione specificata. Solo se tutti i pool per una determinata regione sono inattivi, il traffico tornerà ai pool predefiniti. In questo caso, il nodo di fallback è il pool con la priorità più bassa. 

### Come funziona
{:#how-glb-works}
Quando GLB viene creato, per esso viene aggiunto automaticamente un record DNS con il nome del programma di bilanciamento del carico. GLB restituisce poi uno degli indirizzi IP di origine a un client che sta effettuando una richiesta DNS.

Ad esempio, un pool di origini viene creato con due origini che identificano gli indirizzi IP `169.61.244.18` e `169.61.244.19`. Se viene creato un GLB con il nome `glbcust.ibmmo.com` utilizzando il pool di origini, un client su internet può eseguire il comando:
```
$ ping glbcust.ibmom.com
PING glbcust.ibmom.com (169.61.244.18): 56 data bytes
```
In questo esempio, CIS:

    * ha creato un record DNS denominato `glbcust.ibmmo.com`
    * ha utilizzato GLB per risolvere il nome DNS in uno degli indirizzi IP identificati nel pool di origini

Tieni presente che GLB non termina la connessione TCP.
{:note}

L'impostazione di un elemento DNS o di GLB su "proxy" cambia il comportamento.
Se, ad esempio, attivi proxy e **Security > TLS > Mode** con un valore che non sia `Off`, CIS termina in questo momento la connessione TCP e stabilisce una seconda connessione tra CIS e l'iniziatore.

In questo esempio, CIS:

    * ha creato un record DNS denominato: `glbcust.ibmmo.com`
    * ha utilizzato GLB per risolvere il nome DNS in un indirizzo IP fornito da CIS
    
Ora, le connessioni a `glbcust.ibmmo.com` vengono terminate da CIS e i certificati HTTPS vengono ospitati da CIS (necessario per la terminazione TCP).

Una volta che il client si collega all'applicazione, l'immagine dovrebbe essere simile a: 

`[client]<--tls-->[cis]<-->[origin server]`

## Pool
{:#glb-pools}

Un pool è un gruppo di server di origine a cui viene instradato il traffico in modo intelligente quando collegato a un GLB. Il numero minimo di server di origine disponibili per il pool per venire contrassegnato come integro, è configurabile dall'utente insieme al controllo di integrità da utilizzare. Il pool di origini può essere associato a una regione specifica o può essere reso disponibile per tutte le regioni.

### Distribuzione del traffico all'interno di un pool
{:#distribution-of-traffic-within-a-pool}

Per impostazione predefinita, tutto il traffico viene distribuito in modo uniforme tra le origini nel pool utilizzando il protocollo round-robin. Ciò si applica anche ai GLB senza proxy.

Le origini possono essere configurate con pesi e per i GLB con proxy, i pesi determinano quanto traffico viene ricevuto da ciascun server di origine in relazione alle altre origini nel pool. I pesi sono configurati come numeri compresi tra 0 e 1 e specificano quale frazione del traffico andrà all'origine.  

Per ciascuna origine: 

` Percentuale del traffico all'origine = peso dell'origine / somma di tutti i pesi dell'origine`

Se tutte le origini hanno il peso `1`, il traffico viene distribuito in modo uniforme. 

Le origini con peso `0` non ricevono traffico per questo pool. Tuttavia, l'affinità di sessione potrebbe ancora avere la precedenza su questa impostazione fino a quando tutte le sessioni non vengono chiuse. Se l'origine è un membro di un altro pool, potrebbe ancora ricevere traffico per tale pool. 

**Esempio:** 

Un pool di origini è configurato con 3 origini che hanno i seguenti pesi: origine-A: 0,4, origine-B: 0,3 e origine-C: 0,3. 

* Inizialmente, tutte le origini sono integre. La quantità di traffico ricevuto da ciascuna origine è: origine-A: 40%, origine-B: 30%, e origine-C: 30%.
* La situazione di origine-A diventa critica; non può più ricevere traffico. Le origini rimanenti hanno lo stesso peso e quindi il traffico viene distribuito in modo uniforme, ciascuna riceve il 50%.
* L'amministratore modifica il peso di origine-C in `0`. Ora il 100% del nuovo traffico va a origine-B. Ma con l'affinità di sessione attivata, il traffico per le sessioni esistenti su origine-C continua ad andare a origine-C fino a quando tali sessioni non vengono chiuse (massimo 24 ore).

### Pool di fallback
{:#fallback-pool}

Il pool di origini con la priorità più bassa (il numero più grande) è il "pool di fallback" designato. Quando tutti i pool per una determinata regione sono inattivi, il traffico viene instradato al pool di fallback, indipendentemente dalla sua integrità. 

Quando tutti i pool sono disabilitati, il pool di fallback non è disponibile.
{:note}

## Controllo di integrità
{:#cis-health-check}

Un controllo di integrità consente di acquisire informazioni dettagliate sulla disponibilità dei pool in modo che il traffico possa essere instradato solo ai pool integri. Questi controlli inviano periodicamente le richieste HTTP, HTTPS o TCP e monitorano le risposte. Possono essere configurati con porta, intervallo, timeout, codice di stato personalizzati e altro. Non appena un pool viene contrassegnato come non integro, il traffico viene reinstradato in modo intelligente a un altro pool disponibile.
Tieni presente che i tuoi log hanno riferimenti a Cloudflare in quanto IBM collabora con Cloudflare per potenziare CIS.
{:note}

### Eventi del controllo di integrità
{:#health-check-events}

Gli eventi del controllo di integrità sono modifiche di stato dei pool con controlli di integrità collegati e dei loro server di origine associati. Se lo stato di un'origine si degrada, in una tabella compare una nuova voce con la descrizione dell'evento. Vai a **Reliability > Global Load Balancer > Health Check Events** per vedere una tabella degli eventi del controllo di integrità. Ora puoi filtrare in base alla data, all'integrità del pool o dell'origine, al nome pool e al nome origine selezionando i parametri di filtro dai menu a discesa. Le colonne all'interno della tabella sono ordinabili facendo clic sul nome della colonna.
![>Tabella degli eventi del controllo di integrità](images/health-check-events-table.png)

Le singole righe all'interno della tabella si espandono con ulteriori informazioni relative alla voce. Se il pool è integro, è visibile solo il tile **Pool Details**. Quando la riga contiene un'origine critica oppure un pool degradato, compare anche il tile **Affected Origin Details**. 

![Dettagli degli eventi del controllo di integrità](images/health-check-events-details.png)

#### Dettagli del pool (Pool Details):
* Pool Name - Il nome del pool
* Healthy Origins - Rapporto delle origini integre rispetto a quelle totali in un pool
* Healthy Threshold - Numero delle origini che devono essere integre per poter considerare integro il pool
* Healthy Origins - Nomi delle origini integre
* Critical Origins - Nomi delle origini non integre

#### Dettagli dell'origine interessata (Affected Origin Details):
* Origin Name - Nome dell'origine
* Origin Address - Indirizzo dell'origine
