---
copyright:
  years: 2018
lastupdated: "2018-03-17"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gestisci la tua distribuzione di IBM Cloud Internet Services (CIS)

Inizierai utilizzando la schermata della panoramica come tua base di lavoro delle operazioni. Mostra tutti i parametri correnti della tua distribuzione.

Una volta che hai configurato il tuo DNS, sei pronto per iniziare!

## Utilizzo della schermata della panoramica

Utilizzando la schermata della panoramica, puoi visualizzare lo stato di tutte le tue selezioni. Puoi modificare le impostazioni direttamente dalla schermata della panoramica, semplicemente facendo clic sul nome sottolineato dell'impostazione che desideri modificare, ad esempio, potresti fare clic sul campo `Load Balancers` per aggiungere un programma di bilanciamento del carico.

Nella schermata della panoramica, puoi visualizzare che la tua configurazione del nome del dominio è nello stato **Pending** o **Active** come illustrato nella seguente figura.

![immagine schermata panoramica](images/overview-screen-configuration-summary.png)


## Configurazione e gestione del DNS

Vai alla pagina DNS per aggiungere un record (molto probabilmente un record A). Immetti le informazioni sul tuo record DNS e poi fai clic su `Add record` per implementare le tue modifiche.

![aggiungi-DNS](images/dns/create-a-type-record.png)

## Configura e gestisci la tua memorizzazione nella cache

Successivamente, puoi configurare la memorizzazione nella cache. 

![IMMAGINE](images/caching-screen.png)

Hai l'opzione di 3 tipi di memorizzazione nella cache, disponibili dal menu a discesa della schermata della memorizzazione nella cache: 

 * Nessuna stringa di query :  fornisce le risorse dalla cache solo quando non è presente alcuna stringa di query.
 * Indipendente dalla stringa di query : fornisce la stessa risorsa a chiunque indipendentemente dalla stringa di query. (Nota: l'impostazione **Ignore Query String** si applica solo alle estensioni dei file statici. Questa impostazione rimuove la stringa di query durante la generazione della chiave della cache, per cui una richiesta di `style.css?something` viene normalizzata con `style.css` quando utilizzata dalla cache.)
 * Dipendente dalla stringa di query : fornisce una risorsa differente ogni volta che viene modificata la stringa di query.
  
## Pulisci la cache
 
Puoi pulire la tua cache per preparare gli aggiornamenti in qualsiasi momento, immetti soltanto l'URL nel campo di pulizia della cache. Puoi pulire uno o più file (fino a 30 alla volta).
 
 ## Scadenza del browser
 
Puoi utilizzare il menu a discesa per selezionare l'ora di scadenza del browser di cui hai bisogno, ad esempio 98 ore o 1 giorno.
 
 ## Utilizzo della modalità di sviluppo
 
La **modalità di sviluppo** è pensata per l'utilizzo quando sono richiesti aggiornamenti principali o nuovi caricamenti di file o ogni volta che non vuoi che gli utenti finali utilizzino la cache, ma per richiamare i file direttamente dai server di origine. Per iniziare ad utilizzare la **modalità di sviluppo**, sposta lo switch sulla posizione `Enabled`. Per interrompere l'utilizzo della **modalità di sviluppo**, sposta lo switch sulla posizione `Disabled`. La **modalità di sviluppo** scade automaticamente dopo 3 ore. 

## Gestione delle tue regole della pagina
 
Puoi abilitare fino a 50 regole della pagina. Utilizza i menu a discesa per configurare la regola della pagina. Le impostazioni della regola sono divise in tre categorie: **Security**, **Performance** e **Reliability**.

Tieni presente che quando vengono abilitate alcune regole, altre opzioni vengono disabilitate, se sono in conflitto con le altre regole che hai appena selezionato. Dopo aver selezionato le regole della pagina che desideri, fai clic su **Provision** per abilitarle. Le nuove regole hanno immediatamente effetto e possono essere subito visualizzate nella schermata delle regole della pagina.
 
 ![MENU REGOLE PAGINA](images/page-rule-dropdown-settings.png)
 
Puoi anche abilitare o disabilitare le tue regole della pagina dalla tabella visualizzata nella schermata Page Rules. Per ulteriori informazioni, consulta [Utilizzo delle regole della pagina](using-page-rules.html).
 
 ## Impostazioni di sicurezza
 
Per impostazione predefinita, la protezione DDoS è abilitata per tutti i record DNS con il proxy attivo, che può essere effettuato dalla tabella **Records** nella pagina DNS. Attiva WAF utilizzando l'interruttore. Quando attivi/disattivi le regole, le modifiche vengono applicate immediatamente.

![IMMAGINE](images/ddos-waf-ssl-screen.png)

## Certificati

Quando distribuisci in una zona, IBM CIS distribuisce automaticamente un certificato universale per tale zona. Pertanto, non hai bisogno di fare nulla per avere la protezione basata sul certificato in tale zona. Se lo desideri, puoi caricare il tuo certificato. Avrai bisogno di un certificato diverso per ogni zona e visualizzerai un messaggio di errore se il certificato che stai caricando non corrisponde alla tua zona.

![IMMAGINE](images/certificates-table.png)
 
 ## Configura i tuoi programmi di bilanciamento del carico
 
 IBM CIS fornisce il bilanciamento del carico globale come un servizio. 

![IMMAGINE](images/glb-screen.png)

### Dashboard GLB
Nel tuo dashboard, visualizzerai tre elenchi che mostrano i programmi di bilanciamento del carico, i pool di origini e i controlli di integrità. Gli elenchi visualizzano il programma di bilanciamento del carico globale nuovo o aggiornato o uno dei suoi componenti dopo che ne avrai eseguito il provisioning o lo avrai aggiornato. Inizialmente gli elenchi sono vuoti e prima di creare un programma di bilanciamento del carico devi effettuare alcune azioni.

#### Crea
**Nota**: <sup>`*`</sup> indica che questo passo è facoltativo

1) <sup>`*`</sup>Crea un controllo di integrità, fai clic su "Create health check".
  ![IMMAGINE](images/glb-health-check-list.png)
    <ul>
      <li>* **Percorso**: il percorso endpoint del controllo di integrità.</li> 
      <li>* **Tipo**: il protocollo da utilizzare per il controllo di integrità.</li>
      <li>* **Descrizione**: la descrizione fornita dall'utente.</li>
    </ul>

2) Crea un pool, fai clic su "Create pool".
  ![IMMAGINE](images/glb-pool-list.png)
    <ul>
      <li>* **Integrità**: lo stato del pool.</li>
      <li>* **Nome**: il nome fornito dall'utente.</li>
      <li>* **Origini**: il numero di origini di integrità nel pool.</li>
      <li>* **Controllo di integrità**: il percorso del controllo di integrità collegato, se presente.</li>
    </ul>

3) Crea un programma di bilanciamento del carico, fai clic su "Create load balancer".
  ![IMMAGINE](images/glb-load-balancer-list.png)
    <ul>
      <li>* **Integrità**: lo stato del programma di bilanciamento del carico.</li>
      <li>* **Nome host**: il nome anteposto al nome del dominio.</li>
      <li>* **Pool disponibili**: il numero di pool integri.</li>
      <li>* **TTL**: TTL (Time To Live).</li>
      <li>* **Proxy**: abilita o disabilita il flusso del traffico proxy.</li>
      <li>* **Stato**: abilita o disabilita il programma di bilanciamento del carico.</li>
    </ul>

#### Modifica/Elimina
Per modificare o eliminare un programma di bilanciamento del carico o uno dei suoi componenti, fai clic sul pulsante del menu di overflow ubicato in alto a destra di ogni riga.

Pulsante menu di overflow: 

![IMMAGINE](images/overflow.png)

Le seguenti opzioni sono fornite per ogni elenco.

* Controllo di integrità
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

### Aggiungi un controllo di integrità 

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

### Aggiungi un pool

È necessario almeno un pool per ogni programma di bilanciamento del carico fornito. I pool raggruppano le tue origini del programma di bilanciamento del carico da utilizzare.

Quando crei un pool, sono obbligatori due campi:
 * **Nome**: un nome breve (tag) del pool. Sono consentiti solo caratteri alfanumerici, trattini e caratteri di sottolineatura.
 * **Origini**: l'elenco delle origini in questo pool. Il traffico diretto a questo pool è bilanciato tra tutte le origini attualmente integre, se il pool stesso è integro.

Ulteriori campi facoltativi: 
 * **Descrizione**: una descrizione leggibile dall'utente del pool.
 * **Abilitato**: se abilitare (impostazione predefinita) questo pool. I pool disabilitati non ricevono il traffico e vengono esclusi dai controlli di integrità. La disabilitazione di un pool provoca il failover al pool successivo di tutti i programmi di bilanciamento del carico che lo utilizzano, se presente (il valore predefinito è true).
 * **Soglia origine integra**: il numero minimo di origini che devono essere integre per questo pool per assicurare il traffico. Se il numero di origini integre scende al di sotto di questo numero, il pool viene contrassegnato come non integro ed eseguirà il failover al pool disponibile successivo. (il valore predefinito è 1)
 * **Regioni del controllo di integrità**: la regione da cui il controllo di integrità eseguirà il monitoraggio.
 * **Controllo di integrità**: il controllo di integrità da utilizzare per la verifica delle origini all'interno di questo pool. (il valore predefinito è nessun controllo)
 * **Email di notifica**: l'indirizzo email che dovrebbe ricevere le notifiche sullo stato di integrità. Questo indirizzo può essere una casella di posta individuale o una lista di distribuzione.

 ### Aggiungi un programma di bilanciamento del carico

I programmi di bilanciamento del carico ti aiutano a distribuire il tuo traffico tramite proxy tra più pool di origini utilizzando una distribuzione round-robin.

Quando crei un programma di bilanciamento del carico, i campi obbligatori sono:
 * **Nome**: il nome host DNS da associare al tuo programma di bilanciamento del carico. Se questo nome host già esiste come un record DNS nel DNS di IBM, il programma di bilanciamento del carico ha la precedenza e il record DNS non sarà utilizzato.
 * **Pool predefiniti**: un elenco di ID pool. L'elenco è ordinato per la loro priorità di failover. I pool definiti qui sono utilizzati per impostazione predefinita o quando i pool della regione non sono configurati per una regione selezionata.

Facoltativamente, possono essere configurati i seguenti campi:
 * **Proxy**: instrada il traffico tramite il servizio delle metriche e delle prestazioni di IBM.
 * **Affinità della sessione**: instrada sempre tramite la stessa istanza delle metriche e delle prestazioni. Questa opzione è disponibile solo se è abilitato il proxy.
 * **TTL**: il TTL (Time to live) della voce DNS per l'indirizzo IP restituito da questo programma di bilanciamento del carico. Questa opzione si applica solo ai programmi di bilanciamento del carico senza proxy, altrimenti viene impostata in modo predefinito su `Automatic`.
 * **Pool della regione**: un'associazione di codici paese e regione a un elenco di pool (ordinato per la loro priorità di failover) di una regione selezionata. Tutte le regioni non definite in modo esplicito torneranno ad utilizzare i pool predefiniti.
