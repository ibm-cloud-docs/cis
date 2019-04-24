---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gestisci la tua distribuzione IBM CIS per l'affidabilità ottimale

Per raggiungere l'affidabilità ottimale per la tua distribuzione IBM CIS, puoi configurare una configurazione DNS utile e i programmi di bilanciamento del carico. Per maggiore affidabilità, puoi utilizzare le nostre regole della pagina per assicurarti che il tuo contenuto web sia distribuito ai tuoi clienti, anche se il tuo server di origine o la cache ha un problema. Questo documento fornisce i dettagli su alcune procedure consigliate per rendere la tua distribuzione IBM CIS affidabile in modo ottimale.

Generalmente, le nostre procedure consigliate sono queste:

 * Configura il tuo DNS per usufruire dei vantaggi dei server proxy e di altre funzioni di IBM CIS
 * Utilizza uno o più programmi di bilanciamento del carico globale per distribuire il tuo traffico del sito uniformemente
 * Configura le regole della pagina appropriate per gestire la tua memorizzazione nella cache e altre opzioni

Ognuno di questi elementi fornisce alcune funzionalità che puoi utilizzare per creare una distribuzione CIS più affidabile.

Tieni presente che l'interfaccia CIS è organizzata in sezioni per *security*, *reliability* e *perfomance*. Il menu di navigazione principale viene illustrato nella seguente figura, con gli elementi del menu DNS e i programmi di bilanciamento del carico globale mostrati:

![DNS navigazione sinistra ](images/cis-left-navigation.png)


## Configurazione del DNS
 
 Per iniziare l'impostazione della tua configurazione DNS, seleziona **DNS** dal menu di navigazione, come mostrato precedentemente.
 
 Per le informazioni dettagliare sulla configurazione e la gestione dell'affidabilità del tuo DNS, [fai riferimento a questo documento](dns.html#setting-up-your-domain-name-system-dns-for-ibm-cis).


## Configurazione dei programmi di bilanciamento del carico globale


Per iniziare la configurazione dei tuoi programmi di bilanciamento del carico globale, seleziona **Global Load Balancers** dal menu di navigazione.

Per le informazioni dettagliare sulla configurazione e la gestione dei tuoi programmi di bilanciamento del carico globale, [fai riferimento a questo documento](glb.html#global-load-balancer-glb-concepts).

## Utilizzo delle regole della pagina per aumentare l'affidabilità

Queste sono alcune delle impostazioni della regola della pagina consigliate per fornire al tuo sito la massima affidabilità:

 * Always Online
 * Origin Cache Control
 * Forwarding URL

 ## Always Online

Puoi utilizzare l'impostazione della regola della pagina **Always Online** per conservare una versione limitata del nostro sito online se il tuo server si arresta.

Con **Always Online**, il tuo server si arresta, IBM CIS presenterà le pagine dalla nostra cache, per cui i visitatori continuano a visualizzare alcune delle pagine che stanno tentando di visitare. I tuoi visitatori visualizzeranno un messaggio all'inizio della pagina che dice loro che sono nella modalità di esplorazione offline. Always Online restituisce uno stato HTTP 503, tuttavia, 503 viene anche utilizzato da molte altre applicazioni web. Quando il tuo server torna online, IBM CIS riporterà gli utenti all'esplorazione regolare senza interruzioni.

Se IBM CIS non dispone della pagina richiesta nella sua cache, il tuo visitatore visualizza una pagina di errore che gli fa sapere che la pagina del sito web che sta richiedendo è offline.

### Come configurare Always Online

Per abilitare **Always Online**, segui questa procedura:

 * Utilizza il menu di navigazione per selezionare le regole della pagina in Performance.
 * Crea una regola della pagina con il modello dell'URL del tuo dominio.
 * Aggiungi l'impostazione **Always Online** con l'interruttore attivo.
 * Seleziona di eseguire il provisioning della risorsa.

 ### Limitazioni di Always Online

 * **Always Online** memorizza nella cache i primi 10 link dal tuo HTML principale, poi solo i primi link da ognuna delle pagine e infine i primi link di ognuna delle pagine successive. Questo significa che soltanto alcune pagine nel tuo sito saranno visualizzabili quando si arresta il tuo server di origine.

 * I siti aggiunti più recentemente non hanno una grande quantità di cache per la disponibilità del loro sito, il che significa che **Always Online** potrebbe non funzionare se hai aggiunto il sito solo pochi giorni prima.

 * CIS non è in grado di mostrare il contenuto privato o di gestire l'inoltro del modulo (POST) se il tuo server non è attivo. I visitatori visualizzeranno un errore nelle pagine di chekout o negli elementi che richiedono un accesso per la visualizzazione.

 * Per attivare **Always Online**, il tuo server web deve stare restituendo un codice di errore HTTP standard di timeout 502 o 504. Always Online funziona anche quando riscontriamo dei problemi nel contattare la tua origine (Errori 521 e 523), timeout (522 e 524), errori SSL (525 e 526) o un errore sconosciuto (520). **Always Online** non verrà attivato per altri codici di risposta HTTP come 404, 500, 503, gli errori di connessione al database, l'errore del server interno o le risposte vuote dal server.

 * **Always Online** non funziona se è abilitata una regola della pagina "Cache Everything" con "Edge Cache Expire TTL" inferiore alla frequenza di memorizzazione nella cache (Clienti gratuiti: 7 giorni, clienti Pro: 3 giorni e clienti di business e aziendali: 1 giorno), perché "Edge Cache Expire TTL" provoca che la cache di **Always Online** venga eliminata nell'intervallo corrispondente.

## Origin Cache Control

Puoi utilizzare l'impostazione della regola della pagina **Origin Cache Control** per determinare quale contenuto viene memorizzato nella cache dalla tua origine e quanto spesso viene aggiornato, che influenza l'affidabilità e le prestazioni. Per impostazione predefinita, se non viene modificata alcuna impostazione e non viene inviata alcuna intestazione che impedisce la memorizzazione nella cache dal tuo server di origine, IBM CIS memorizza nella cache tutto il contenuto statico con alcune estensioni. Questi tipi di contenuto includono immagini, CSS e JavaScript. Questa memorizzazione nella cache è principalmente per motivi legati alle prestazioni.

Per configurare il **Origin Cache Control** dovrei utilizzare le regole della pagina per attivare le intestazioni specifiche che forniscono il comportamento desiderato con il rispetto di ogni risorsa del tuo contenuto. Per comprendere come utilizzare il **Origin Cache Control**, sono necessarie alcune ulteriori spiegazioni sulle regole della pagina e sul comportamento della memorizzazione nella cache in generale di CIS per fornire il contesto, che vedrai nelle prossime sezioni. Esistono tre metodi che puoi utilizzare per controllare la memorizzazione nel cache in generale e il **Origin Cache Control** è il secondo.

L'impostazione di **Origin Cache Control** richiama le regole di memorizzazione nella cache che cercano di rispettare strettamente i RFC e le procedure consigliate internet, principalmente con il rispetto della riconvalida. Ad esempio, il comportamento predefinito di CIS con `max-age=0` è di non memorizzare nella cache, al contrario l'impostazione **Origin Cache Control** memorizza ma viene sempre riconvalidata.

### Come configurare Origin Cache Control

 * Utilizza il menu di navigazione per selezionare le regole della pagina in Performance.
 * Crea una regola della pagina con il modello dell'URL che fa riferimento al tuo dominio. 
 * Aggiungi l'impostazione **Origin Cache Control** con l'interruttore attivo.
 * Seleziona di eseguire il provisioning della risorsa.

### Precedenza della regola della pagina

Due regole della pagina specifiche hanno la precedenza per la memorizzazione nella cache generale:

 * Se una regola della pagina ha **Cache Level** impostato su `Bypass`, le risorse che corrispondono a tale regola della pagina non vengono memorizzate nella cache. IBM CIS funziona ancora come un proxy e le nostre altre funzioni delle prestazioni rimangono attive. Tuttavia, il tuo contenuto non sarà presentato dalla nostra cache, sarà richiamato direttamente dal tuo server di origine.

 * Se una regola della pagina ha **Cache Level** impostato su `Cache everything`, le risorse che corrispondono alla regola della pagina vengono memorizzate nella cache. **L'utilizzo di questa impostazione della regola della pagina è l'unico modo di farci sapere di memorizzare nella cache le risorse oltre a quelle che consideriamo statiche, incluso HTML.**

Se non viene impostata alcuna regola della pagina, utilizzeremo la modalità di memorizzazione nella cache `Standard`, che si basa sull'estensione della risorsa. Memorizzeremo nella cache solo le risorse statiche (come menzionato precedentemente).

### Intestazioni del controllo della cache dell'origine

Il secondo modo per modificare cosa IBM CIS memorizzerà nella cache è tramite le intestazioni della cache inviate dall'origine. CIS rispetterà queste impostazioni, ma puoi sovrascriverle specificando l'impostazione della regola della pagina **Edge Cache TTL**. Queste sono le intestazioni che consideriamo quando decidiamo quali risorse memorizzare nella cache dalla tua origine:

 * Se l'intestazione **Cache-Control** è impostata su `private`, `no-store`, `no-cache` o `max-age=0` o se è presente un cookie nella risposta, IBM CIS non memorizzerà nella cache la risorsa. Tieni presente che il materiale sensibile non dovrebbe essere memorizzato nella cache, per cui potresti considerare di utilizzare una di queste indicazioni in tale caso.

 * Se l'intestazione **Cache-Control** è impostata su `public` e `max-age` è maggiore di 0 o se le intestazioni `Expires` sono impostate su un valore nel futuro, memorizzeremo nella cache la risorsa.

**Nota:** come per le regole RFC, `Cache-Control: max-age` prevale sulle intestazioni `Expires`. Se vediamo entrambe e non corrispondono, prevale `max-age`.

### Utilizzo dell'intestazione 's-maxage' 

Il terzo modo di controllare il comportamento della memorizzazione nella cache e il comportamento della memorizzazione nella cache del browser è di utilizzare l'intestazione `s-maxage` Cache-Control.

Normalmente rispettiamo la direttiva `max-age`:

`Cache-Control: max-age=1000`

Ma se vuoi specificare un timeout della cache differente da quello del browser, possiamo utilizzare `s-maxage`. Questo è un esempio che indica a IBM CIS di memorizzare nella cache l'oggetto per 200 secondi e al browser per 60 secondi.

`Cache-Control: s-maxage=200, max-age=60`

Sostanzialmente `s-maxage` è progettato per essere seguito SOLO da proxy inversi (per cui il browser dovrebbe ignorarlo) mentre d'altra parte noi (IBM CIS) forniamo la priorità a `s-maxage` se presente. Rispetteremo qualsiasi valore sia il maggiore: l'impostazione della memorizzazione nella cache del browser o l'intestazione `max-age`.

### Riepilogo delle intestazioni del controllo della memorizzazione nella cache e delle regole della pagina per l'affidabilità

Per riassumere, queste sono alcune delle aree principali da considerare per l'affidabilità nei confronti della memorizzazione nella cache:

 * Controlla le intestazioni di memorizzazione nella cache della tua origine per assicurarti che non ci siano intestazioni sovrascrivibili per le risorse memorizzabili (`Cache-Control` e `Expires`).

 * CIS memorizza nella cache sempre il contenuto statico per impostazione predefinita, con il seguente TTL a seconda del codice di ritorno:

```
200 301    120m;
302 303    20m;
403        5m; for reliability
404        5m;
any        0s;
```

 * Per memorizzare nella cache altro, crea una regola della pagina con **Cache Level** impostato su "Cache everything" nell'URL desiderato (se il tuo browser web restituisce 404 durante la richiesta di questo URL, memorizzeremo nella cache questo risultato per soli 5m).

 * Per impedire la memorizzazione nella cache da un URL, crea una regola della pagina **Cache Level** impostata su "Bypass".


 ## URL di instradamento

Per assicurarti che il tuo contenuto sia sempre disponibile (HA), puoi creare una regola della pagina con l'impostazione **Forwarding URL** da utilizzare nel caso il tuo sito non sia disponibile.

 **Nota:** quando abiliti **Forwarding URL**, tutte le tue altre impostazioni vengono disabilitate perché stai inviando tutto il tuo traffico a un altro URL.

### Come configurare Forwarding URL

 * Utilizza il menu di navigazione per selezionare le regole della pagina in Performance.
 * Crea una regola della pagina con il modello dell'URL che fa riferimento al tuo dominio. 
 * Aggiungi l'impostazione **Forwarding URL**.
 * Seleziona il tipo di instradamento e immetti l'URL di destinazione.
 * Seleziona di eseguire il provisioning della risorsa.

### Esempi di instradamento:

Immagina di voler rendere più facile per chiunque raggiungere un URL come:

    *www.example.com/+

    *example.com/+

Questo modello corrisponderà a:

    http://example.com/+
    http://www.example.com/+
    https://www.example.com/+
    https://blog.example.com/+
    https://www.blog.example.com/+
    Etc...

Non corrisponderà a:

    http://www.example.com/blog/+  [extra directory before the +]
    http://www.example.com+  [no trailing slash]


Una volta che hai creato il modello che corrisponde a ciò che desideri, aggiungi l'impostazione **Forwarding URL** e seleziona il tipo di instradamento e immetti l'URL di destinazione. Ad esempio:

    https://plus.google.com/yourid

Seleziona di eseguire il provisioning della risorsa. In pochi secondi tutte le richieste che corrispondono al modello saranno instradate al nuovo URL con il reindirizzamento specificato.

### Opzioni di instradamento avanzate:

Se utilizzi un reindirizzamento di base, come un instradamento del dominio root a www.yourdomain.com, perdi qualcosa nell'URL. Ad esempio, potresti configurare il modello:

    example.com

E instradarlo a:

    http://www.example.com

Ma se qualcuno immette:

    example.com/some-particular-page.html

Sarà reindirizzato a:

    www.example.com

invece di 

    www.example.com/some-particular-page.html

La soluzione è di utilizzare le variabili. Ogni carattere jolly corrisponde a una variabile a cui può essere fatto riferimento nel seguente indirizzo. Le variabili sono rappresentate a un carattere `$` seguito da un numero. Per fare riferimento al primo carattere jolly devi utilizzare `$1`, per il secondo `$2` e così via. Per correggere l'instradamento dalla root a `www` nel precedente esempio, potrai utilizzare lo stesso modello:

    example.com/*

Dovrai quindi configurare il seguente URL per il traffico da instradare:

    http://www.example.com/$1

In questo caso, se qualcuno è andato in:

    example.com/some-particular-page.html

Sarà reindirizzato a:

    http://www.example.com/some-particular-page.html
