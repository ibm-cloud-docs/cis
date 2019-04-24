---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Best practices, CIS setup

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Procedure consigliate per la configurazione CIS
{:#best-practices-for-cis-setup}

Poiché IBM CIS è posizionato ai margini della tua rete, dovrai effettuare alcuni passi per garantire una buona integrazione con i tuoi servizi CIS. Queste sono le procedure consigliate per l'integrazione di CIS con i tuoi server di origine. 

Puoi seguire questi passi sia prima che dopo aver modificato il tuo DNS e attivato il nostro servizio proxy. Questi consigli permettono a IBM CIS di collegarsi ai tuoi server di origine correttamente. Ti aiuteranno a prevenire i problemi con il traffico HTTPS o API e consentiranno ai tuoi log di acquisire gli indirizzi IP corretti dei tuoi clienti invece degli indirizzi IP CIS di protezione.

Questo è quello che dovrai configurare:

 * Procedura consigliata 1: ripristina gli IP originati dai tuoi clienti
 * Procedura consigliata 2: incorpora gli indirizzi IP CIS
 * Procedura consigliata 3: assicurati che le tue impostazioni di sicurezza non interferiscano con il traffico API
 * Procedura consigliata 4: configura le tue impostazioni di sicurezza il più strettamente possibile
 
## Procedura consigliata 1: impara come ripristinare gli IP originati dai tuoi clienti
{:#best-practice-know-how-to-restore-origininating-ip}

Come un proxy inverso, forniamo l'IP di origine in queste intestazioni:

  * `CF-Connecting-IP`
  * `X-Forwarded-For`
  * `True-Client-IP` (facoltativo)

Puoi ripristinare gli indirizzi IP dell'utente utilizzando una varietà di strumenti, per infrastrutture come Apache, Windows IIS e NGINX.

## Procedura consigliata 2: incorpora gli indirizzi IP CIS per rendere fluida l'integrazione
{:#best-practice-incorporate-cis-ip-addresses}

Questi sono i due passi da effettuare:

  * Rimuovi qualsiasi limite alla frequenza di indirizzi IP CIS
  * Configura i tuoi ACL per consentire solo gli indirizzi IP CIS e altre parti attendibili.

Puoi trovare l'elenco aggiornato degli intervalli di IP per IBM CIS [in questa ubicazione](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses).

## Procedura consigliata 3: controlla le tue impostazioni di sicurezza per assicurarti che non interferiscano con il traffico API
{:#best-practice-review-security-settings-interference}

IBM CIS normalmente accelera il traffico API rimuovendo il sovraccarico della connessione. Tuttavia, la posizione di sicurezza predefinita può interferire con molte chiamate API. Ti consigliamo di effettuare alcune azioni per prevenire l'interferenza con il tuo traffico API quando la trasmissione tramite proxy è attiva.

 * Disattiva le funzioni di sicurezza in modo selettivo, utilizzando le funzioni **Page Rules**.
   * Crea una regola della pagina con il modello dell'URL della tua API, come `api.example.com`
   * Aggiungi i seguenti comportamenti della regola:
     * Seleziona **Security Level** su **Essentially off**
     * Seleziona **TLS** su **Off**
     * Seleziona **Browser Integrity Check** su **Off**
   * Seleziona **Provision Resource**

 * In alternativa, puoi disattivare **Web Application Firewall** globalmente dalla pagina Security.

| *Cosa fa il controllo di integrità del browser?* | 
|------------------------------------------------|
| *Il controllo di integrità del browser ricerca le intestazioni HTTP che vengono comunemente sfruttate dagli spammer. Nega al traffico con queste intestazioni di accedere alla tua pagina. Blocca inoltre i visitatori che non dispongono di un agent utente o chi aggiunge un agent utente non standard (questa tattica è comunemente utilizzata dallo sfruttamento di bot, crawler e API).* |

## Procedura consigliata 4: configura le tue impostazioni di sicurezza il più strettamente possibile
{:#best-practice-configure-stict-security-settings}

CIS fornisce alcune opzioni per la codifica del tuo traffico. Come un proxy inverso, chiudiamo le connessioni TLS ai nostri data center e apriamo una nuova connessione TLS ai tuoi server di origine. Per la tua fine con CIS, puoi caricare un certificato personalizzato dal tuo account, puoi utilizzare un certificato con carattere jolly che ti ha fornito CIS o entrambi.

### Carica un certificato personalizzato
{:#strict-upload-custom-cert}
 
Puoi caricare le tue chiavi pubblica e privata quando crei un dominio aziendale. Se carichi il tuo certificato, ottieni la compatibilità immediata e mantieni il controllo sul tuo certificato (ad esempio, un certificato di convalida estesa (EV)). Ricorda che sarai responsabile della gestione del tuo certificato se carichi un certificato personalizzato. Ad esempio, IBM CIS non traccia le date di scadenza del certificato. 
 
### In alternativa, utilizza un certificato fornito da CIS
{:#strict-utilize-cert-cis-provisioned}
 
IBM CIS ha collaborato con molte autorità di certificazione (CA) per fornire i certificati con carattere jolly del dominio ai nostri clienti, per impostazione predefinita. Potrebbe essere richiesta la verifica manuale per la configurazione di questi certificati e il tuo team di supporto può aiutarti ad eseguire questi ulteriori passi.
 
### Modifica le tue impostazioni TLS con **End-to-End CA Signed**
{:#strict-change-tls-setting}
 
La maggior parte dei nostri clienti aziendali utilizza la configurazione di sicurezza End-to-End CA Signed. Una configurazione **End-to-End CA Signed** richiede un certificato firmato CA valido installato nel tuo server web. La data di scadenza del certificato deve essere nel futuro e deve avere un *nome host* o *nome alternativo di soggetto (SAN)* corrispondente.

