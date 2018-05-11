---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Utilizza le regole della pagina 

Una regola della pagina specifica le impostazioni e i valori che puoi applicare a un modello URL specifico che fa riferimento al tuo dominio. Le regole della pagina ti aiutano a gestire la sicurezza, le prestazioni e l'affidabilità basate su ogni URL individuale nel tuo sito. La seguente tabella illustra le regole della pagina disponibili a tutti i clienti, i loro funzionamenti e tutte le considerazioni speciali che devi tenere a mente prima di utilizzarle.

## Sicurezza

| **Impostazione** | **Funzionamento** | **Considerazioni** |
|-----------|----------|----------------|
|**Browser Integrity Check**|Ricerca le intestazioni HTTP comuni sfruttate dagli spammer e nega l'accesso alla tua pagina. Blocca inoltre i visitatori che non dispongono di un agent utente o aggiunge un agent utente non standard (è anche comunemente utilizzata dallo sfruttamento di bot, crawler e API). | |
|**Disable Security**|Disabilita le seguenti funzioni: <ul><li>Email Obfuscation</li> <li>Server Side Excludes</li> <li>WAF</li></ul>|Se una regola è impostata per disabilitare la sicurezza e un'altra per abilitare WAF, la regola WAF ha la precedenza, indipendentemente dall'ordine in cui sono visualizzate.|
|**Email Obfuscation**|Attiva/disattiva l'offuscamento dell'email. | |
|**IP Geolocation Header**|Include il codice paese dell'ubicazione del visitatore a tutte le richieste al tuo sito web. Le informazioni possono essere trovate nell'intestazione HTTP `CF-IPCountry`. | |  
|**Security Level**|Controlla quanto deve essere alto il punteggio della minaccia in modo che a un client sia visualizzata una pagina di richiesta di sicurezza. Questa impostazione può essere utilizzata in modo che il tuo sito presenti sempre ai visitatori la richiesta di sicurezza **Defense Mode** quando visitano il tuo sito. | |
|**Server Side Excludes**|Attiva/disattiva l'esclusione lato server.  | |
|**TLS**|Controlla quali modalità TLS vengono utilizzate. | |
|**WAF**|Attiva/disattiva WAF. | |  
|**Automatic HTTPS Rewrites**|Attiva/disattiva automaticamente le riscritture HTTPS.  | |
|**Opportunistic Encryption**|Attiva/disattiva la codifica opportunistica. | |
|**Cache Deception Armor**|Attiva/disattiva la protezione dall'inganno della cache.  | |
|**Always Use HTTPS**|Converte tutti gli URL `http://` in `https://` creando un reindirizzamento `301`.|L'utilizzo di questa impostazione disabilita la configurazione di tutte le altre impostazioni della regola, perché IBM CIS applica un reindirizzamento a `HTTPS` per la richiesta, che diventa una nuova richiesta che viene quindi valutata con le regole della pagina. |

## Prestazioni
| **Impostazione** | **Funzionamento** | **Considerazioni** |
|-----------|----------|----------------|
|**Browser Cache TTL**|Controlla per quanto tempo le risorse memorizzate nella cache dai browser client rimangono valide. | |
|**Bypass Cache on Cookie**|Presenta un oggetto memorizzato nella cache a meno che vediamo un cookie di un nome specifico, ad esempio, presenta una versione memorizzata nella cache della homepage a meno non vediamo un cookie `SessionID` che indica che il cliente ha eseguito l'accesso e pertanto gli dovrebbe essere presentato del contenuto personalizzato. | |
|**Cache Level**|**Bypass** - Le risorse che corrispondono a tale regola della pagina non vengono memorizzate nella cache.<br>**No query string** - Fornisce le risorse dalla cache solo quando non è presente alcuna stringa di query.<br>**Ignore query string** - Fornisce la stessa risorsa a chiunque indipendentemente dalla stringa di query.<br>**Standard** - Fornisce una risorsa differente ogni volta che viene modificata la stringa di query.<br> **Cache everything** - Le risorse che corrispondono a tale regola della pagina vengono memorizzate nella cache.|Per impostazione predefinita, il contenuto HTML non viene memorizzato nella cache. Deve essere scritta una regola della pagina per memorizzare nella cache il contenuto HTML statico. |
|**Edge Cache TTL**|Controlla per quanto tempo IBM CIS conserverà i file nella nostra cache. |Questa impostazione è facoltativa quando specifichi il livello della cache. |

## Affidabilità
| **Impostazione** | **Funzionamento** | **Considerazioni** |
|-----------|----------|----------------|
|**Always Online**|Mantiene una versione limitata del sito online se il server si arresta. |Per ulteriori informazioni vedi [Gestione della tua distribuzione CIS per l'affidabilità ottimale](managing-for-reliability.html) |
|**Origin Cache Control**|Determina quale contenuto viene memorizzato nella cache dall'origine e quanto spesso viene aggiornato. |Per ulteriori informazioni vedi [Gestione della tua distribuzione CIS per l'affidabilità ottimale](managing-for-reliability.html) |
|**Forwarding URL** |L'URL che deve essere utilizzato nel caso il sito non sia disponibile. | L'utilizzo di questa funzionalità disabilita la configurazione di tutte le altre impostazioni perché stai inoltrando la richiesta da qualche altra parte. Per ulteriori informazioni vedi [Gestione della tua distribuzione CIS per l'affidabilità ottimale](managing-for-reliability.html)|

## Modelli URL della regola della pagina

Una regola della pagina ha effetto su un modello dell'URL fornito, che corrisponde al seguente formato: 

`<scheme>://<hostname><:port>/<path>`

Un esempio di utilizzo di tutti i componenti sarà:

`https://www.example.com:80/image.png`

I componenti *scheme* e *port* sono facoltativi. Se viene omesso scheme, coprirà entrambi i protocolli `http://` e `https://`. Se non viene specificato port, la regola corrisponderà a tutte le porte. Puoi eseguire le corrispondenze jolly di base utilizzando un simbolo ‘*’ nel tuo modello della regola, consentendo la corrispondenza di una serie di modelli simili invece di uno soltanto.

Queste sono tre cose importanti da ricordare con le regole della pagina:

 * Solo una regola della pagina avrà effetto su ogni richiesta selezionata. 
 * Le regole della pagina forniscono la priorità dall'alto in basso. 
 * Quando un URL corrisponde a una regola, sarà applicata solo tale regole; cioè, se una regola della pagina ha già attivato una richiesta, tutte le regole successive che corrispondono al modello dell'URL non hanno effetto. Come regola generale, ti consigliamo di ordinare le tue regole dalla _più specifica_ alla _meno specifica_.

Le regole della pagina possono essere disabilitate, in tal caso non avranno alcun effetto. Ma possono ancora essere visualizzate e modificate nell'elenco. Impostando l'interruttore **Enabled** su **Off** creerai una regola della pagina che  è inizialmente disabilitata.

Per ulteriori informazioni, fai riferimento al [documento Memorizzazione nella cache e regole della pagina](caching-with-page-rules.html).
