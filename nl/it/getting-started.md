---
copyright:
  years: 2018
lastupdated: "2018-03-19"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Introduzione a IBM Cloud Internet Services (CIS)

IBM Cloud Internet Services (CIS) offre tre funzionalità principali per migliorare il tuo flusso di lavoro: [sicurezza](/docs/infrastructure/cis/managing-for-security.html), [affidabilità](/docs/infrastructure/cis/managing-for-reliability.html) e [prestazioni](/docs/infrastructure/cis/managing-for-performance.html). Ogni area della funzionalità viene rappresentata nella barra di navigazione di sinistra della tua schermata, dopo che hai aperto l'applicazione IBM CIS.

Per ogni funzionalità, IBM CIS ti aiuta a ottimizzare le sue funzioni per soddisfare i tuoi bisogni specifici, tra cui:

 * Server DNS autorevoli
 * Bilanciamento del carico locale e globale 
 * WAF (Web Application Firewall)
 * Protezione DDoS
 * Memorizzazione nella cache e regole della pagina



## Prima di iniziare
Prima di iniziare ad utilizzare IBM CIS, avrai prima bisogno di un [ID IBM](https://www.ibm.com/account/us-en/signup/register.html). Dopodiché puoi ordinare i tuoi servizi tramite l'account IBM Cloud o il nuovo [Portale IBM Cloud Internet Services](https://console.bluemix.net/catalog/services/internet-services), a seconda della tua preferenza.

Se hai bisogno di assistenza per ottenere un account per utilizzare IBM Cloud Internet Services, [contatta il tuo rappresentante delle vendite IBM](https://www.ibm.com/cloud-computing/bluemix/contact-us) per ulteriori informazioni introduttive.

Se hai un account Softlayer esistente, puoi [collegare il tuo account](https://console.bluemix.net/docs/account/softlayerlink.html#unifyingaccounts) al tuo ID IBM. 

## Panoramica del processo

Puoi iniziare ad utilizzare IBM CIS per il tuo traffico internet con pochi passi.

 * Apri l'applicazione IBM CIS dal tuo dashboard IBM Cloud.
 * Aggiungi il dominio che vuoi gestire. 
 * Configura le tue informazioni DNS con i server dei nomi che abbiamo fornito. 
 * Continua l'introduzione a IBM CIS, seguendo un'esercitazione o configurando altre funzioni.

### Passo 1: apri l'applicazione IBM CIS 

Apri il tuo [dashboard IBM Cloud](https://console.bluemix.net/catalog/). Quindi passa all'icona dell'applicazione IBM CIS selezionando la categoria **Platform -> Network** nella barra di navigazione di sinistra del dashboard. Apri l'applicazione IBM Cloud Internet Services facendo clic sull'icona che vedrai vicino al centro della tua schermata. 

![Catalogo](images/catalog-cis-tile.png)

**La schermata della panoramica**

Una volta che l'applicazione IBM CIS è stata avviata, visualizzerai la schermata **Overview** di IBM CIS e troverai le schede **Security**, **Reliability** e **Perfomance** nell'area di sinistra della vista della IU.

**Quale piano scelgo?**

Per la release _Early Access_, c'è solo un piano che puoi scegliere ed è gratuito. Fai clic sul pulsante **Create** in basso a sinistra nella tua schermata **Overview** per avviare il provisioning del tuo account.

**Avvia il provisioning**

Visualizzerai la prima schermata dell'applicazione IBM CIS, in cui selezionerai il pulsante **Add Domain** per iniziare.

|**Nota che il programma Early Access è limitato a una istanza per account.** |
|-------------------------------------------------------------------|
| Dopo aver creato un'istanza della risorsa e aggiunto un dominio ad essa, non ti è consentito aggiungere nuove istanze della risorsa a IBM CIS. Questa limitazione viene applicata anche se elimini un dominio di prova e poi tenti di aggiungere nuovamente un dominio alla stessa istanza della risorsa. Riceverai un errore se tenti di farlo.|

### Passo 2. Aggiungi e configura il tuo dominio.

Inizia proteggendo e migliorando le prestazioni del tuo servizio web immettendo il tuo dominio o dominio secondario.

**Nota:** specifica le zone DNS. Puoi configurare i server dei nomi per questi domini o domini secondari nella funzione di registrazione o nel provider DNS del dominio. Non utilizzare i CNAME.

![Introduzione](images/overview-add-domain.png)
th
La schermata della panoramica visualizzerà il tuo dominio nello stato `Pending`. Il tuo dominio rimarrà `Pending` finché non completi il passo 3.

**Nota:** l'istanza di IBM CIS non può essere eliminata dopo che è stato aggiunto un dominio. Per eliminare l'istanza, elimina prima il dominio dall'istanza.

### Passo 3. Configura i tuoi server dei nomi con la funzione di registrazione o il provider DNS esistente.

Per iniziare a usufruire dei vantaggi di IBM CIS, configura il provider del nome del dominio o la funzione di registrazione per utilizzare i server dei nomi elencati. Se stai delegando un dominio (qualcosa simile a `example.com`), configura i server dei nomi elencati nelle impostazioni del tuo dominio, dove sono gestiti dalla tua funzione di registrazione (ad esempio, nel portale web della funzione di registrazione). Se non sei sicuro di quale sia la funzione di registrazione del tuo dominio, puoi ricercarla all'indirizzo https://whois.icann.org/. Se deleghi un dominio secondario (ad esempio, `subdomain.example.com`) da un altro provider DNS, devi aggiungere un record Name Server (NS) ad ognuno dei server dei nomi elencato.

Dopo aver configurato la funzione di registrazione o il provider DNS, possono essere necessarie fino a 24 ore perché le modifiche abbiano effetto. Una volta verificato che i server dei nomi specificati sono stati configurati correttamente per il tuo dominio o dominio secondario, lo stato cambia da `Pending` a `Active`. Dopo aver configurato i server dei nomi, puoi fare clic sul link "Recheck name servers" nella pagina `Overview` per potenzialmente accelerare l'attivazione del tuo dominio (puoi inviare questo controllo solo una volta in un'ora).

### Passo 4. Assicurati che IBM Cloud Internet Services stia risolvendo le informazioni del dominio per la tua applicazione, nome host o sito web.

Per procedere, seleziona la scheda **Reliability** dalla tua barra di navigazione di sinistra, quindi seleziona l'opzione **DNS**. Assicurati di aggiungere i _Record DNS_ appropriati. Aggiungi **Un Record** e tutte le voci **AAAA** o **MX** che vengono popolate. Se dimentichi di aggiungere questi record prima del completamento della delega della funzione di registrazione, IBM Cloud Internet Services non può risolvere le informazioni del dominio per le tue applicazioni verso internet.  

![Introduzione](images/dns-records.png)

### Passo 5. Nel frattempo, puoi iniziare a gestire altre funzioni di IBM CIS.

Per ulteriori dettagli sulla gestione delle altre funzioni, consulta le [istruzioni dettagliate](/docs/infrastructure/cis/how-to.html).
