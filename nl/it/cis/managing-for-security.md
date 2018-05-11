---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gestisci il tuo IBM CIS per la sicurezza ottimale

Le impostazioni di sicurezza di IBM Cloud Internet Services (CIS) includono valori predefiniti sicuri progettati per impedire i falsi positivi e l'impatto negativo sul tuo traffico. Tuttavia, queste impostazioni predefinite sicure non forniscono il comportamento di sicurezza migliore per ogni cliente. Completa la seguente procedura per assicurarti che il tuo account CIS sia configurato in modo sicuro:

**Consigli e procedure consigliate:**

* Proteggi gli indirizzi IP di origine tramite proxy e aumentando l'offuscamento
* Configura il tuo livello di sicurezza selettivamente
* Attiva il tuo WAF (Web Application Firewall) in modo sicuro

## Procedura consigliata 1: proteggi i tuoi indirizzi IP di origine 

Quando un dominio secondario viene protetto tramite proxy utilizzando IBM CIS, viene protetto tutto il traffico perché rispondiamo attivamente agli indirizzi IP specifici di IBM CIS (ad esempio, tutti i nostri clienti si collegano prima ai proxy CIS e i tuoi indirizzi IP di origine sono oscurati).

### Utilizza i proxy IBM CIS per tutti i record DNS del traffico HTTP(S) dalla tua origine

Per migliorare la sicurezza del tuo indirizzo IP di origine, tutto il traffico HTTP(S) dovrebbe essere tramite proxy.

**Guarda la differenza da solo - Esegui la query di un record protetto da proxy e di uno senza:**

```
$ dig greycloud.theburritobot.com +short
1.2.3.4 (The origin IP address)

$ dig orangecloud.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (CIS IP addresses)
```

### Oscura i record di origine non tramite proxy con nomi non standard
Tutti i record che non possono essere protetti dal proxy tramite IBM CIS e che ancora utilizzano il tuo IP di origine, come ad esempio FTP, possono essere protetti creando un maggiore offuscamento. In particolare, se richiedi un record per la tua origine che non può essere protetto dal proxy da IBM CIS, utilizza un nome non standard. Ad esempio, invece di `ftp.example.com` utilizza `[random word or-random characters].example.com.` Questo offuscamento rende alle scansioni del dizionario dei tuoi record DNS meno probabile esporre i tuoi indirizzi IP di origine.

### Utilizza intervalli di IP separati per il traffico HTTP e non HTTP se possibile
Alcuni clienti utilizzano intervalli di IP separati per il traffico HTTP e non HTTP, consentendo quindi di proteggere tramite proxy tutti i record che puntano al proprio intervallo di IP HTTP e di oscurare tutto il traffico non HTTP con una sottorete di IP differente.

## Procedura consigliata 2: configura il tuo livello di sicurezza selettivamente 
Il tuo **Security Level** stabilisce la sensibilità del nostro **IP Reputation Database**. IBM CIS vede oltre 1 miliardo di indirizzi IP univoci ogni mese, da più di 7 milioni di siti web, che consente al nostro sistema di identificare gli aggressori e di impedirgli di raggiungere le tue risorse web. Per evitare interazioni negative o falsi positivi, configura il tuo **Security Level** dal dominio per accrescere la sicurezza quando necessario e per diminuirla dove appropriato.

### Aumenta il livello di sicurezza delle aree sensibili su 'High'
Puoi aumentare questa impostazione aggiungendo una **Page Rule** per le pagine di gestione o di accesso, per ridurre gli attacchi di forza bruta:

1. Crea una **Page Rule** con il modello dell'URL della tua API (ad esempio, `www.example.com/wp-login`). 
2. Identifica l'impostazione **Securty Level**.
3. Contrassegna l'impostazione come **High**.
4. Seleziona **Provision Resource**.

### Diminuisci il livello di sicurezza delle API o dei percorsi non sensili per ridurre i falsi positivi.
Questa impostazione può essere ridotta per le pagine generali e il traffico API: 

1. Crea una **Page Rule** con il modello dell'URL della tua API (ad esempio, `www.example.com/api/*`).
2. Identifica l'impostazione **Security Level**.
3. Imposta il livello di sicurezza su **Low** o **Essentially off**.
4. Seleziona **Provision Resource**.

### Cosa vogliono dire le impostazioni del livello di sicurezza?
Le nostre impostazioni del livello di sicurezza sono allineate con i punteggi della minaccia che alcuni indirizzi IP acquisiscono dal comportamento doloso sulla nostra rete. Un punteggio della minaccia superiore a 10 viene considerato alto.

* **HIGH**: vengono affrontati punteggi della minaccia superiori a 0.
* **MEDIUM**: vengono affrontati punteggi della minaccia superiori a 14.
* **LOW**: vengono affrontati punteggi della minaccia superiori a 24.
* **ESSENTIALLY**: vengono affrontati punteggi della minaccia superiori a 49.

Ti consigliamo di controllare le tue impostazioni del livello di sicurezza periodicamente e puoi trovare le istruzioni nelle nostre [Procedure consigliate per la documentazione di configurazione CIS](best-practices.html)

## Procedura consigliata 3: attiva il tuo WAF (Web Application Firewall) in modo sicuro
Il tuo WAF è disponibile nella sessione **Security**. Ti guideremo attraverso queste impostazioni in ordine inverso per assicurarci che il tuo WAF sia configurato nel modo più sicuro possibile prima di attivarlo per il tuo dominio completo. Queste impostazioni iniziali possono ridurre i falsi positivi popolando l'applicazione del traffico con gli eventi WAF per una maggiore ottimizzazione. Il tuo WAF viene aggiornato automaticamente per gestire le nuove vulnerabilità come vengono identificate.

WAF ti protegge dai seguenti tipi di attacco:
* Attacco SQL injection
* Cross-site scripting
* Cross-site forgery

WAF contiene una serie di regole predefinite che include le regole per fermare gli attacchi più comuni. In questo momento, ti permettiamo sia di abilitare che disabilitare WAF. Consulta il documento [Serie di regole predefinite WAF](waf-rule-set.html) per ulteriori dettagli sulla serie di regole predefinite e il comportamento di ogni regola.

Per ulteriori informazioni su WAF, consulta il [documento Concetti su WAF](waf-concept.html)

## Procedura consigliata 4: configura le tue impostazioni TLS
IBM CIS fornisce alcune opzioni per la codifica del tuo traffico. Come un proxy inverso, chiudiamo le connessioni TLS ai nostri data center e apriamo una nuova connessione TLS al tuo server di origine. 

TLS offre quattro modalità di funzionamento:
* **Off**: TLS è disabilitato in questa modalità, non è consigliato.
* **Client-to-edge**: TLS codifica il traffico da CIS ai tuoi client, ma non da CIS ai tuoi server di origine.
* **End-to-end flexible**: TLS codifica tutto il traffico; tuttavia, può utilizzare un certificato autofirmato per proteggere il traffico tra CIS e i tuoi server di origine.
* **End-to-end CA signed**: TLS codifica tutto il traffico; devi utilizzare un certificato firmato CA.

Per ulteriori dettagli sulle tue opzioni TLS, fai riferimento a [questo documento](ssl-options.html).

IBM CIS ti consente di utilizzare certificati personalizzati o un certificato con carattere jolly che ti ha fornito CIS.

### Carica un certificato personalizzato
Puoi caricare il tuo certificato personalizzato facendo clic sul pulsante **Add Certificate** e immettendo il certificato, la chiave privata e il metodo di bundle. Se carichi il tuo certificato, ottieni la compatibilità immediata e mantieni il controllo sul tuo certificato (ad esempio, un certificato di convalida estesa (EV)). Ricorda che sarai responsabile della gestione del tuo certificato se carichi un certificato personalizzato. Ad esempio, IBM CIS non traccia le date di scadenza del certificato. 

![certificato-personalizzato](images/upload-custom-certificate.png)

### Utilizza un certificato fornito
IBM ha collaborato con molte autorità di certificazione (CA) per fornire i certificati con carattere jolly del dominio ai nostri clienti. Potrebbe essere richiesta la verifica manuale per la configurazione di questi certificati. Il tuo team di supporto può aiutarti ad eseguire questi ulteriori passi. 
