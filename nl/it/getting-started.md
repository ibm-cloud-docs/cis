---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-29"

keywords: IBM Cloud Internet Services, IBM CIS application, Authoritative DNS servers

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Introduzione a IBM Cloud Internet Services (CIS)
{:#getting-started}

IBM Cloud Internet Services (CIS), con tecnologia Cloudflare, offre tre funzionalità principali per migliorare il tuo flusso di lavoro: [sicurezza](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-for-optimal-security), [affidabilità](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability) e [prestazioni](/docs/infrastructure/cis?topic=cis-manage-your-cis-deployment-for-best-performance). Ogni area della funzionalità viene rappresentata nella barra di navigazione di sinistra della tua schermata, dopo che hai aperto l'applicazione IBM CIS.

Per ogni funzionalità, IBM CIS ti aiuta a ottimizzare le sue funzioni per soddisfare i tuoi bisogni specifici, tra cui:

 * Server DNS autorevoli
 * Bilanciamento del carico locale e globale
 * WAF (Web Application Firewall)
 * Protezione DDoS
 * Memorizzazione nella cache e regole della pagina


## Prima di iniziare
{:#before-you-begin}

Prima di iniziare ad utilizzare IBM CIS, avrai prima bisogno di un [ID IBM](https://www.ibm.com/account/reg/us-en/signup?formid=urx-19776). Dopodiché puoi ordinare i tuoi servizi tramite l'account IBM Cloud o il nuovo [Portale IBM Cloud Internet Services](https://{DomainName}/catalog/services/internet-services), a seconda della tua preferenza.

Se hai bisogno di assistenza per ottenere un account per utilizzare IBM Cloud Internet Services, [contatta il tuo rappresentante delle vendite IBM](https://{DomainName}/cloud/support) per ulteriori informazioni introduttive.

Se hai un account Softlayer esistente, puoi [collegare il tuo account](https://{DomainName}/docs/account?topic=account-unifyingaccounts) al tuo ID IBM. 

## Panoramica del processo
{:#process-overview}

Puoi iniziare ad utilizzare IBM CIS per il tuo traffico Internet con pochi passi. 

 * Apri l'applicazione IBM CIS dal tuo dashboard IBM Cloud.
 * Aggiungi il dominio che vuoi gestire.
 * Configura le tue informazioni DNS con i server dei nomi che abbiamo fornito.
 * Continua l'introduzione a IBM CIS, seguendo un'esercitazione o configurando altre funzioni.

### Passo 1: apri l'applicazione IBM CIS
{:#open-cis-application}

Apri il tuo [dashboard IBM Cloud](https://{DomainName}/catalog/). Quindi passa all'icona dell'applicazione IBM CIS selezionando la categoria **Infrastructure -> Network** nella barra di navigazione di sinistra del dashboard. Apri l'applicazione IBM Cloud Internet Services facendo clic sull'icona che vedrai vicino al centro della tua schermata. 

![Catalogo](images/catalog-cis-tile.png)

**La schermata della panoramica**

Una volta che l'applicazione IBM CIS è stata avviata, visualizzerai la schermata **Overview** di IBM CIS e troverai le schede **Security**, **Reliability** e **Performance** nell'area di sinistra della vista della IU.

**Quale piano scelgo?**

Ci sono 4 piani tra cui puoi scegliere:  
* **Enterprise Usage** 
* **Enterprise Package** 
* **Piano Standard** 
* **Free Trial**. 

**Free Trial** scade dopo 30 giorni, a quel punto puoi eseguire l'upgrade al **piano Standard** o a un **piano Enterprise**. Una singola istanza **Standard** può gestire un dominio. Puoi creare tutte le istanze del servizio **Standard** che desideri all'interno di un singolo account, ognuna delle quali gestisce un singolo dominio.  

I **piani Enterprise** ti consentono di gestire più domini in una singola istanza del servizio. Seleziona il pulsante **Create** sulla schermata **Overview** per avviare il provisioning del tuo account.

**Free Trial** è limitato a un'istanza per account.
{:note}

**Avvia il provisioning**

Visualizzerai la prima schermata dell'applicazione IBM CIS, in cui selezionerai il pulsante **Add Domain** per iniziare.


### Passo 2. Aggiungi e configura il tuo dominio.
{:#add-configure-your-domain}

Seleziona **Let's get started** dalla pagina di benvenuto per iniziare a configurare CIS.

![Introduzione](images/overview-setup-step1.png)

Poi, inizia proteggendo e migliorando le prestazioni del tuo servizio web immettendo il tuo dominio o dominio secondario. 

Specifica le zone DNS. Puoi configurare i server dei nomi per questi domini o domini secondari nella funzione di registrazione o nel provider DNS del dominio. Non utilizzare i CNAME.
{:note}

![Introduzione](images/overview-setup-step2.png)

La schermata della panoramica visualizzerà il tuo dominio nello stato `Pending`. Il tuo dominio rimarrà `Pending` finché non completi il passo 4. 

L'istanza di IBM CIS non può essere eliminata dopo che è stato aggiunto un dominio. Per eliminare l'istanza, elimina prima il dominio dall'istanza.
{:note}

### Passo 3. Configura i tuoi record DNS (facoltativo).
{:#setup-your-dns-records}

Prima di passare il traffico per il tuo dominio a CIS, ti consigliamo vivamente di importare o di ricreare i tuoi record DNS in CIS. Puoi scegliere di ignorare questo passo, ma se i tuoi record DNS non sono configurati correttamente in CIS, alcune parti del tuo sito web potrebbero rimanere inaccessibili. 

Importa i record caricando i tuoi record esportati dal tuo DNS corrente oppure crea manualmente i tuoi record DNS. Per importare i record, seleziona **Import records**.

![Introduzione](images/overview-setup-step3.png)

Una volta che hai terminato oppure se desideri ignorare questo passo, seleziona **Passo successivo**.

### Passo 4. Configura i tuoi server dei nomi con la funzione di registrazione o il provider DNS esistente.
{:#configure-your-name-servers-with-the-registrar-or-existing-dns-provider}

Per iniziare a usufruire dei vantaggi di IBM CIS, configura il provider del nome del dominio o la funzione di registrazione per utilizzare i server dei nomi elencati. Se stai delegando un dominio (qualcosa simile a `example.com`), configura i server dei nomi elencati nelle impostazioni del tuo dominio, dove sono gestiti dalla tua funzione di registrazione (ad esempio, nel portale web della funzione di registrazione). Se non sei sicuro di quale sia la funzione di registrazione del tuo dominio, puoi ricercarla all'indirizzo https://whois.icann.org/. Se deleghi un dominio secondario (ad esempio, `subdomain.example.com`) da un altro provider DNS, devi aggiungere un record Name Server (NS) ad ognuno dei server dei nomi elencato. Vedi [Managing DNS Records ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://support.cloudflare.com/hc/en-us/articles/360019093151-Managing-DNS-records-in-Cloudflare){:new_window}, scritto dai nostri partner di Cloudflare, per istruzioni dettagliate del provider.

Dopo aver configurato la funzione di registrazione o il provider DNS, possono essere necessarie fino a 24 ore perché le modifiche abbiano effetto. Una volta verificato che i server dei nomi specificati sono stati configurati correttamente per il tuo dominio o dominio secondario, lo stato cambia da `Pending` a `Active`. Dopo aver configurato i server dei nomi, puoi fare clic sul link "Recheck name servers" nella pagina `Overview` per potenzialmente accelerare l'attivazione del tuo dominio (puoi inviare questo controllo solo una volta in un'ora).

Lo stato del tuo dominio deve diventare `Active` entro 60 giorni oppure il tuo dominio e tutti i dati di configurazione verranno rimossi.
{:note}

![Introduzione](images/overview-setup-step4.png)

### Passo 5. Assicurati che IBM Cloud Internet Services stia risolvendo le informazioni del dominio per la tua applicazione, nome host o sito web. 
{:#ensure-cis-is-resolving-domain-info}

Per procedere, seleziona la scheda **Reliability** dalla tua barra di navigazione di sinistra, quindi seleziona l'opzione **DNS**. Assicurati di aggiungere i _Record DNS_ appropriati. Aggiungi **Un Record** e tutte le voci **AAAA** o **MX** che vengono popolate. Se dimentichi di aggiungere questi record prima del completamento della delega della funzione di registrazione, IBM Cloud Internet Services non può risolvere le informazioni del dominio per le tue applicazioni verso internet.

![Introduzione](images/dns-records.png)

### Passo 6. Nel frattempo, puoi iniziare a gestire altre funzioni di IBM CIS. 
{:#manage-other-cis-functions}

Per ulteriori dettagli sulla gestione delle altre funzioni, consulta le [istruzioni dettagliate](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cloud-internet-services-cis-deployment).
