---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: edge functions beta, edge functions

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Funzioni Edge (Beta)
{: #edge-functions}

Le funzioni edge di CIS ti consentono di creare nuove applicazioni o di modificarne di esistenti, senza dover configurare o mantenere l'infrastruttura, utilizzando un ambiente di esecuzione senza server. Le funzioni edge possono essere definite e caricate nell'edge Cloud per elaborare le richieste prima che raggiungano l'origine. Le funzioni edge CIS possono essere utilizzate per modificare le richieste e le risposte HTTP, per effettuare richieste in parallelo o per generare risposte dall'edge Cloud. 

## Come funzionano le funzioni edge
{: #how-edge-functions-work}

Le funzioni edge associano le **azioni** agli URI in base a un dominio definito. Questa associazione viene detta **trigger**. Le richieste in entrata al tuo sito verranno intercettate nell'edge del cloud e messe in corrispondenza con i trigger presenti nel tuo account o dominio. Se l'URL della richiesta corrisponde all'URI del trigger, viene eseguita l'azione associata al trigger. 

Le funzioni edge vengono create usando come modello i [processi di lavoro dei servizi](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) disponibili nei browser web moderni e utilizzano la stessa API quando possibile.

L'API del processo di lavoro dei servizi ti consente di intercettare qualsiasi richiesta effettuata al tuo sito. Una volta che il tuo JavaScript sta gestendo la richiesta, puoi scegliere di effettuare qualsiasi numero di sottorichieste al tuo sito o ad altri siti e restituire, alla fine, la risposta che ti soddisfa al tuo visitatore.

A differenza dei processi di lavoro dei servizi standard, le funzioni edge vengono eseguite sui server edge CIS, non nel browser dell'utente. Ciò significa che puoi essere certo che il tuo codice verrà eseguito in un ambiente attendibile in cui non potrà essere eluso da client dolosi. Significa anche che l'utente non ha bisogno di utilizzare un browser moderno che supporti i processi di lavoro dei servizi – puoi anche intercettare le richieste dai client API che non sono affatto browser. 

Internamente, le funzioni edge utilizzano lo stesso motore JavaScript V8 utilizzato nel browser Google Chrome per eseguire i processi di lavoro nella nostra infrastruttura. V8 compila dinamicamente il tuo codice JavaScript in un codice macchina ultra veloce, rendendolo molto performante. Ciò consente al tuo codice di essere eseguito in microsecondi e per il nostro edge di eseguire molte migliaia di script al secondo.

Mentre le funzioni edge utilizzano V8, non utilizzano Node.js. Le API JavaScript disponibili per te all'interno dei processi di lavoro vengono implementate direttamente da noi. Utilizzare direttamente V8 consente al codice di essere eseguito in modo più efficiente e con i controlli di sicurezza necessari per proteggere i clienti e l'infrastruttura. 


## Azioni
{: #edge-functions-actions}

Le azioni sono scritte in JavaScript e necessitano di un listener di eventi per rispondere a un evento trigger. Le azioni non influiranno sul tuo traffico a meno che non vengano utilizzate da un trigger. 

### Piani aziendali contro piani standard
{: #edge-functions-enterprise-v-standard-plans}

I piani Standard hanno massimo un'azione. All'azione viene assegnato un nome che è uguale a quello del tuo dominio. Puoi sostituire la tua azione caricando un altro file oppure aggiornare la tua azione utilizzando un editor di codice. Il caricamento di un altro file rimuoverà l'azione esistente. 

I piani Enterprise possono caricare un numero illimitato di script. A tali script possono essere assegnati nomi univoci. 

### Azioni di creazione
{: #edge-functions-create-actions}

Seleziona **Create** per aggiungere un'azione utilizzando l'editor di codice. Nei piani Enterprise, immetti un nome per la tua azione. Nei piani Standard, il nome non è modificabile ed è impostato sul nome del tuo dominio. Una volta aggiunto il tuo codice Javascript, seleziona **Save** per creare la tua azione. 

### Azioni di caricamento
{: #edge-functions-upload-actions}

Utilizza il pulsante **Upload** per caricare un file Javascript. Nei piani Enterprise, il nome dell'azione è il nome del file. Nei piani Standard, il nome dell'azione è impostato sul nome del tuo dominio. 

Il caricamento o la creazione di un'azione con lo stesso nome di un'azione esistente causerà la sovrascrittura dell'azione esistente. Ridenomina il file dell'azione prima di caricarlo o immetti un nome univoco nel campo di testo durante la creazione per evitare che si verifichi questa situazione.
{:note}

### Azioni di modifica
{: #edge-functions-edit-actions}

La selezione di un'azione apre tale azione nell'editor per la modifica. Ogni volta che salvi le modifiche, l'azione verrà caricata nell'edge del cloud. Dopo l'aggiornamento, seleziona **Save**. Se l'azione è in uso, le modifiche diventeranno immediatamente effettive.  

### Azioni di eliminazione
{: #edge-functions-delete-actions}

Elimina un'azione facendo clic sull'icona di **eliminazione** nella tabella **Actions**. Un'azione non può essere eliminata mentre è in uso. Per eliminare l'azione, rimuovila innanzitutto dai trigger. La colonna degli **utilizzi** mostra il numero di trigger associati a questa azione. L'eliminazione non può essere annullata. 


### Trigger associati
{: #edge-functions-associated-triggers}

Aggiungi un trigger e associalo a un'azione. 

### Limitazioni note delle funzioni edge
{: #edge-functions-known-limitations}

Il caricamento di un'azione con lo stesso nome di un'azione esistente. L'azione esistente verrà sovrascritta. Ridenomina il file dell'azione prima di caricarlo per evitare questa situazione. 


## Trigger
{: #triggers}

### Informazioni sui trigger
{: #about-triggers}

I trigger (rotte) determinano l'instradamento del traffico del dominio alle azioni. I trigger associano determinati modelli dell'URL, basati su un dominio sull'account, a un'azione predefinita. L'URL deve contenere il dominio, ma può contenere caratteri jolly come un prefisso al dominio o alla fine del percorso. Se su un modello non viene specificato alcun percorso, viene aggiunto implicitamente un carattere `/`. Il modello dell'URL non può contenere caratteri jolly infissi o parametri di query. 

Devi aggiungere un dominio per aggiungere i trigger. Puoi aggiungere i trigger senza avere azioni. 

### Aggiungi i trigger
{: #add-triggers}

Vai alla scheda **Triggers** e fai clic su **Add trigger**. Immetti un modello dell'URL e seleziona un'azione dall'elenco delle azioni esistenti.  

Per un'azione puoi anche selezionare **Avoid Edge Functions**. Ciò consente al percorso del trigger di rimanere attivo ma di evitare di utilizzare le azioni della funzione edge. Ad esempio, è presente un'azione denominata `my-function` e un trigger con il percorso `beta.cistest-load.com/*`. Se il percorso `beta.cistest-load.com/data` non deve utilizzare l'azione `my-function`, crea un altro trigger con il percorso `beta.cistest-load.com/data` e l'opzione **Avoid Edge Functions**. Ciò consente al percorso `beta.cistest-load.com/data` di rimanere attivo senza utilizzare l'azione `my-function`.

### Modifica i trigger
{: #edit-triggers}

Aggiorna un trigger utilizzando l'opzione di menu nella riga della tabella per un trigger selezionato. Dopo l'aggiornamento, seleziona **Save**. 

### Elimina i trigger
{: #delete-triggers}

Elimina un trigger utilizzando l'opzione di menu nella riga della tabella per un trigger selezionato. Questa azione non può essere annullata. 


## Casi di utilizzo
{: #edge-functions-use-cases-examples}

Questi esempi sono solo a scopo dimostrativo e non sono progettati per essere utilizzati nella produzione.
{:important}
* [Test A/B](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#ab-testing)
* [Aggiunta di un'intestazione della risposta](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#add-response-header)
* [Aggregazione di più richieste](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#aggregate-multiple-requests)
* [Instradamento condizionale](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#conditional-routing)
* [Protezione hotlink](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#hot-link-protection)
* [Risposte senza origine](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#originless-responses)
* [Richieste Post](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#post-requests)
* [Impostazione di un cookie](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#setting-cookies)
* [Richieste firmate](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#signed-requests)
* [Risposte di streaming](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#streaming-responses)
