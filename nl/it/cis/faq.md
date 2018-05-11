---
copyright:
  years: 2018
lastupdated: "2018-28-03"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# FAQ

## Cosa posso fare con un piano Early Access?
Il programma Early Access, come progettato, consente solo una zona per account. Ti consigliamo di creare una sola istanza per account e di verificare il nome della zona. È molto importante che il nome della zona venga verificato prima di essere aggiunto. Se una zona viene eliminata, un'altra zona o la stessa zona non possono essere aggiunte durante il programma Early Access.

## Perché il mio dominio è nello stato in sospeso? Come lo attivo?
Quando aggiungi un dominio a CIS, ti forniamo un paio di server dei nomi da configurare nella tua funzione di registrazione (o nel tuo provider DNS, se stai aggiungendo un dominio secondario). Il dominio o il dominio secondario rimane nello stato in sospeso finché non configuri i server dei nomi correttamente. Assicurati di aggiungere entrambi i server dei nomi alla tua funzione di registrazione o provider DNS. Eseguiamo periodicamente la scansione del sistema DNS pubblico per controllare se i server dei nomi sono stati configurati come indicato. Non appena siamo in grado di verificare la modifica al server dei nomi (possono essere necessarie fino a 24 ore), attiviamo il dominio. Puoi inviare una richiesta per ricontrollare i server dei nomi facendo clic su **Recheck nameservers** nella pagina della panoramica.

## Qual è la funzione di registrazione del mio dominio?
Consulta https://whois.icann.org/ per queste informazioni. **Nota**: devi avere i privilegi amministrativi per modificare la configurazione del tuo dominio nella funzione di registrazione per aggiornare o aggiungere i server dei nomi forniti al tuo dominio quando lo hai aggiunto a CIS. Se non conosci quale è la funzione di registrazione del dominio che stai tentando di aggiungere a CIS, è probabile che non disponi dell'autorizzazione per aggiornare la configurazione del tuo dominio nella funzione di registrazione. Collabora con il proprietario del dominio nella tua organizzazione per apportare le modifiche necessarie.

## Voglio conservare il mio provider DNS corrente del mio dominio (example.com). Posso delegare un dominio secondario (subdomain.example.com) dal mio provider DNS corrente a CIS?
Sì. Il processo è simile all'aggiunta di un dominio, ma invece della funzione di registrazione, utilizzi il provider DNS per il dominio di livello superiore. Quando aggiungi un dominio secondario a CIS, ti vengono forniti due server dei nomi da configurare, come al solito. Configura un record Name Server (NS) per ognuno dei due server dei nomi come i record DNS nel tuo dominio che stanno venendo gestiti dall'altro provider DNS. Quando siamo in grado di verificare che i record NS richiesti sono stati aggiunti, attiviamo il tuo dominio secondario. Se non gestisci il dominio di livello superiore nella tua organizzazione, devi collaborare con il proprietario di tale dominio per aggiungere i record NS.

## Cosa è TLS?
TLS è un protocollo di sicurezza standard per stabilire i link codificati tra un server web e un browser in una comunicazione online. È necessario un certificato TLS per creare una connessione TLS con un sito web e che comprende il nome del dominio, il nome dell'azienda e ulteriori dati come l'indirizzo, la città, lo stato e il paese dell'azienda. Il certificato mostra inoltre la data di scadenza e i dettagli della autorità di certificazione (CA) di emissione.

## Come funziona TLS?
Quando un browser web inizia una connessione con un sito web protetto da TLS, per prima cosa richiama il certificato TLS del sito per verificare che sia ancora valido. Verifica che la CA sia una di quelle attendibili del browser e che il certificato stia venendo utilizzato dal sito web per il quale è stato emesso. Se uno di questi controlli non riesce, riceverai un'avvertenza che indica che il sito web non è protetto da un certificato valido.

Quando un certificato TLS è installato su un server web, abilita una connessione sicura tra il server web e il browser che si collega. L'URL del sito web è preceduto da "https" invece di "http" e viene visualizzato un lucchetto chiuso nella barra degli indirizzi. Se un sito web utilizza un certificato di convalida estesa (EV), il browser potrebbe inoltre visualizzare una barra degli indirizzi verde.

## Perché visualizzo una avvertenza sulla privacy?
I certificati TLS emessi da IBM Cloud CIS coprono il dominio root (`example.com`) e un livello del dominio secondario (`*.example.com`). Se stai tentando di raggiungere un dominio secondario di secondo livello (`*.*.example.com`) visualizzerai un'avvertenza sulla privacy nel tuo browser, perché questi nomi host non sono aggiunti nella SAN.

Inoltre, concedi almeno 15 minuti a una delle nostre autorità di certificazione (CA) partner per emettere un nuovo certificato. Visualizzerai un'avvertenza sulla privacy nel tuo browser se il tuo nuovo certificato non è ancora stato emesso.

## Cosa è DDoS?
Un attacco distributed denial-of-service (DDoS) è un tentativo di rendere un servizio online non disponibile travolgendolo con il traffico da più origini. In un attacco DDoS, più sistemi di computer compromessi attaccano un bersaglio come un server, un sito web o un'altra risorsa di rete e che influenza gli utenti della risorsa di destinazione.

Il flusso di messaggi in entrata, richieste di connessione o pacchetti malformati al sistema bersaglio lo costringe a rallentare o anche ad arrestarsi e spegnersi, negando quindi il servizio agli utenti o ai sistemi legittimi. Gli attacchi DDoS vengono eseguiti da diversi aggressori, da pirati informatici individuali a organizzazioni criminali e agenzie governative.

## Cosa posso fare se sono sotto un attacco DDoS?

**Passo 1:** attiva “Defense mode" nella schermata **Overview**.  

![Defense Mode](images/defense-mode.png)

**Passo 2:** imposta i tuoi record DNS sulla sicurezza massima.

**Passo 3:** non limitare la frequenza o le richieste da IBM CIS, abbiamo bisogno della larghezza di banda per aiutarti con la tua situazione.

**Passo 4:** blocca alcuni paesi o visitatori specifici se necessario.

## Ricevo un errore 522, cosa faccio ora?

Un errore 522 indica che non siamo in grado di stabilire una connessione con il tuo server di origine (ovvero, il tuo host). Dopo circa 15 secondi di connessione non riuscita, chiudiamo la connessione e visualizziamo una pagina di errore 522.

Questo problema normalmente viene causato dal firewall o dal software di sicurezza che accidentalmente blocca i nostri indirizzi IP. Poiché CIS funziona come un proxy inverso, le connessioni al tuo sito saranno visualizzate come provenienti da un intervallo di IP CIS. Questo comportamento può comportare che certi firewall bloccano queste connessioni, che ci impedisce di fornire il contenuto ai tuoi visitatori del sito correttamente.

Per risolvere questo problema, chiedi al tuo host di aggiungere alla whitelist tutti gli intervalli di IP CIS, elencati [qui](whitelisted-ips.html).

Tutti questi IP devono essere aggiunti alla whitelist per evitare gli errori 522. Vale anche la pena di controllare se gli IP in questi intervalli sono bloccati.

Gli errori 522 possono inoltre essere causati da problemi di connettività di rete, conferma quindi che i tuoi server e rete siano generalmente integri e non sovraccaricati.

Se dopo aver seguito i precedenti passi ricevi ancora gli errori, contatta il supporto IBM CIS e conferma quanto segue:

* Hai aggiunto alla whitelist i nostri intervalli di IP
* I tuoi server/rete sono online e generalmente integri

Se contatti il nostro team di supporto, fornisci un ID raggio da un errore 522 recente. Possiamo utilizzarlo per determinare su quale data center stavi provando ed eseguendo i test.

## Cosa è un record con proxy e perché ne ho bisogno?

I record con proxy sono record che trasmettono tramite proxy il loro traffico attraverso IBM CIS. Solo i record con proxy ricevono i vantaggi di CIS, come il mascheramento dell'IP, dove un IP CIS viene sostituito al tuo IP di origine per proteggerlo:

```
$ whois 104.28.22.57 | grep OrgName
OrgName:        IBM
```

Se al contrario preferisci ignorare CIS per un dominio (continueremo a risolvere con DNS), la non trasmissione tramite proxy del record sarebbe una soluzione possibile.

## Ho ricevuto un errore di convalida DNS: 1004; ora cosa posso fare?

Per il funzionamento delle regole della pagina, DNS ha bisogno di risolvere per la tua zona. Di conseguenza, devi avere un record DNS con proxy per la tua zona. 
