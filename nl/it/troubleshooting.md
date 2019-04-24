---
copyright:
  years: 2018
lastupdated: "2018-03-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Risoluzione dei problemi della tua connessione di rete CIS

## Come so se i miei dati stanno passando tramite la mia connessione IBM CIS?

IBM Cloud Internet Services (CIS) utilizza le intestazioni HTTP, che può leggere, aggiungere o modificare. L'intestazione ci permette di tracciare una richiesta che è stata instradata, utilizzando un numero CF-Ray. Il numero CF-Ray può essere trovato da un comando `curl` o con un plugin di Google Chrome denominato "Claire".

Per sapere se i dati sono stati trasmessi tramite IBM CIS, individua il `Ray ID` che sarà presentato per ogni pacchetto.

**Strumenti della riga di comando Unix:**

 * curl for HTTP:
`$ curl -vso /dev/null http://example.com`

 * dig for DNS:
`$ dig www.example.com`

 * traceroute for network:
`$ traceroute example.com`

**Ad esempio:**

Comando di terminale: `curl -svo /dev/null YOUR_URL_HERE. -L`

Da come risultato: `CF-RAY: 1ca349b6c1300da3-SJC`

## Come traccio una rotta?

Per vedere se una rotta passa tramite il tuo percorso di comunicazione IBM CIS, puoi eseguire ‘dig’ in una finestra del terminale per Mac o Linux
o utilizzare `nslookup` nel prompt dei comandi Windows per Windows.

Se il pacchetto a un valore CF-Ray, è stato trasmesso tramite CIS.

Il comando `traceroute` mostra il percorso completo seguito da una richiesta IP.

Il team di supporto fa uso di questi comandi per aiutarti.

## Se visualizzi un'avvertenza sulla privacy:

I certificati emessi da IBM CIS coprono il dominio root (`example.com`) e un livello del dominio secondario (`*.example.com`). Se stai tentando di raggiungere un dominio secondario di secondo livello (`*.*.example.com`) visualizzerai un'avvertenza sulla privacy nel tuo browser, perché questi nomi host non sono aggiunti nella SAN.

Inoltre, concedi almeno 15 minuti a una delle nostre autorità di certificazione (CA) partner per emettere un nuovo certificato. Visualizzerai un'avvertenza sulla privacy nel tuo browser se il tuo nuovo certificato non è ancora stato emesso.

## Cosa posso fare se sono sotto un attacco DDoS?

 * **Passo 1:** attiva "Defense Mode" dal tuo dashboard
 * **Passo 2:** imposta i tuoi record DNS sulla sicurezza massima 
 * **Passo 3:** non limitare la frequenza o le richieste da IBM CIS 
 
Durante "Defense Mode", a ogni nuovo visitatore viene proposto una richiesta di sicurezza "Captcha", che devono passare prima che gli venga fornito un cookie per l'accesso senza richiesta. In questo modo, il traffico botnet viene bloccato finché "Defense Mode" è abilitato. I visitatori che non superano la richiesta di sicurezza vengono aggiunti al database della reputazione dell'IP (negativo).

## Altri problemi che potresti riscontrare:

Questi sono alcuni dei messaggi di errore comuni che tu o il tuo team di supporto potreste visualizzare:

| Codice di errore | Motivo |
| ------------- | ------------- |
| 1001  | Errore risoluzione DNS. Il cliente appena registrato o le sue informazioni DNS non sono ancora state trasmesse o chiunque stia gestendo il DNS ha un problema. |
| 521  | Il server web di origine ha rifiutato la connessione da CIS. Il server web di origine non è in esecuzione o qualcuno sta bloccando gli indirizzi IP IBM CIS. |
| 522  | Timeout di connessione al server di origine (valore predefinito di 30 secondi). CIS potrebbe essere a frequenza limitata, il server web potrebbe stare utilizzando tutte le risorse (server condiviso) o è stato riscontrato qualche problema di connettività di rete tra il server web e IBM CIS. |
| 523  | Il server di origine non è raggiungibile. Assicurati che l'indirizzo IP di origine del record DNS sia lo stesso di quello visualizzato nella pagina delle impostazioni DNS di CIS. |
| 524  | IBM CIS potrebbe effettuare una connessione TCP ma non ha ricevuto una risposta dal server web. Un'applicazione a esecuzione prolungata o una query del database sta interferendo. |

### Non vedo alcun traffico di rete

Se non stai vedendo il traffico e stai utilizzando un CNAME, assicurati che sia in atto un reindirizzamento, così il traffico non viene reinstradato al dominio root. Ricorda che alcune propagazioni DNS possono richiedere fino a 48 ore per il completamento.

### Sito web offline

Questo è quello che potresti visualizzare:

`IBM CIS non può collegarsi al server di origine (errore 521, 522, 523)`.

**Sito web offline - nessuna versione memorizzata nella cache**

1. Il server è online, ma sta bloccando la richiesta IBM CIS.
2. Il server di origine è offline e IBM CIS non ha un'immagine del sito web di backup 

Azioni possibili:

* Verifica che gli indirizzi IP di IBM CIS siano consentiti.
* Assicurati che gli IP di IBM CIS non siano a frequenza limitata.
* Questo è l'elenco di [IP da consentire](whitelisted-ips.html)

### Errore 502 “The dreaded 502”

Questo errore è uno dei più comuni che puoi visualizzare. Normalmente si verifica quando una parte di una rete non è disponibile, ad esempio, all'inizio di un attacco DDoS. Un data center particolare può non essere disponibile per un po'. Il traffico sarà reinstradato. Esegui una rotta di tracciamento. 

Questo è quello che potresti visualizzare: `Error 502 - bad gateway error`

Cosa è successo: 

* Una parte di una rete IBM CIS sta riscontrando un problema.
* Normalmente il problema è limitato a un server in un data center.
* Influisce solo su una parte dei visitatori del sito.
* Il team delle operazioni tecniche di IBM CIS si occupa di questo.

Azioni possibili:

* Invia i risultati da `www.YOUR_DOMAIN.com/cdn-cgi/trace` in un ticket al [Supporto](https://console.bluemix.net/docs/support/index.html#contacting-support).
* Disattiva temporaneamente i tuoi record DNS (nessun proxy).

