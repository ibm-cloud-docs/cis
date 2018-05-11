---
  
copyright:
   years: 2018
lastupdated: "2018-03-16"
 
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Gestisci la tua distribuzione CIS per prestazioni ottimali

IBM Cloud Internet Services (CIS) può fornire l'esperienza più veloce ai tuoi clienti perché ottimizza le tue immagini e archivia il tuo contenuto web il più vicino possibile ai tuoi utenti finali. Il tuo contenuto viene caricato dai server perimetrali con proxy (che riduce la latenza).

Con IBM CIS, puoi ulteriormente migliorare le prestazioni del tuo sito utilizzando le procedure consigliate per velocizzare il caricamento del tuo contenuto web. Queste sono alcune delle procedure consigliate per il miglioramento delle prestazioni del tuo contenuto web all'interno di CIS.

**Consigli e procedure consigliate:**

 * Memorizza nella cache la maggior parte del tuo contenuto web statico e semi statico.
 * Per il contenuto guidato dagli eventi, pulisci la tua cache utilizzando l'API.
 
## Procedura consigliata 1: memorizza nella cache la maggior parte del contenuto statico e semi statico 

  * Abilita **Cache Everything** per le pagine web HTML statiche
  * Utilizza il **Time to Live (TTL)** tradizionale per il tuo contenuto che viene modificato occasionalmente

### Utilizza i TTL (Time-to-Live) tradizionali per il contenuto che viene modificato occasionalmente
Se il contenuto viene modificato raramente, puoi configurare un TTL tradizionale per utilizzare la nostra cache il più possibile. Se hai un'alta percentuale di richieste di riconvalida, potresti incrementare i TTL del tuo contenuto senza influenzare negativamente i tuoi clienti. Utilizzando la cache in modo più efficace, aumenterai le prestazioni perché dovrai eseguire la riconvalida meno spesso.

### Come faccio a sapere se i miei elementi stanno venendo memorizzati nella cache?
IBM CIS aggiunge l'intestazione di risposta `CF-Cache-Status` quando tenta di memorizzare nella cache un oggetto. Se la memorizzazione nella cache ha esito positivo, il valore di questa intestazione indica il suo stato con una di queste parole chiave:

* **MISS:** la risorsa non è ancora stata memorizzata nella cache o il TTL è scaduto (ovvero, ha raggiunto il numero massimo di giorni di controllo della cache di 0).
* **HIT:** la risorsa è stata distribuita dalla cache.
* **EXPIRED:** questa risorsa era stata distribuita dalla cache, ma la richiesta successiva richiederà una riconvalida.
* **REVALIDATED:** la risorsa è stata distribuita dalla cache. Il TTL era scaduto, ma una richiesta `If-Modified-Since` all'origine ha indicato che la risorsa non è stata modificata. Pertanto, la versione nella cache viene nuovamente considerata valida.

## Procedura consigliata 2: per il contenuto guidato dagli eventi, utilizza l'API per pulire la tua cache
Ad esempio, ogni volta che viene aggiunto un nuovo post al tuo blog, potresti facilmente pulire la cache di CIS utilizzando un comando API. È comune visualizzare il contenuto guidato dagli eventi e lo rendiamo più semplice per garantire che nessun contenuto obsoleto raggiunga i tuoi utenti. I comandi per pulire la cache immediatamente nella nostra rete globale completa sono elencati qui di seguito. Puoi utilizzare la nostra applicazione di memorizzazione nella cache o l'API.

  * Pulisci la cache utilizzando una tag della cache
  * Pulisci la cache globalmente
  * Pulisci la cache con la regola della pagina
  * Utilizza le funzioni di memorizzazione nella cache avanzate

### Pulisci la cache con una tag della cache 
Le tag della cache ti permettono di definire i bucket del contenuto che desideri eliminare. È un modo eccellente di combinare gli oggetti che vengono comunemente modificati insieme. Quindi un post di blog HTML, ad esempio, e tutto il suo contenuto di immagini potrebbero essere contrassegnati insieme. Anche il contenuto soltanto mobile può essere integrato utilizzando le tag della cache, per cui puoi eliminare tutto quando esegui un nuovo aggiornamento al tuo dominio mobile.

### Pulisci la cache globalmente
Hai anche l'opzione di applicare la riconvalida di tutta la nostra cache. Puoi reimpostare tutti gli oggetti memorizzati nella nostra cache in modo che ogni richiesta sia instradata al server di origine.

### Pulisci la cache con la regola della pagina
Le regole della pagina ti permettono di pulire tutta la cache in base a un'espressione regolare. Puoi utilizzare una regola della pagina predefinita e riconvalidare tutti i riscontri con tale regola della pagina. Puoi creare fino a 50 regole della pagina.

### Utilizza le funzioni di memorizzazione nella cache avanzate

**Bypass Cache on Cookie:** è configurato in una regola della pagina, questa funzione ti permette di presentare un oggetto memorizzato nella cache a meno che non esista un cookie di un nome specifico. Ad esempio, puoi presentare una versione memorizzata nella cache della homepage a meno che trovi un cookie `SessionID` che indica che il cliente è collegato e pertanto gli dovrebbe essere presentato del contenuto personalizzato.
