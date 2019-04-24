---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: health checks, origin pools, load balancers, IBM CIS

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Configura i tuoi programmi di bilanciamento del carico
{:#set-up-and-configure-your-load-balancers}
 
 IBM CIS fornisce il bilanciamento del carico globale come un servizio. Ecco che aspetto ha il dashboard GLB:

![IMMAGINE](images/glb-screen.png)

## Dashboard GLB
{:#glb-dashboard}

Nel tuo dashboard, visualizzerai tre elenchi che mostrano i programmi di bilanciamento del carico, i pool di origini e i controlli di integrità. Gli elenchi visualizzano il programma di bilanciamento del carico globale nuovo o aggiornato o uno dei suoi componenti dopo che ne avrai eseguito il provisioning o lo avrai aggiornato. Inizialmente gli elenchi sono vuoti e prima di creare un programma di bilanciamento del carico devi effettuare alcune azioni.

Fai riferimento a [Quick Start Guide](/docs/infrastructure/cis?topic=cis-global-load-balancer-quick-setup) se sai già cosa devi fare. 

### Crea
{:#create-health-check}

<sup>`*`</sup> indica che questo passo è facoltativo
{:note}

1) <sup>`*`</sup>Crea un controllo di integrità, fai clic su **Create health check**.
  ![IMMAGINE](images/glb-health-check-list.png)
    <ul>
      <li><b>Percorso</b>: il percorso endpoint del controllo di integrità.</li> 
      <li><b>Tipo</b>: il protocollo da utilizzare per il controllo di integrità.</li>
      <li><b>Descrizione</b>: la descrizione fornita dall'utente.</li>
    </ul>

2) Crea un pool, fai clic su **Create pool**.
  ![IMMAGINE](images/glb-pool-list.png)
    <ul>
      <li><b>Integrità</b>: lo stato del pool.</li>
      <li><b>Nome</b>: il nome fornito dall'utente.</li>
      <li><b>Origini</b>: il numero di origini di integrità nel pool.</li>
      <li><b>Controllo di integrità</b>: il percorso del controllo di integrità collegato, se presente.</li>
    </ul>

3) Crea un programma di bilanciamento del carico, fai clic su **Create load balancer**.
  ![IMMAGINE](images/glb-load-balancer-list.png)
    <ul>
      <li><b>Integrità</b>: lo stato del programma di bilanciamento del carico.</li>
      <li><b>Nome host</b>: il nome anteposto al nome del dominio.</li>
      <li><b>Pool disponibili</b>: il numero di pool integri.</li>
      <li><b>TTL</b>: TTL (Time To Live).</li>
      <li><b>Proxy</b>: abilita o disabilita il flusso del traffico proxy.</li>
      <li><b>Stato</b>: abilita o disabilita il programma di bilanciamento del carico.</li>
    </ul>

Le regioni geografiche di IBM sono diverse dalle regioni di Cloudflare. Per dettagli sulle regioni geografiche utilizzate da Cloudflare, vedi [Load Balancing: Geographic Regions ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://support.cloudflare.com/hc/en-us/articles/115000540888-Load-Balancing-Geographic-Regions){:new_window}.  
{:note}

### Modifica/Elimina
{:#edit-delete-load-balancer}
Per modificare o eliminare un programma di bilanciamento del carico o uno dei suoi componenti, fai clic sul pulsante del menu di overflow ubicato in alto a destra di ogni riga.

Pulsante menu di overflow:

![IMMAGINE](images/overflow.png)

Le seguenti opzioni sono fornite per ogni elenco.

* Controllo di integrità
    * **Visualizza controllo di integrità**: questa opzione mostra un breve riepilogo del controllo di integrità, con un link che ti porta al flusso di modifica. 
    * **Modifica controllo di integrità**: questa opzione reindirizza l'utente al flusso di modifica. 
    * **Elimina controllo di integrità**: questa opzione visualizza la finestra di dialogo di conferma per l'eliminazione del flusso.

* Pool
    * **Visualizza dettagli pool**: questa opzione porta a una finestra di dialogo modale con le informazioni sul pool.
    * **Modifica pool**: questa opzione reindirizza l'utente al flusso di modifica.
    * **Elimina pool**: questa opzione visualizza la finestra di dialogo di conferma per l'eliminazione del flusso.

* Programma di bilanciamento del carico
    * **Abilita/disabilita**: abilita o disabilita un programma di bilanciamento del carico.
    * **Modifica programma di bilanciamento del carico**: reindirizza al flusso di modifica. 
    * **Elimina programma di bilanciamento del carico**: visualizza la finestra di dialogo di conferma per l'eliminazione del flusso.

## Aggiungi un controllo di integrità
{:#add-a-health-check}

I controlli di integrità sono allegati facoltativi dei pool di origini. Utilizzano un intervallo di ripetizione per analizzare un corpo della risposta specifico o per un codice di stato, per monitorare l'integrità del pool. Una volta creati, i controlli di integrità vengono aggiunti a un nuovo o esistente pool di origini.

Quando crei un controllo di integrità, è obbligatorio solo un campo:
 * **Codice di risposta**: il codice di risposta HTTP previsto o l'intervallo di codici del controllo di integrità. Questo valore deve essere compreso tra 200 e 299 con i caratteri jolly indicati da una 'x'.

Ulteriori campi facoltativi:
 * **Percorso**: il percorso endpoint con cui eseguire il controllo di integrità (il valore predefinito è /).
 * **Tipo**: il protocollo da utilizzare per il controllo di integrità (il valore predefinito è HTTP).
 * **Descrizione**: la descrizione del controllo di integrità.
 * **Intervallo**: l'intervallo (in secondi) tra ciascun controllo di integrità. Intervalli più brevi possono migliorare il tempo di failover, ma incrementano il carico sulle origini poiché viene eseguito il controllo da più ubicazioni (il valore predefinito è 60).
 * **Metodo**: il metodo HTTP da utilizzare per il controllo di integrità (il valore predefinito è GET).
 * **Timeout**: il tempo (in secondi) prima di contrassegnare il controllo di integrità come non riuscito (il valore predefinito è 5).
 * **Tentativi**: il numero di tentativi da effettuare nel caso di un timeout prima di contrassegnare l'origine come non integra. I tentativi vengono effettuati immediatamente (il valore predefinito è 2).
 * **Corpo della risposta**: una stringa secondaria non sensibile al maiuscolo/minuscolo per la corrispondenza nel corpo della risposta. Se questa stringa non viene trovata, l'origine viene contrassegnata come non integra.
 * **Intestazioni della richiesta**: le intestazioni della richiesta HTTP da inviare nel controllo di integrità. Si consiglia di configurare un'intestazione host per impostazione predefinita. L'intestazione `User-Agent` non può essere sovrascritta.

## Aggiungi un pool
{:#add-a-pool}

È necessario almeno un pool per ogni programma di bilanciamento del carico fornito. I pool raggruppano le tue origini del programma di bilanciamento del carico da utilizzare.

Quando crei un pool, sono obbligatori due campi:
 * **Nome**: un nome breve (tag) del pool. Sono consentiti solo caratteri alfanumerici, trattini e caratteri di sottolineatura.
 * **Origini**: l'elenco delle origini in questo pool. Il traffico diretto a questo pool è bilanciato tra tutte le origini attualmente integre, se il pool stesso è integro.

Ulteriori campi facoltativi:
 * **Descrizione**: una descrizione leggibile dall'utente del pool.
 * **Abilitato**: se abilitare (impostazione predefinita) questo pool. I pool disabilitati non ricevono il traffico e vengono esclusi dai controlli di integrità. La disabilitazione di un pool provoca il failover al pool successivo di tutti i programmi di bilanciamento del carico che lo utilizzano, se presente (il valore predefinito è true).
 * **Soglia origine integra**: il numero minimo di origini che devono essere integre per questo pool per assicurare il traffico. Se il numero di origini integre scende al di sotto di questo numero, il pool viene contrassegnato come non integro ed eseguirà il failover al pool disponibile successivo. (il valore predefinito è 1)
 * **Regioni del controllo di integrità**: la regione da cui il controllo di integrità eseguirà il monitoraggio. **Nota**: le regioni geografiche di IBM sono diverse dalle regioni di Cloudflare. Per dettagli sulle regioni geografiche utilizzate da Cloudflare, vedi [Load Balancing: Geographic Regions ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://support.cloudflare.com/hc/en-us/articles/115000540888-Load-Balancing-Geographic-Regions){:new_window}. 
 * **Controllo di integrità**: il controllo di integrità da utilizzare per la verifica delle origini all'interno di questo pool. (il valore predefinito è nessun controllo)
 * **Email di notifica**: l'indirizzo email che dovrebbe ricevere le notifiche sullo stato di integrità. Questo indirizzo può essere una casella di posta individuale o una lista di distribuzione.

## Aggiungi un programma di bilanciamento del carico
{:#add-a-load-balancer}

I programmi di bilanciamento del carico ti aiutano a distribuire il tuo traffico tramite proxy tra più pool di origini utilizzando una distribuzione round-robin.

Quando crei un programma di bilanciamento del carico, i campi obbligatori sono:
 * **Nome**: il nome host DNS da associare al tuo programma di bilanciamento del carico. Se questo nome host già esiste come un record DNS nel DNS di IBM, il programma di bilanciamento del carico ha la precedenza e il record DNS non sarà utilizzato.
 * **Pool predefiniti**: un elenco di ID pool. L'elenco è ordinato per la loro priorità di failover. I pool definiti qui sono utilizzati per impostazione predefinita o quando i pool della regione non sono configurati per una regione selezionata.

Facoltativamente, possono essere configurati i seguenti campi:
 * **Proxy**: instrada il traffico tramite il servizio delle metriche e delle prestazioni di IBM.
 * **Affinità della sessione**: instrada sempre tramite la stessa istanza delle metriche e delle prestazioni. Questa opzione è disponibile solo se è abilitato il proxy.
 * **TTL**: il TTL (Time to live) della voce DNS per l'indirizzo IP restituito da questo programma di bilanciamento del carico. Questa opzione si applica solo ai programmi di bilanciamento del carico senza proxy, altrimenti viene impostata in modo predefinito su `Automatic`.
 * **Pool della regione**: un'associazione di codici paese e regione a un elenco di pool (ordinato per la loro priorità di failover) di una regione selezionata. Tutte le regioni non definite in modo esplicito torneranno ad utilizzare i pool predefiniti. **Nota**: le regioni geografiche di IBM sono diverse dalle regioni di Cloudflare. Per dettagli sulle regioni geografiche utilizzate da Cloudflare, vedi [Load Balancing: Geographic Regions ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://support.cloudflare.com/hc/en-us/articles/115000540888-Load-Balancing-Geographic-Regions){:new_window}. 
 
Per le definizioni dei termini utilizzati in questo documento, che generalmente sono termini comuni utilizzati nel settore, fai riferimento al [Glossario](/docs/infrastructure/cis?topic=cis-glossary).
