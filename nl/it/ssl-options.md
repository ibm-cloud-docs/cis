---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: TLS Options, secure connection, Automatic HTTPS

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Opzioni TLS
{:#cis-tls-options}

Le opzioni TLS ti consentono di controllare se i visitatori possono sfogliare il tuo sito web su una connessione sicura e quando lo fanno, come CIS si collegherà al tuo server di origine.

## Automatic HTTPS rewrite
{:#automatic-https-rewrite}

Le riscritture HTTPS automatiche (Automatic HTTPS rewrite) consentono di correggere contenuto misto modificando “http” in “https” per tutte le risorse o tutti i link sul tuo sito web che possono essere gestiti con HTTPS. Questa impostazione si trova nella pagina di configurazione della sicurezza **Advanced**.

## Modalità di codifica TLS
{:#tls-encryption-modes}

Queste opzioni sono elencate nell'ordine dalla meno sicura (Off) alla più sicura (End-to-End CA signed). 
 * Off (non consigliata)
 * Client-to-Edge (i certificati edge to origin non sono codificati, i certificati autofirmati non sono supportati) 
 * End-to-End flexible (i certificati edge to origin possono essere autofirmati)  
 * End-to-End CA signed (predefinita e consigliata)
 * HTTPS only origin pull (solo Enterprise)

### Off 
{:#tls-encryption-modes-off}
Nessuna connessione protetta tra il tuo visitatore e CIS e tra CIS e il tuo server web. I visitatori possono solo visualizzare il tuo sito web su HTTP e chi tenta di collegarsi utilizzando HTTPS riceverà `HTTP 301 Redirect` che reindirizza alla versione HTTP semplice del tuo sito web.

### Client-to-Edge
{:#tls-encryption-modes-client-to-edge}

Una connessione sicura tra il tuo visitatore e CIS ma non tra CIS e il tuo server web. Non devi disporre di un certificato TLS sul tuo server web, ma i tuoi visitatori vedono ancora il tuo sito come abilitato HTTPS. Questa opzione non è consigliata se hai informazioni sensibili sul tuo sito web. Questa impostazione funzionerà solo per la porta 443->80. Dovrebbe essere utilizzata solo come ultima risorsa se non sei in grado di configurare TLS sul tuo server web. È _meno sicura_ di tutte le altre opzioni (anche di “Off”) e potrebbe causare problemi quando decidi di passare a un'altra opzione.

### End-to-End Flexible
{:#tls-encryption-modes-end-to-end-flexible}

Una connessione sicura tra il tuo visitatore e CIS e (ma non autenticata) tra CIS e il tuo server web. Il tuo server deve essere configurato per rispondere alle connessioni HTTPS, con almeno un certificato autofirmato. L'autenticità del certificato non viene verificata: dal punto di vista di CIS (quando ci colleghiamo al tuo server web di origine), è equivalente a ignorare questo messaggio di errore. Finché l'indirizzo del tuo server web di origine è corretto nelle tue impostazioni DNS, sai che ci stiamo collegando noi al tuo server web e non qualcun altro.

### End-to-End CA Signed
{:#tls-encryption-modes-end-to-end-ca-signed}

Predefinita e consigliata. Una connessione sicura tra il visitatore e CIS e sicura e autenticata tra CIS e il tuo server web. Il tuo server deve essere configurato per rispondere alle connessioni HTTPS, con un certificato TLS valido. Questo certificato deve essere firmato da un'autorità di certificazione, avere una data di scadenza nel futuro e rispondere al nome del dominio della richiesta (nome host). Ti consigliamo di continuare a utilizzare questa modalità TLS per procedure di sicurezza migliori, a meno che tu non comprenda le potenziali minacce alla sicurezza derivanti dal passare a una delle modalità meno rigide. 

### HTTPS Only Origin Pull
{:#tls-encryption-modes-origin-only-pull}

*Solo Enterprise.* Questa modalità ha gli stessi requisiti di certificato di End-to-End CA Signed ed esegue anche l'upgrade di tutte le connessioni tra CIS e il tuo server web di origine da HTTP a HTTPS, anche se il contenuto originale richiesto è su HTTP.

## Versione TLS minima
{:#minimum-tls-version}

Imposta la versione minima TLS per il traffico che tenta di collegarsi al tuo sito. Per impostazione predefinita, viene impostata su 1.0. Le versioni TLS successive a questa offrono sicurezza aggiuntiva, ma potrebbero non essere supportate da tutti i browser. Ciò potrebbe impedire ad alcuni clienti di collegarsi al tuo sito. 
