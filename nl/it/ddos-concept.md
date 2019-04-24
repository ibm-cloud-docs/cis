---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Attack Concepts, Application layer attacks, common types of internet attacks

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Concetti sull'attacco Distributed Denial of Service (DDoS)
{:#distributed-denial-of-service-ddos-attack-concepts}

Gli attacchi DDoS sono tra i tipi più comuni di attacchi internet che si possono verificare sul tuo sito web o host.

## Cosa è un attacco DDoS?
{:#what-is-a-ddos-attack}

Un attacco distributed denial of service (DDoS) è un tentativo doloso di interrompere il traffico normale di un server, un servizio o una rete travolgendo la destinazione o la relativa infrastruttura circostante con una marea di traffico internet. Gli attacchi DDoS prendono efficacia utilizzando molti sistemi di computer compromessi come origini del traffico dell'attacco. Le macchine sfruttate possono includere computer o altre risorse di rete come i dispositivi IoT. Ad alto livello, un attacco DDoS è come un ingorgo di traffico che blocca un'autostrada, che previene al traffico regolare di arrivare alla destinazione desiderata.

## Come funziona un attacco DDoS?
{:#how-does-a-ddos-attack-work}

Un aggressore acquisisce il controllo di una rete di macchine online per eseguire un attacco DDoS. I computer e le altre macchine (come i dispositivi IoT) sono infetti da malware, trasformando ognuno di essi in un bot (o zombie). L'aggressore controlla il gruppo di bot, denominato _botnet_. 

Dopo aver stabilito una botnet, l'aggressore indirizza le macchine inviando istruzioni aggiornate ad ogni bot utilizzando il controllo remoto. Un indirizzo IP di destinazione può ricevere le richieste da una moltitudine di bot, portando il server o la rete di destinazione ha superare la capacità. Questo crea un DoS (denial-of-service) del traffico normale. Poiché ogni bot è un dispositivo internet legittimo, la suddivisione del traffico dell'attacco dal normale può essere difficile. 

## Quali sono i tipi comuni di attacchi DDoS?
{:#what-are-common-types-of-ddos-attacks}

I vettori di attacco DDoS riguardano vari componenti di una connessione di rete. Mentre quasi tutti gli attacchi DDoS implicano la sopraffazione di un dispositivo o una rete di destinazione, gli attacchi possono essere divisi in tre categorie. Un aggressore può utilizzare uno o più vettori di attacco e può anche ruotare questi vettori di attacco in base alle contromisure prese dal bersaglio.

I tipi comuni sono:

 * Attacchi al livello dell'applicazione (livello 7)
 * Attacchi al protocollo (livelli 3 e 4)
 * Attacchi volumetrici (attacchi di amplificazione)

### Attacchi al livello dell'applicazione
{:#application-layer-attacks}

A un attacco al livello dell'applicazione viene qualche volta fatto riferimento come a _attacco DDoS di livello 7_ (in riferimento al settimo livello del modello OSI). L'obiettivo di questi attacchi è di esaurire le risorse della vittima, colpendo il livello in cui vengono generate le pagine web nel server e consegnate ai visitatori in risposta alle richiese HTTP (ovvero, il livello dell'applicazione). Gli attacchi di livello 7 sono impegnativi, perché è difficile identificare il traffico come doloso.

### Attacchi al protocollo
{:#protocol-attacks}

Gli attacchi al protocollo utilizzano le debolezze nei livelli 3 e 4 dello stack del protocollo ISO per rendere il bersaglio inaccessibile. Questi attacchi, conosciuti anche come attacchi state-exhaustion, provocano un'interruzione del servizio consumando tutta la capacità della _tabella di stato_ disponibile dei server dell'applicazione web o delle risorse intermedie come i firewall e i programmi di bilanciamento del carico. 
  
### Attacchi volumetrici
{:#volumetric-attacks}

Questa categoria di attacchi tenta di creare una congestione consumando tutta la larghezza di banda disponibile tra il bersaglio e internet. Viene inviata una grande quantità di dati a un bersaglio utilizzando una forma di amplificazione o in altre parole creando un traffico enorme, come le richieste da una botnet. 


## Cosa posso fare se sono sotto un attacco DDoS?
{:#under-ddos-attack}

**Passo 1:** attiva “Defense mode" dalla schermata **Overview**. 

![Defense Mode](images/defense-mode.png)

**Passo 2:** imposta i tuoi record DNS sulla sicurezza massima.

**Passo 3:** non limitare la frequenza o le richieste da IBM CIS, abbiamo bisogno della larghezza di banda per aiutarti con la tua situazione.

**Passo 4:** blocca alcuni paesi o visitatori specifici se necessario.
