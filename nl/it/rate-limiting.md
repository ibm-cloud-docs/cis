---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Bypass, header responses, brute-force login attempts

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Limitazione frequenza
{:#cis-rate-limiting}

La limitazione frequenza (solo piano Enterprise) protegge da attacchi DoS (denial-of-service), tentativi di accesso di forza bruta e altri tipi di comportamenti abusivi diretti a livello dell'applicazione. 

Seleziona il tipo di regola che limita la frequenza, **Custom rule** o **Protect login**

## Crea una regola personalizzata che limita la frequenza
{:#create-a-custom-rate-limiting-rule}

Immetti un nome regola che ti consenta di ricordare la funzione svolta dalla regola. Questo è un campo facoltativo. 

**Traffic matching criteria** utilizza l'operazione AND. Immetti un URL di cui stai limitando la frequenza e poi quando le richieste provenienti dallo **stesso IP superano** il numero che hai specificato per le **richieste al secondo**, la regola viene attivata. 

L'opzione **Advanced Criteria** ti consente di specificare i metodi HTTP, le risposte di intestazione e i codici di risposta origine per limitare ulteriormente i criteri corrispondenti.  

Seleziona un valore dall'elenco a discesa **Method** (ANY è il valore predefinito).  

Aggiorna l'**intestazione della risposta HTTP**.  Puoi anche **aggiungere l'intestazione della risposta** per includere le intestazioni restituite dal tuo server web di origine.  

Se hai più di un'intestazione nell'**intestazione della risposta HTTP**, viene applicata una logica booleana _AND_. Per escludere un'intestazione dalla corrispondenza, utilizza l'opzione _Not Equal_. Inoltre, ciascuna intestazione deve essere una corrispondenza esatta. Tuttavia, la sensibilità al minuscolo/maiuscolo non si applica.
{:note}

In **Origin response code**, immetti il valore numerico valido di ogni codice di risposta HTTP da mettere in corrispondenza. Per includere due o più codici di risposta, separa ciascun valore con una virgola. Ad esempio, puoi immettere `401, 403` se desideri che vengano conteggiati solo tali codici di errore.  

### Configura la risposta
{:#rate-limiting-configure-response}

Seleziona dalle azioni elencate e specifica il periodo di timeout. In questo caso, il timeout fa riferimento al periodo di divieto in cui si verifica l'azione. Un timeout di 60 secondi significa che l'applicazione viene applicata per 60 secondi. 

|Azione| Descrizione|
|------|------------|
|Block | Emette un errore 429 quando viene superata la soglia|
|Challenge | L'utente deve superare una verifica Google reCaptcha prima di procedere. Se l'esito è positivo, accettiamo la richiesta. In caso contrario, la richiesta viene bloccata. | 	
|JS Challenge |	L'utente deve superare una verifica Javascript prima di procedere. Se l'esito è positivo, accettiamo la richiesta. In caso contrario, la richiesta viene bloccata.
|Simulate| Puoi utilizzare questa opzione per verificare la tua regola prima di applicare una qualsiasi delle altre opzioni nel tuo ambiente reale. 

**Risposta avanzata**

Specifica il tipo di risposta quando viene superata la soglia di una regola.  

### Bypass
{:#rate-limiting-bypass}

Bypass ti consente di creare l'equivalente di una whitelist o di un'eccezione per una serie di URL.  Non vengono attivate azioni per tali URL, anche se la regola che limita la frequenza viene soddisfatta. 

## Protect login
{:#rate-limiting-protect-login}

Protect login crea una regola standard che protegge le pagine di accesso da attacchi di forza bruta. I client che tentano l'accesso per più di 5 volte in 5 minuti verranno bloccati per 15 minuti.  

Immetti un nome per la regola e l'URL di accesso.
