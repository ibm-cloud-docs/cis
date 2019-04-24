---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Overview page, page rules, Service Mode

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Gestisci la tua distribuzione di IBM Cloud Internet Services (CIS)
{:#manage-your-cis-deployment}

Inizierai utilizzando la schermata della panoramica come tua base di lavoro delle operazioni. Mostra tutti i parametri correnti della tua distribuzione.

Una volta che hai configurato il tuo DNS, sei pronto per iniziare!

## Utilizzo della schermata della panoramica
{:#using-the-overview-screen}

Utilizzando la schermata della panoramica, puoi visualizzare lo stato di tutte le tue selezioni. Ciascuna impostazione si collega alla sezione dell'interfaccia utente in cui è configurata l'impostazione. Per modificare qualsiasi selezione, puoi spostarti facendo clic sul link relativo all'impostazione. Ad esempio, per modificare la configurazione del programma di bilanciamento del carico o per aggiungere un nuovo programma di bilanciamento del carico, fai clic sul campo `Load Balancer`.

Nella schermata della panoramica, puoi visualizzare che la tua configurazione del nome del dominio è nello stato **Pending** o **Active** come illustrato nella seguente figura.


![immagine schermata panoramica](images/overview-screen-configuration-summary.jpg)

Lo stato **Pending** indica che il dominio non è ancora completamente configurato. Devi aggiornare il tuo provider DNS o la tua funzione di registrazione con i server dei nomi forniti come parte del processo di configurazione. 

**Solo Enterprise**: la sezione **Service Details** della panoramica ti consente anche di aggiungere altri domini alla tua istanza di CIS e di passare da un dominio all'altro. 

## Modifica della modalità di servizio (Service Mode)
{#changing-the-service-mode}

Nella pagina della panoramica, nella sezione Service Mode, è presente un elenco a discesa per selezionare una delle due modalità: 

* **Defense Mode** aiuta a proteggere da attacchi DNS prevedibili o esistenti. Questa modalità impedisce a tutto il traffico di raggiungere i tuoi server di origine tramite il tuo dominio. 
* **Pause Service** disabilita tutti i vantaggi di sicurezza e delle prestazioni nel tuo dominio. Le funzioni DNS risolvono ancora per il tuo sito web, ma il traffico viene inviato direttamente alle origini configurate.  

### Passi per configurare la modalità di servizio (Service Mode)
{:#steps-to-set-service-mode}

1. Seleziona la modalità desiderata dal menu a discesa. 
1. Fai clic sul pulsante `Activate`.
1. Conferma o annulla la selezione nel messaggio a comparsa di conferma. 

Viene visualizzata una notifica su tutte le pagine per mostrare che Pause Service o Defense Mode è attivo.
Per ritornare alla modalità operativa normale, fai clic su `Deactivate mode` nel banner di notifica.
![immagine pulsante deactivate mode](images/deactivate-mode.png)


## Configurazione e gestione del DNS
{:#configure-and-manage-your-dns}

Vai alla pagina DNS per aggiungere un record (molto probabilmente un record A). Immetti le informazioni sul tuo record DNS e poi fai clic su `Add record` per implementare le tue modifiche.

![aggiungi-DNS](images/dns/create-a-type-record.png)

Dopo aver creato i tuoi record, considera di attivare l'impostazione `Proxy`. La maggior parte delle funzioni di CIS richiede che il traffico internet al tuo sito fluisca tramite l'infrastruttura CIS. In altre parole, si applica solo ai programmi di bilanciamento del carico e ai record con proxy. Per beneficiare davvero di CIS, assicurati che i tuoi record DNS e i tuoi programmi di bilanciamento del carico abbiano l'impostazione proxy abilitata. 

## Configura e gestisci la tua memorizzazione nella cache
{:#set-up-and-manage-your-caching}

Successivamente, puoi configurare la memorizzazione nella cache. 

![IMMAGINE](images/caching-screen.png)

Hai l'opzione di 3 tipi di memorizzazione nella cache, disponibili dal menu a discesa della schermata della memorizzazione nella cache: 

 * Nessuna stringa di query :  fornisce le risorse dalla cache solo quando non è presente alcuna stringa di query.
 * Indipendente dalla stringa di query : fornisce la stessa risorsa a chiunque indipendentemente dalla stringa di query. (Nota: l'impostazione **Ignore Query String** si applica solo alle estensioni dei file statici. Questa impostazione rimuove la stringa di query durante la generazione della chiave della cache, per cui una richiesta di `style.css?something` viene normalizzata con `style.css` quando utilizzata dalla cache.)
 * Dipendente dalla stringa di query : fornisce una risorsa differente ogni volta che viene modificata la stringa di query.
  
## Pulisci la cache
{:#purge-cache-overview}
 
Puoi pulire la tua cache per preparare gli aggiornamenti in qualsiasi momento, immetti soltanto l'URL nel campo di pulizia della cache. Puoi pulire uno o più file (fino a 30 alla volta).
 
 ## Scadenza del browser
 {:#browser-expiration}
 
Puoi utilizzare il menu a discesa per selezionare l'ora di scadenza del browser di cui hai bisogno, ad esempio 98 ore o 1 giorno.

Solo Enterprise: puoi anche indicare a CIS di non sovrascrivere il controllo della cache del browser impostando questo valore su **Respect Existing Headers**.
 
 ## Utilizzo della modalità di sviluppo
 {:#using-development-mode}
 
La **modalità di sviluppo** è pensata per l'utilizzo quando sono richiesti aggiornamenti principali o nuovi caricamenti di file o ogni volta che non vuoi che gli utenti finali utilizzino la cache, ma per richiamare i file direttamente dai server di origine. Per iniziare ad utilizzare la **modalità di sviluppo**, sposta lo switch sulla posizione `Enabled`. Per interrompere l'utilizzo della **modalità di sviluppo**, sposta lo switch sulla posizione `Disabled`. La **modalità di sviluppo** scade automaticamente dopo 3 ore. 

## Gestione delle tue regole della pagina
{:#managing-your-page-rules}
 
Puoi utilizzare le regole della pagina per specificare impostazioni particolari che si applicano solo a determinati URL, ad esempio, per avere impostazioni diverse del controllo della cache per determinati percorsi URL. Utilizza i menu a discesa per configurare la regola della pagina. Le impostazioni della regola sono divise in tre categorie: **Security**, **Performance** e **Reliability**.

Tieni presente che quando vengono abilitate alcune regole, altre opzioni vengono disabilitate, se sono in conflitto con le altre regole che hai appena selezionato. Dopo aver selezionato le regole della pagina che desideri, fai clic su **Provision** per abilitarle. Le nuove regole hanno immediatamente effetto e possono essere subito visualizzate nella schermata delle regole della pagina.
 
 ![MENU REGOLE PAGINA](images/page-rule-dropdown-settings.png)
 
Puoi anche abilitare o disabilitare le tue regole della pagina dalla tabella visualizzata nella schermata Page Rules. Per ulteriori informazioni, consulta [Utilizzo delle regole della pagina](/docs/infrastructure/cis?topic=cis-use-page-rules).
 
 ## Impostazioni di sicurezza
 {:#security-settings-overview}
 
Per impostazione predefinita, la protezione DDoS è abilitata per tutti i record DNS o i programmi di bilanciamento del carico con il proxy attivo.
Le impostazioni di sicurezza sono: 

* Attiva WAF utilizzando l'interruttore sulla pagina **Web Application Firewall**. Quando attivi/disattivi le regole, le modifiche vengono applicate immediatamente.

* **Solo Enterprise**: la pagina **Rate limiting** ti consente di configurare le regole che limitano la frequenza per evitare un problema di elementi di disturbo e per respingere DDoS.

* Nella pagina **IP Firewall** puoi configurare le regole di accesso in base a IP, codice paese o ASN. Puoi anche configurare le regole per bloccare gli agent utente. La sezione di blocco del dominio di questa pagina ti consente di limitare l'accesso al tuo dominio a determinati indirizzi IP. 

* Puoi esaminare gli eventi correlati al firewall nella pagina **Events**.

## Certificati
{:#certificates-overview}

Quando configuri un dominio, IBM CIS distribuisce automaticamente un certificato universale per tale dominio. Pertanto, non hai bisogno di fare nulla per avere la protezione basata sul certificato in tale dominio. Se lo desideri, puoi caricare il tuo certificato. Avrai bisogno di un certificato diverso per ogni dominio e visualizzerai un messaggio di errore se il certificato che stai caricando non corrisponde al tuo dominio. Puoi anche ordinare certificati personalizzati su questa pagina.  

![IMMAGINE](images/certificates-table.png)
 
 
