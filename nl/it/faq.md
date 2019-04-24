---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: configuration domain, Free Trial plan, CIS instance

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}



# FAQ
{:#faq}

## Cosa è accaduto al piano Early Access che si trovava nel catalogo?
{:#cis-faq-early-access-plan}
{: faq}

Il piano Early Access è stato rimosso dal catalogo il 31 maggio 2018. È stato sostituito dal piano di pagamento Standard e da un nuovo piano Free Trial di 30 giorni. Se hai un'istanza del piano Early Access, esegui subito l'upgrade al piano Standard per evitare di perdere dati; non potrai creare un'istanza Free Trial se hai preso parte alla versione beta di Early Access.

## Cosa posso fare con un piano Free Trial?
{:#cis-faq-free-trial-plan}
{: faq}

Il piano Free Trial, come progettato, consente solo una zona per account. Ti consigliamo di creare una sola istanza per account e di verificare il nome della zona. È molto importante che il nome della zona venga verificato prima di essere aggiunto. Se una zona viene eliminata, un'altra zona o la stessa zona non possono essere aggiunte durante il piano Free Trial. 

## Quante istanze del piano Free Trial posso avere?
{:#cis-faq-free-trial-instances}
{: faq}

Puoi avere massimo un'istanza Free Trial per account, per tutta la durata dell'account. Se hai già un'istanza Free Trial, oppure se elimini un'istanza Free Trial o se Free Trial scade, non potrai creare un'altra istanza Free Trial. Puoi, tuttavia, creare istanze di altri piani a pagamento (ad esempio, Standard), indipendenti da qualsiasi Free Trial tu possa aver creato. 

## Ho un'istanza del servizio sottoscritta al piano Early Access. Posso modificarla in una Free Trial?
{:#cis-faq-early-access-to-free-trial-plan}
{: faq}

No. Puoi eseguire solo l'upgrade del piano Early Access a un piano a pagamento che in questo momento è il piano Standard. 

## Avevo un'istanza Early Access che potrei aver eliminato o meno. Posso creare ora un'istanza Free Trial?
{:#cis-faq-early-access-and-free-trial-plan}
{: faq}

No. Ciascun account ha diritto ad una sola istanza gratuita. Sia il piano Early Access che il piano Free Trial che lo ha sostituito la conteggiano come piani gratuiti. Ciò significa anche che puoi avere al massimo un'istanza Free Trial.

## Posso eseguire il downgrade da Standard a Free Trial?
{:#cis-faq-downgrade-standard-to-free-plan}
{: faq}

No. Non è consentito. 

## Il mio Free Trial è scaduto. Quali sono le mie opzioni?
{:#cis-faq-free-trial-plan-expired}
{: faq}

Per evitare perdite di dati, devi eseguire l'upgrade da Free Trial a Standard prima della data di scadenza. Dopo di che, supportiamo solo l'upgrade del piano o l'eliminazione dell'istanza CIS. Se l'istanza non viene eliminata o non viene eseguito l'upgrade dopo 45 giorni (dall'avvio dell'istanza), il dominio di configurazione, il GLB, i pool e i controlli di integrità vengono eliminati automaticamente.

## Come elimino la mia istanza CIS?
{:#{:#cis-faq-delete-instance}
{: faq}

Per eliminare un'istanza CIS, devi innanzitutto eliminare tutti i GLB, i pool e i controlli di integrità. Quindi elimina il dominio associato (zona). Vai alla pagina **Overview** e fai clic sull'icona del cestino accanto al nome del dominio che si trova nella sezione **Service Details** per avviare il processo di eliminazione. 

## Ho aggiunto un utente al mio account e gli ho concesso l'autorizzazione utente per gestire le istanze Internet Services. Perché tale utente sta riscontrando problemi di autenticazione? 
{:#cis-faq-user-authentication-issue}
{: faq}

È possibile che tu non abbia assegnato i ruoli di accesso al servizio all'utente. Tieni presente che esistono due serie separate di ruoli: "accesso alla piattaforma" e "accesso al servizio". I ruoli di accesso alla piattaforma sono obbligatori per creare e gestire le istanze del servizio, ma i ruoli di accesso al servizio sono obbligatori per eseguire operazioni specifiche del servizio sulle istanze del servizio. Nella console, queste impostazioni possono essere aggiornate selezionando **Manage > Security > Identity and Access**.

## Perché il mio dominio è nello stato in sospeso? Come lo attivo?
{:#cis-faq-pending-domain}
{: faq}

Quando aggiungi un dominio a CIS, ti forniamo un paio di server dei nomi da configurare nella tua funzione di registrazione (o nel tuo provider DNS, se stai aggiungendo un dominio secondario). Il dominio o il dominio secondario rimane nello stato in sospeso finché non configuri i server dei nomi correttamente. Assicurati di aggiungere entrambi i server dei nomi alla tua funzione di registrazione o provider DNS. Eseguiamo periodicamente la scansione del sistema DNS pubblico per controllare se i server dei nomi sono stati configurati come indicato. Non appena siamo in grado di verificare la modifica al server dei nomi (possono essere necessarie fino a 24 ore), attiviamo il dominio. Puoi inviare una richiesta per ricontrollare i server dei nomi facendo clic su **Recheck nameservers** nella pagina della panoramica.

## Qual è la funzione di registrazione del mio dominio?
{:#cis-faq-who-is-registrar}
{: faq}

Consulta https://whois.icann.org/ per queste informazioni. **Nota**: devi avere i privilegi amministrativi per modificare la configurazione del tuo dominio nella funzione di registrazione per aggiornare o aggiungere i server dei nomi forniti al tuo dominio quando lo hai aggiunto a CIS. Se non conosci quale è la funzione di registrazione del dominio che stai tentando di aggiungere a CIS, è probabile che non disponi dell'autorizzazione per aggiornare la configurazione del tuo dominio nella funzione di registrazione. Collabora con il proprietario del dominio nella tua organizzazione per apportare le modifiche necessarie.

## Voglio conservare il mio provider DNS corrente del mio dominio (example.com). Posso delegare un dominio secondario (subdomain.example.com) dal mio provider DNS corrente a CIS?
{:#cis-faq-keep-current-dns-provider}
{: faq}

Sì. Il processo è simile all'aggiunta di un dominio, ma invece della funzione di registrazione, utilizzi il provider DNS per il dominio di livello superiore. Quando aggiungi un dominio secondario a CIS, ti vengono forniti due server dei nomi da configurare, come al solito. Configura un record Name Server (NS) per ognuno dei due server dei nomi come i record DNS nel tuo dominio che stanno venendo gestiti dall'altro provider DNS. Quando siamo in grado di verificare che i record NS richiesti sono stati aggiunti, attiviamo il tuo dominio secondario. Se non gestisci il dominio di livello superiore nella tua organizzazione, devi collaborare con il proprietario di tale dominio per aggiungere i record NS.

## Cosa è TLS?
{:#cis-faq-what-is-tls}
{: faq}

TLS è un protocollo di sicurezza standard per stabilire i link codificati tra un server web e un browser in una comunicazione online. È necessario un certificato TLS per creare una connessione TLS con un sito web e che comprende il nome del dominio, il nome dell'azienda e ulteriori dati come l'indirizzo, la città, lo stato e il paese dell'azienda. Il certificato mostra inoltre la data di scadenza e i dettagli della autorità di certificazione (CA) di emissione.

## Come funziona TLS?
{:#cis-faq-how-does-tls-work}
{: faq}

Quando un browser web inizia una connessione con un sito web protetto da TLS, per prima cosa richiama il certificato TLS del sito per verificare che sia ancora valido. Verifica che la CA sia una di quelle attendibili del browser e che il certificato stia venendo utilizzato dal sito web per il quale è stato emesso. Se uno di questi controlli non riesce, riceverai un'avvertenza che indica che il sito web non è protetto da un certificato valido.

Quando un certificato TLS è installato su un server web, abilita una connessione sicura tra il server web e il browser che si collega. L'URL del sito web è preceduto da "https" invece di "http" e viene visualizzato un lucchetto chiuso nella barra degli indirizzi. Se un sito web utilizza un certificato di convalida estesa (EV), il browser potrebbe inoltre visualizzare una barra degli indirizzi verde.

## Perché visualizzo una avvertenza sulla privacy?
{:#cis-faq-privacy-warning}
{: faq}

I certificati TLS emessi da IBM Cloud CIS coprono il dominio root (`example.com`) e un livello del dominio secondario (`*.example.com`). Se stai tentando di raggiungere un dominio secondario di secondo livello (`*.*.example.com`) visualizzerai un'avvertenza sulla privacy nel tuo browser, perché questi nomi host non sono aggiunti nella SAN.

Inoltre, concedi almeno 15 minuti a una delle nostre autorità di certificazione (CA) partner per emettere un nuovo certificato. Visualizzerai un'avvertenza sulla privacy nel tuo browser se il tuo nuovo certificato non è ancora stato emesso.

## Perché visualizzo un errore di certificato SSL non valido?
{:#cis-faq-invalid-ssl-cert-error}
{: faq}

Se visualizzi "Error 526, Invalid SSL Certificate" quando visiti il tuo sito, potrebbe significare che il tuo certificato di origine non è valido. Quando viene abilitato il proxy CIS, è necessario un certificato firmato CA all'origine nella modalità SSL predefinita, "End-to-end CA Signed". Tieni presente che l'impostazione predefinita per la modalità SSL era, in precedenza, "End-to-end Flexible", che ignora la validità del certificato presentato dall'origine. Il nuovo valore predefinito viene applicato solo ai domini aggiunti daccapo. Se il tuo dominio è stato scritto quando la modalità SSL predefinita era End-to-end Flexible, tale impostazione non viene sovrascritta. Puoi cambiare la modalità con una meno rigida, ma è sconsigliato per gli ambienti di produzione. 

## Cosa è DDoS?
{:#cis-faq-what-is-ddos}
{: faq}

Un attacco distributed denial-of-service (DDoS) è un tentativo di rendere un servizio online non disponibile travolgendolo con il traffico da più origini. In un attacco DDoS, più sistemi di computer compromessi attaccano un bersaglio come un server, un sito web o un'altra risorsa di rete e che influenza gli utenti della risorsa di destinazione.

Il flusso di messaggi in entrata, richieste di connessione o pacchetti malformati al sistema bersaglio lo costringe a rallentare o anche ad arrestarsi e spegnersi, negando quindi il servizio agli utenti o ai sistemi legittimi. Gli attacchi DDoS vengono eseguiti da diversi aggressori, da pirati informatici individuali a organizzazioni criminali e agenzie governative.

## Cosa posso fare se sono sotto un attacco DDoS?
{:#cis-faq-what-to-do-in-ddos}
{: faq}

**Passo 1:** attiva “Defense mode" nella schermata **Overview**. 

![Defense Mode](images/defense-mode.png)

**Passo 2:** imposta i tuoi record DNS sulla sicurezza massima.

**Passo 3:** non limitare la frequenza o le richieste da IBM CIS, abbiamo bisogno della larghezza di banda per aiutarti con la tua situazione.

**Passo 4:** blocca alcuni paesi o visitatori specifici se necessario.

## Ricevo un errore 522, cosa faccio ora?
{:#cis-faq-522-error}
{: faq}

Un errore 522 indica che non siamo in grado di stabilire una connessione con il tuo server di origine (ovvero, il tuo host). Dopo circa 15 secondi di connessione non riuscita, chiudiamo la connessione e visualizziamo una pagina di errore 522.

Questo problema normalmente viene causato dal firewall o dal software di sicurezza che accidentalmente blocca i nostri indirizzi IP. Poiché CIS funziona come un proxy inverso, le connessioni al tuo sito saranno visualizzate come provenienti da un intervallo di IP CIS. Questo comportamento può comportare che certi firewall bloccano queste connessioni, che ci impedisce di fornire il contenuto ai tuoi visitatori del sito correttamente.

Per risolvere questo problema, chiedi al tuo host di aggiungere alla whitelist tutti gli intervalli di IP CIS, elencati [qui](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses).

Tutti questi IP devono essere aggiunti alla whitelist per evitare gli errori 522. Vale anche la pena di controllare se gli IP in questi intervalli sono bloccati.

Gli errori 522 possono inoltre essere causati da problemi di connettività di rete, conferma quindi che i tuoi server e rete siano generalmente integri e non sovraccaricati.

Se dopo aver seguito i precedenti passi ricevi ancora gli errori, contatta il supporto IBM CIS e conferma quanto segue: 

* Hai aggiunto alla whitelist i nostri intervalli di IP
* I tuoi server/rete sono online e generalmente integri

Se contatti il nostro team di supporto, fornisci un ID raggio da un errore 522 recente. Possiamo utilizzarlo per determinare su quale data center stavi provando ed eseguendo i test.

## Cosa è un record con proxy e perché ne ho bisogno?
{:#cis-faq-proxied-record}
{: faq}

I record con proxy sono record che trasmettono tramite proxy il loro traffico attraverso IBM CIS. Solo i record con proxy ricevono i vantaggi di CIS, come il mascheramento dell'IP, dove un IP CIS viene sostituito al tuo IP di origine per proteggerlo:

```
$ whois 104.28.22.57 | grep OrgName
OrgName:        IBM
```

Se al contrario preferisci ignorare CIS per un dominio (continueremo a risolvere con DNS), la non trasmissione tramite proxy del record costituisce una soluzione possibile. 

## Ho ricevuto un errore di convalida DNS: 1004; ora cosa posso fare?
{:#cis-faq-dns-validation-error}
{: faq}

Per il funzionamento delle regole della pagina, DNS ha bisogno di risolvere per la tua zona. Di conseguenza, devi avere un record DNS con proxy per la tua zona. 

## Posso aggiungere un CNAME per un record root?
{:#cis-faq-add-cname-root-record}
{: faq}

Sì. IBM CIS supporta una funzione denominata "flattening del CNAME" che consente ai nostri utenti di aggiungere un CNAME come un record root. I nostri server DNS autorevoli elencano i record della destinazione CNAME e rispondono con quei record invece che con il CNAME stesso, nascondendo effettivamente il fatto che l'utente ha configurato un CNAME nella root del dominio. 

## Qual è il timeout predefinito per il controllo di integrità?
{:#cis-faq-default-health-check-timeout}
{: faq}

Il timeout predefinito del controllo di integrità per i piani Free Trial e Standard è di 60 secondi.

## I controlli di integrità possono essere configurati per il traffico non HTTP/HTTPS?
{:#cis-faq-health-check-non-http-traffic}
{: faq}

No, possono essere configurati solo con HTTP/HTTPS.

## Il GLB può essere configurato per il traffico non HTTP/HTTPS? 
{:#cis-faq-glb-non-http-traffic}
{: faq}

No, possono essere configurati solo con HTTP/HTTPS.

## Se disabilito tutte le mie origini in un pool di origini, disabilito l'intero pool di origini stesso? 
{:#cis-faq-disabling-origins-disable-origin-pool}
{: faq}

Sì, se il pool di origini viene utilizzato in un programma di bilanciamento del carico, il traffico viene instradato al successivo pool con priorità più elevata o al pool di fallback.

## Ho un errore nel mio Ingress Kubernetes, cosa faccio?
{:#cis-faq-kubernetes-ingress-error}
{: faq}

Il nome host in un Ingress Kubernetes deve essere composto da caratteri alfanumerici minuscoli, '-' oppure '.' e deve iniziare e finire con un carattere alfanumerico. L'utilizzo di `_` nel nome del programma di bilanciamento del carico, sebbene consentito, può causare un errore Ingress nei cluster Kubernetes. Ti consigliamo di non utilizzare `-` nel nome del programma di bilanciamento del carico per evitare problemi con i cluster Kubernetes.

## Ho ricevuto un errore 502 mentre tentavo di salvare un'azione delle funzioni edge, cosa faccio? 
{:#cis-faq-502-error}
{: faq}

Contatta il [supporto IBM](/docs/infrastructure/cis?topic=cis-getting-help-and-support) e fornisci lo script che stavi tentando di salvare.
