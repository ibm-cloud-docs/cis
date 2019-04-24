---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Use Page Rules, standard cache levels, Custom Caching Sets

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Utilizza le regole della pagina con la memorizzazione nella cache
{:#use-page-rules-with-caching}

Le regole della pagina ti forniscono la capacità di effettuare molte azioni basate sull'URL della pagina, come la creazione dei reindirizzamenti, l'ottimizzazione del comportamento della memorizzazione nella cache o l'abilitazione e disabilitazione dei servizi.

Una regola della pagina ha effetto sul modello dell'URL fornito che corrisponde al seguente formato:

`<scheme>://<hostname><:port>/<path>`

Ad esempio:

`https://www.example.com:80/image.png`

I componenti `scheme` e `port` sono facoltativi. Se viene omesso il componente `scheme`, il formato accetta i protocolli `http://` e `https://`. Se non viene specificato `port`, la regola corrisponde a tutte le porte. Puoi eseguire le corrispondenze jolly di base utilizzando un simbolo `*` nel tuo modello della regola, consentendo la corrispondenza di una serie di modelli simili.

**Cose importanti da ricordare con le regole della pagina:**

 * Solo una regola della pagina può avere effetto su ogni richiesta selezionata.
 * Le regole della pagina forniscono la priorità dall'alto in basso. Quando un URL corrisponde a una regola, viene applicata solo tale regole; cioè, se una regola della pagina ha già attivato una richiesta, tutte le regole successive che corrispondono al modello dell'URL non avranno effetto. 
 * Come regola generale, ti consigliamo di ordinare le tue regole dalla più specifica alla meno.
 * Le regole della pagina possono essere disabilitate, in tal caso non avranno alcun effetto ma possono ancora essere visualizzate nell'elenco e modificate. Impostando l'interruttore *Enabled* su "Off" si crea una regola della pagina che è inizialmente disabilitata.


## Inoltro (reindirizzamento dell'URL)
{:#forwarding-url-redirection}

Reindirizza un URL a un altro utilizzando un reindirizzamento HTTP 301 o 302. È possibile fare riferimento ai contenuti di tutte le sezioni di un URL che corrispondono a un carattere jolly utilizzando la sintassi `$X`. La `X` indica l'indice nel modello: `$1` viene sostituito con la prima corrispondenza del carattere jolly, `$2` con la seconda e così via.

Ad esempio, supponi di configurare la seguente regola:

![immagine](images/url-redirection-example.png)

Qui, una richiesta a `www.example.com/stuff/things` sarà reindirizzata a `http://example.com/stuff/things`.

Fai attenzione a non creare un reindirizzamento in cui il dominio punta a se stesso come destinazione. Questo errore può causare un errore di reindirizzamento infinito e gli URL colpiti non saranno in grado di risolverlo.
{:note}


## Reindirizzamento a HTTPS
{:#redirecting-to-https}

Se vuoi reindirizzare i tuoi visitatori all'utilizzo di HTTPS, utilizza invece l'impostazione **Always Use HTTPS**:

![immagine2](images/url-matching-patterns.png)


## Memorizzazione nella cache personalizzata
{:#custom-caching}

Imposta il comportamento della memorizzazione nella cache per tutti gli URL che corrispondono al modello della regola della pagina, utilizzando uno qualsiasi dei nostri livelli di cache standard. Impostando **Cache Level** su **Cache Everything** si memorizza nella cache tutto il contenuto, anche se non è uno dei nostri tipi di file statici predefiniti. Impostando **Cache Level** su **Bypass** impedisci la memorizzazione nella cache per tale URL.

Quando specifichi il livello della cache utilizzando le regole della pagina, puoi impostare **Edge Cache TTL**, che controlla per quanto tempo CIS conserverà i file nella nostra cache.

**Browser Cache TTL** controlla per quanto tempo le risorse memorizzate nella cache dai browser client rimangono valide. Se un browser richiede nuovamente una risorsa e il TTL non è scaduto, il browser riceve una risposta `HTTP 304 (Not Modified)`. Puoi impostare i TTL in un intervallo compreso tra 30 minuti e 1 anno.

Non tutti i comportamenti della memorizzazione nella cache predefiniti sono strettamente conformi a RFC. L'impostazione di **Origin Cache Control** significa che le regole della pagina utilizzano una serie più recente di regole di memorizzazione nella cache che cercano di rispettare più strettamente i RFC, principalmente con il rispetto della riconvalida. Ad esempio, il nostro comportamento predefinito con `max-age=0` è di non memorizzare nella cache, al contrario l'impostazione **Origin Cache Control** memorizza ma viene sempre riconvalidata.

Il seguente esempio imposta una regola della pagina per memorizzare nella cache tutto quello che è stato trovato nella cartella `/images`. Le risorse memorizzate nella cache scadono in 30 minuti nel browser dell'utente e dopo un giorno nei data center IBM CIS:

![immagine3](images/url-example.png)

**Serve Stale Content** offre pagine dalla nostra cache, anche quando il server si arresta. I visitatori vedono una versione limitata del nostro sito, con un messaggio indicante che sono nella modalità di esplorazione offline.  

Questa funzione restituisce uno stato HTTP 503. Quando i server sono di nuovo online, CIS porta i visitatori all'esplorazione regolare senza interruzioni. 

Se la pagina richiesta non si trova nella cache, il tuo visitatore visualizza una pagina di errore che lo informa che la pagina che sta richiedendo è offline.
Se una regola della pagina **Cache Everything** è abilitata con tempi di scadenza più bassi della frequenza di memorizzazione nella cache, **Serve Stale Content** viene ripulito nell'intervallo corrispondente.
{:note}
