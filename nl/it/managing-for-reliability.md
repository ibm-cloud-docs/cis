---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Page Rules, web content, IBM CIS deployment

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Gestisci la tua distribuzione IBM CIS per l'affidabilità ottimale
{:manage-your-ibm-cis-deployment-for-optimal-reliability}

Per raggiungere l'affidabilità ottimale per la tua distribuzione IBM CIS, puoi configurare una configurazione DNS utile e i Load Balancers globale. Per maggiore affidabilità, puoi utilizzare le nostre regole della pagina per assicurarti che il tuo contenuto web sia distribuito ai tuoi clienti, anche se il tuo server di origine o la cache ha un problema. Questo documento fornisce i dettagli su alcune procedure consigliate per rendere la tua distribuzione IBM CIS affidabile in modo ottimale.

Generalmente, le nostre procedure consigliate sono queste:

 * Configura il tuo DNS per usufruire dei vantaggi dei server proxy e di altre funzioni di IBM CIS
 * Utilizza uno o più Load Balancers globale per distribuire il tuo traffico del sito uniformemente
 * Configura le regole della pagina appropriate per gestire la tua memorizzazione nella cache e altre opzioni

Ognuno di questi elementi fornisce alcune funzionalità che puoi utilizzare per creare una distribuzione CIS più affidabile.

Tieni presente che l'interfaccia CIS è organizzata in sezioni per *security*, *reliability* e *performance*. Il menu di navigazione principale viene illustrato nella seguente figura, con gli elementi del menu DNS e i Load Balancers globale mostrati:

![DNS navigazione sinistra ](images/cis-left-navigation.png)


## Configurazione del DNS
{:#setting-up-dns}
 
 Per iniziare l'impostazione della tua configurazione DNS, seleziona **DNS** dal menu di navigazione, come mostrato precedentemente.
 
 Per informazioni dettagliate sulla configurazione e la gestione dell'affidabilità del tuo DNS, [fai riferimento a questo documento](/docs/infrastructure/cis?topic=cis-set-up-your-domain-name-system-dns-for-ibm-cis). 


## Configurazione dei Load Balancers globale
{:#setting-up-glb}


Per iniziare la configurazione dei tuoi Load Balancers globale, seleziona **Global Load Balancers** dal menu di navigazione.

Per informazioni dettagliate sulla configurazione e la gestione dei tuoi GLB, [fai riferimento a questo documento](/docs/infrastructure/cis?topic=cis-global-load-balancer-glb-concepts).

## Utilizzo delle regole della pagina per aumentare l'affidabilità
{:#using-page-rules-to-increase-reliability}

Queste sono alcune delle impostazioni della regola della pagina consigliate per fornire al tuo sito la massima affidabilità:

 * Serve Stale Content
 * Origin Cache Control
 * Forwarding URL

## Serve Stale Content
{:#serve-stale-content}

Puoi utilizzare l'impostazione della regola della pagina **Serve Stale Content** per conservare una versione limitata del nostro sito online se il tuo server si arresta. 

Con **Serve Stale Content**, quando il tuo server si arresta, IBM CIS presenterà le pagine provenienti dalla nostra cache, quindi i tuoi visitatori visualizzeranno ancora alcune delle pagine che stanno tentando di visitare. I tuoi visitatori vedranno un messaggio all'inizio della pagina che dice loro che sono nella modalità di esplorazione offline. Serve Stale Content restituisce uno stato HTTP 503, tuttavia, 503 viene anche utilizzato da molte altre applicazioni web. Quando il tuo server torna online, IBM CIS riporterà gli utenti all'esplorazione regolare senza interruzioni.

Se IBM CIS non dispone della pagina richiesta nella sua cache, il tuo visitatore visualizza una pagina di errore che gli fa sapere che la pagina del sito web che sta richiedendo è offline.

### Come configurare Serve Stale Content
{:#setting-up-serve-stale-content}
Per abilitare **Serve Stale Content**, segui questi passi:

 * Utilizza il menu di navigazione per selezionare le regole della pagina in Performance.
 * Crea una regola della pagina con il modello dell'URL del tuo dominio.
 * Aggiungi l'impostazione **Serve Stale Content** con l'interruttore attivo. 
 * Seleziona di eseguire il provisioning della risorsa.

### Limitazioni di Serve Stale Content
{limitations-serve-stale-content}

 * **Serve Stale Content** memorizza nella cache i primi 10 link dal tuo HTML root, poi solo i primi link da ognuna di quelle pagine e infine i primi link di ognuna delle pagine successive. Questo significa che soltanto alcune pagine nel tuo sito saranno visualizzabili quando si arresta il tuo server di origine. 

 * I siti aggiunti recentemente non hanno una grande quantità disponibile di cache del loro sito, ciò significa che **Serve Stale Content** potrebbe non funzionare se hai aggiunto il sito solo pochi giorni prima. 

 * CIS non mostra contenuto privato o gestisce l'inoltro del modulo (POST) se il tuo server è inattivo. Ai visitatori viene mostrata una pagina `error on checkout` o `items require a login to view`.

 * Per attivare **Serve Stale Content**, il tuo server web deve restituire un codice di errore HTTP standard 502 o 504 di timeout. Serve Stale Content funziona anche quando riscontriamo problemi nel contattare la tua origine (Errore 521 e 523), timeout (522 e 524), errori SSL (525 e 526) o un errore sconosciuto (520). **Serve Stale Content** non viene attivato per altri codici di risposta HTTP, ad esempio 404, 500, 503, errori di connessione al database, errore server interno o risposte vuote dal server.

 * **Serve Stale Content** non funziona se viene abilitata una regola della pagina "Cache Everything" con "Edge Cache Expire TTL" inferiore alla frequenza di memorizzazione nella cache, perché "Edge Cache Expire TTL" fa in modo che il contenuto della cache di **Serve Stale Content** venga eliminato dalla cache nell'intervallo corrispondente. 

## Origin Cache Control
{:#origin-cache-control}
Puoi utilizzare l'impostazione della regola della pagina **Origin Cache Control** per determinare quale contenuto viene memorizzato nella cache dalla tua origine e quanto spesso viene aggiornato, che influenza l'affidabilità e le prestazioni. Per impostazione predefinita, se non viene modificata alcuna impostazione e non viene inviata alcuna intestazione che impedisce la memorizzazione nella cache dal tuo server di origine, IBM CIS memorizza nella cache tutto il contenuto statico con alcune estensioni. Questi tipi di contenuto includono immagini, CSS e JavaScript. Questa memorizzazione nella cache è principalmente per motivi legati alle prestazioni.

Per configurare **Origin Cache Control**, utilizza le regole della pagina per attivare specifiche intestazioni che forniscono il comportamento desiderato riguardo a ciascuna risorsa del contenuto. Per comprendere come utilizzare **Origin Cache Control**, è necessaria qualche spiegazione generale sulle regole della pagina e sul comportamento generale della memorizzazione nella cache per CIS per fornire un contesto, tali argomenti verranno trattati nelle prossime sezioni. Esistono tre metodi che puoi utilizzare per controllare la memorizzazione nel cache in generale e **Origin Cache Control** è il secondo.

L'impostazione di **Origin Cache Control** richiama le regole di memorizzazione nella cache che cercano di rispettare strettamente i RFC e le procedure consigliate internet, principalmente con il rispetto della riconvalida. Ad esempio, il comportamento predefinito di CIS con `max-age=0` è di non memorizzare nella cache, al contrario l'impostazione **Origin Cache Control** memorizza ma viene sempre riconvalidata.

### Come configurare Origin Cache Control
{:#setting-up-origin-cache-control}

 * Utilizza il menu di navigazione per selezionare le regole della pagina in Performance.
 * Crea una regola della pagina con il modello dell'URL che fa riferimento al tuo dominio.
 * Aggiungi l'impostazione **Origin Cache Control** con l'interruttore attivo.
 * Seleziona di eseguire il provisioning della risorsa.

### Precedenza della regola della pagina
{:#page-rule-precedence}

Due regole della pagina specifiche hanno la precedenza per la memorizzazione nella cache generale:

 * Se una regola della pagina ha **Cache Level** impostato su `Bypass`, le risorse che corrispondono a tale regola della pagina non vengono memorizzate nella cache. IBM CIS funziona ancora come un proxy e le nostre altre funzioni delle prestazioni rimangono attive. Tuttavia, il tuo contenuto viene richiamato direttamente dal tuo server di origine invece di essere presentato dalla nostra cache. 

 * Se una regola della pagina ha **Cache Level** impostato su `Cache everything`, le risorse che corrispondono alla regola della pagina vengono memorizzate nella cache. **L'utilizzo di questa impostazione della regola della pagina è l'unico modo di farci sapere di memorizzare nella cache le risorse oltre a quelle che consideriamo statiche, incluso HTML.**

Se non viene impostata alcuna regola della pagina, utilizziamo la modalità di memorizzazione nella cache `Standard`, che si basa sull'estensione della risorsa. Memorizziamo nella cache solo risorse statiche. 

### Intestazioni del controllo della cache dell'origine
{:#origin-cache-control-headers}

Il secondo modo per modificare cosa IBM CIS memorizza nella cache, è quello tramite le intestazioni della memorizzazione nella cache inviate dall'origine. CIS rispetta queste impostazioni, ma puoi sovrascriverle specificando l'impostazione della regola della pagina **Edge Cache TTL**. Queste sono le intestazioni che consideriamo quando decidiamo quali risorse memorizzare nella cache dalla tua origine:

 * Se l'intestazione **Cache-Control** è impostata su `private`, `no-store`, `no-cache` o `max-age=0` o se è presente un cookie nella risposta, IBM CIS non memorizzerà nella cache la risorsa. Tieni presente che il materiale sensibile non dovrebbe essere memorizzato nella cache, per cui potresti considerare di utilizzare una di queste indicazioni in tale caso.

 * Se l'intestazione **Cache-Control** è impostata su `public` e `max-age` è maggiore di 0 o se le intestazioni `Expires` sono impostate su un valore nel futuro, memorizzeremo nella cache la risorsa.

**Nota:** come per le regole RFC, `Cache-Control: max-age` prevale sulle intestazioni `Expires`. Se vediamo entrambe e non corrispondono, prevale `max-age`.

### Utilizzo dell'intestazione 's-maxage'
{:#using-the-s-maxage-header}

Il terzo modo di controllare il comportamento della memorizzazione nella cache e il comportamento della memorizzazione nella cache del browser è di utilizzare l'intestazione `s-maxage` Cache-Control.

Normalmente rispettiamo la direttiva `max-age`:

`Cache-Control: max-age=1000`

Ma se vuoi specificare un timeout della cache diverso da quello del browser, possiamo utilizzare `s-maxage`. Questo è un esempio che indica a IBM CIS di memorizzare nella cache l'oggetto per 200 secondi e al browser per 60 secondi.

`Cache-Control: s-maxage=200, max-age=60`

Sostanzialmente `s-maxage` è progettato per essere seguito SOLO da proxy inversi (per cui il browser dovrebbe ignorarlo) mentre d'altra parte noi (IBM CIS) diamo la priorità a `s-maxage` se presente. Rispettiamo qualunque valore sia più elevato: l'impostazione della memorizzazione nella cache del browser o l'intestazione `max-age`.

### Riepilogo delle intestazioni del controllo della memorizzazione nella cache e delle regole della pagina per l'affidabilità
{:#summary-cache-control-headers-page-rules}

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

 * Per memorizzare altro nella cache, crea una regola della pagina con **Cache Level** impostato su `Cache everything` nell'URL desiderato (se il tuo server web restituisce un 404 alla richiesta di questo URL, memorizzeremo nella cache questo risultato solo per 5m).

 * Per impedire la memorizzazione nella cache in un URL, crea una regola della pagina con **Cache Level** impostato su `Bypass`.


## Forwarding URL
{:#forwarding-url}

Per assicurarti che il tuo contenuto sia sempre disponibile, crea una regola della pagina con l'impostazione **Forwarding URL** da utilizzare nel caso in cui il tuo sito non sia disponibile. 

Quando abiliti **Forwarding URL**, tutte le tue altre impostazioni vengono disabilitate perché stai inviando tutto il tuo traffico a un altro URL.
{:note}

### Come configurare Forwarding URL
{:#setting-up-forwarding-url}

 * Utilizza il menu di navigazione per selezionare le regole della pagina in Performance.
 * Crea una regola della pagina con il modello dell'URL che fa riferimento al tuo dominio.
 * Aggiungi l'impostazione **Forwarding URL**.
 * Seleziona il tipo di instradamento e immetti l'URL di destinazione.
 * Seleziona di eseguire il provisioning della risorsa.

### Esempi di instradamento
{:#forwarding-examples}

Immagina di voler rendere più facile per chiunque raggiungere un URL come:

    *www.example.com/+

    *example.com/+

Questo modello corrisponde a:

    http://example.com/+
    http://www.example.com/+
    https://www.example.com/+
    https://blog.example.com/+
    https://www.blog.example.com/+
    Etc...

Non corrisponde a:

    http://www.example.com/blog/+  [extra directory before the +]
    http://www.example.com+  [no trailing slash]


Una volta che hai creato il modello che corrisponde a ciò che desideri, aggiungi l'impostazione **Forwarding URL** e seleziona il tipo di instradamento e immetti l'URL di destinazione. Ad esempio:

    https://plus.google.com/yourid

Seleziona di eseguire il provisioning della risorsa. In pochi secondi tutte le richieste che corrispondono al modello vengono instradate al nuovo URL con il reindirizzamento specificato. 

### Opzioni di instradamento avanzate
{:#advanced-forwarding-options}

Se utilizzi un reindirizzamento di base, come un instradamento del dominio root a `www.yourdomain.com`, perdi qualsiasi altra cosa nell'URL. Ad esempio, potresti configurare il modello:

    example.com

E instradarlo a:

    `http://www.example.com`

Ma se qualcuno immette:

    `example.com/some-particular-page.html`

Viene reindirizzato a:

    `www.example.com`

invece di

    `www.example.com/some-particular-page.html`

La soluzione è di utilizzare le variabili. Ogni carattere jolly corrisponde a una variabile a cui può essere fatto riferimento nel seguente indirizzo. Le variabili sono rappresentate da un carattere `$` seguito da un numero. Per fare riferimento al primo carattere jolly devi utilizzare `$1`, per il secondo `$2` e così via. Per correggere l'instradamento dalla root a `www` nell'esempio precedente, utilizziamo lo stesso modello:

    `example.com/*`

Quindi configura il seguente URL a cui instradare il traffico:

    `http://www.example.com/$1`

In questo caso, se qualcuno è andato in:

    `example.com/some-particular-page.html`

Viene reindirizzato a:

    `http://www.example.com/some-particular-page.html`
