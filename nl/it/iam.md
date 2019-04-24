---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Access Group Writer role, CIS instance, IAM

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# IAM e CIS
{:#iam-and-cis}

IBM Cloud Internet Services (CIS) si avvale di IAM per eseguire l'autorizzazione e l'autenticazione. 

Se non desideri aggiungere nessuno alla tua istanza CIS, puoi ignorare questa pagina.
{:note}

Limita l'accesso tramite tre ambiti funzionali CIS, in base alla struttura ad albero di navigazione:  
* affidabilità - ad esempio DNS, GLB
* sicurezza - ad esempio, certificato, regole di IP Firewall e limitazione della frequenza
* prestazioni - ad esempio regole della pagina, memorizzazione nella cache e instradamento

Questa sezione illustra come fornire un controllo di accesso dettagliato della tua istanza. 

## Ruoli
{:#iam-and-cis-roles}

Utilizza i seguenti tre ruoli per avvalerti di IAM
* Lettore - In grado di ottenere informazioni sull'istanza e sul dominio
* Scrittore - In grado di apportare modifiche alla configurazione esistente
* Gestore - In grado di creare o eliminare le istanze, i domini, la configurazione

## Gruppi di accesso e utenti
{:#iam-and-cis-access-groups-users}

Una politica può essere assegnata a un utente direttamente o a un gruppo di accesso.
Ti consigliamo di assegnarla a un gruppo di accesso per ridurre il numero di politiche create e l'impegno nella gestione di queste politiche. 

## Cache
{:#iam-and-cis-cache}

Memorizziamo nella cache i risultati di autorizzazione e utilizziamo la cache per prendere una decisione quando arriva di nuovo la stessa richiesta. Una volta che la cache raggiunge il suo TTL (Time to Live) (10 minuti), scade.

## Procedure consigliate
{:#iam-and-cis-best-practices}

1. Invece di modificare una politica, elimina la politica esistente e poi creane una nuova. 

## Scenari
{:#iam-and-cis-scenarios}

Questa sezione illustra i diversi esempi di politiche di accesso create tramite CIS. 

### Livello di dominio con tipo `config`
{:#iam-and-cis-scenarios-domain-level}

#### Accesso al singolo dominio con `security config` in un gruppo di accesso
##### Ruolo Scrittore

Bob ha un'istanza CIS, `cis-test-instance`, e due domini, `bob.com` e `bob-ibm.com`.
Bob vuole fornire a tutti gli ingegneri della sicurezza (sec-group) della società, l'accesso al ruolo Scrittore solo per la **configurazione della sicurezza** di **`bob.com`**.

Questi passi mostrano come creare una politica IAM per rendere possibile questo scenario.

Una volta che Bob accede a cis-test-instance:
1. Fa clic sulla scheda **Account > Access** nella barra di navigazione
1. Seleziona il **gruppo di accesso** - **sec-group** a cui desidera fornire l'accesso
1. Seleziona **`bob.com`**
1. Seleziona il ruolo Scrittore (**Writer**)
1. Seleziona l'opzione **Security config**
1. Fa clic su **create policy**

Nella scheda Manage:
Vengono create le seguenti politiche per **sec-group**:

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e

Service Instance 
    name: cis-test-instance  
    id: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9 
Domain 
    name: bob.com
    id: 4b23ec772965f672f96f05670e36827e 
Config Type
    cfgType: security
```

Ora sec-group ha l'accesso per vedere solo `bob.com` e può modificare i valori relativi alla sicurezza.  

##### Aggiornamento da Scrittore a Gestore per un gruppo di accesso

Se Bob desidera aggiornare il ruolo di sec-group da Scrittore a Gestore, deve eliminare la politica esistente.  
1. Vai alla **scheda Manage IAM > Access groups > sec-group > access policies**
1. Elimina la seguente politica 
  ```
  Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
  ```

Quindi, Bob deve creare la nuova politica. 
1. Fai clic sulla scheda **Account > Access** nella barra di navigazione
1. Seleziona il **gruppo di accesso** - **sec-group** a cui desideri fornire l'accesso
1. Seleziona **`bob.com`**
1. Seleziona il ruolo Gestore (**Manager**)
1. Seleziona l'opzione **Security config**
1. Fai clic su **create policy**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

Se la politica esistente (writer) non viene eliminata, il tentativo di creare la politica per Gestore avrà esito negativo. 

##### Aggiornamento della configurazione per includere le prestazioni con la sicurezza

Se Bob desidera fornire l'accesso Gestore a sec-group per la configurazione delle prestazioni in `bob.com` insieme alla sicurezza: 
1. Fa clic sulla scheda **Account > Access** nella barra di navigazione
1. Seleziona il **gruppo di accesso** - **sec-group** a cui desidera fornire l'accesso
1. Seleziona **`bob.com`**
1. Seleziona il ruolo Gestore (**Manager**)
1. Seleziona l'opzione **Performance config**
1. Fa clic su **create policy**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: performance, domainId: 4b23ec772965f672f96f05670e36827e

```

#### Accesso a tutti i domini con `security config`

Se desideri fornire le azioni di sicurezza per `bob.com` e`bob-ibm.com` dall'esempio precedente, devi creare una nuova politica ripetendo i passi per ciascun dominio. L'unica differenza è la selezione del rispettivo dominio per ciascuna politica. 

1. Fai clic sulla scheda **Account > Access** nella barra di navigazione
1. Seleziona il **gruppo di accesso** - **sec-group** a cui desideri fornire l'accesso
1. Seleziona **`bob.com`**
1. Seleziona il ruolo Gestore (**Manager**)
1. Seleziona l'opzione **Security config**
1. Fai clic su **create policy**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

1. Fai clic sulla scheda **Account > Access** nella barra di navigazione
1. Seleziona il **gruppo di accesso** - **sec-group** a cui desideri fornire l'accesso
1. Seleziona **`bob-ibm.com`**
1. Seleziona il ruolo Gestore (**Manager**)
1. Seleziona l'opzione **Security config**
1. Fai clic su **create policy**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 7ad7341865246f5df482ad9f76aafb5a
```



#### Accesso al singolo dominio con `security config` e `reliability config`

Bob ha un'istanza CIS, cis-test-instance, e 2 domini, `bob.com` e `bob-ibm.com`.
Bob desidera fornire a Tony l'accesso al ruolo Scrittore solo per le **azioni di sicurezza e affidabilità** di **`bob-ibm.com`**.

Una volta che Bob accede a cis-test-instance:
1. Fa clic sulla scheda **Account > Access** nella barra di navigazione
1. Seleziona **Tony** come colui a cui desidera fornire l'accesso
1. Seleziona **`bob-ibm.com`**
1. Seleziona il ruolo Scrittore (**Writer**)
1. Seleziona la casella di spunta per l'opzione **Security and reliability** 
1. Fa clic su **create policy**

Questa procedura crea due politiche sul backend per ogni tipo di configurazione. 

### Livello di dominio con tutti i tipi di configurazione
{:#iam-and-cis-scenarios-domain-level-all-config-types}

Bob desidera concedere a Tony l'accesso per la lettura/scrittura/gestione a livello di dominio. 

#### Scrittura
Una volta che Bob accede a cis-test-instance:
1. Fa clic sulla scheda **Account > Access** nella barra di navigazione
1. Seleziona **Tony** come colui a cui desidera fornire l'accesso
1. Seleziona **`bob.com`**
1. Seleziona il ruolo Scrittore (**Writer**)
1. Seleziona tutte le caselle per l'ambito funzionale CIS
1. Fa clic su **create policy**

```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### Gestore
Una volta che Bob accede a cis-test-instance:
1. Fa clic sulla scheda **Account > Access** nella barra di navigazione
1. Seleziona **Tony** come colui a cui desidera fornire l'accesso
1. Seleziona **`bob.com`**
1. Seleziona il ruolo Gestore (**Manager**)
1. Seleziona tutte le caselle per l'ambito funzionale CIS
1. Fa clic su **create policy**

```
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### Lettore
Una volta che Bob accede a cis-test-instance:
1. Fai clic sulla scheda **Account > Access** nella barra di navigazione
1. Seleziona **Tony** come colui a cui desidera fornire l'accesso
1. Seleziona **`bob.com`**
1. Seleziona il ruolo Lettore (**Reader**)
  1. Tutte le caselle di spunta sono preselezionate per mostrare che l'utente ha bisogno dell'accesso in lettura *minimo* all'intero dominio e non può avere un accesso parziale a un dominio
1. Fai clic su **create policy**


```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

### Livello di istanza - tutti i tuoi domini
{:#iam-and-cis-scenarios-instance-level}

Questa politica deve essere creata e gestita tramite la pagina di gestione IAM. 

L'accesso a livello di istanza significa che Bob può fornire a Tony l'autorizzazione all'istanza 1 sulle 10 istanze presenti.
Tony è in grado di visualizzare tutti i domini in questa istanza.  

Se Bob desidera concedere il ruolo di Scrittore o Gestore per accedere a quanto segue, deve fornire l'accesso a livello di istanza: 
* Programma di bilanciamento del carico - pool e controlli di integrità
* Regole di accesso Firewall
* Processi di lavoro 

Nella pagina di gestione IAM, crea una politica scrittore/gestore nell'istanza di servizio cis-test-instance.

```
Manager	Resource	Only service instance cis-test-instance of CIS 	
or
Writer	Resource	Only service instance cis-test-instance of CIS 	
```

## Politiche di gestione IAM 
{:#manage-iam-policies}

CIS consente agli utenti di creare politiche IAM, ma la gestione deve essere effettuata tramite la [pagina IAM](
https://{DomainName}/iam#/overview).

## Nota
{:#iam-note}
Per ogni politica creata nella pagina di accesso nell'istanza CIS, verranno create a turno 2-3 politiche. 

1. Il ruolo di visualizzatore per la piattaforma dell'istanza di servizio consente all'utente aggiunto di visualizzare l'istanza sul dashboard. 

**Esempio**
```
Viewer	Resource	Only service instance cis-instance-instance of CIS 	
```

2. L'accesso in lettura a livello di dominio è il requisito minimo affinché l'accesso dettagliato funzioni. 

**Esempio**
```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
```
3. La politica che hai creato con il tipo di configurazione presente. 

**Esempio**
```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

**FAQ**
1. Come ottengo il mio ID dell'istanza di servizio?

   Copia il CRN nella pagina della panoramica
   ```
   crn:v1:test:public:internet-svcs:global:a/2c38d9a9913332006a27665dab3d26e8:836f33a5-d3e1-4bc6-876a-982a8668b1bb::
   ```
   L'ultima parte del CRN è la tua istanza del servizio: `836f33a5-d3e1-4bc6-876a-982a8668b1bb`.
   
   oppure
   
   Fai clic sulla riga contenente l'istanza CIS nella pagina principale dell'elenco delle risorse e copia il GUID per l'ID dell'istanza del servizio. 

2. Ho eliminato una politica ma l'utente a cui l'ho fornita può ancora eseguire tale azione! 

   CIS memorizza nella cache i risultati di autorizzazione e il TTL per la cache è di 10 minuti.   
   
   Quando IAM lo autorizza, utilizza le politiche di accesso provenienti dal gruppo di accesso e le politiche proprie dell'utente prima di prendere una decisione. 

3. Quali autorizzazioni sono necessarie per eseguire il provisioning di Internet Services?

   Se non sei in grado di creare una risorsa e di aggiungerla a un gruppo di risorse, è probabile che tu stia riscontrando un problema di accesso. Devi disporre almeno del ruolo Visualizzatore per il gruppo di risorse stesso e del ruolo Editor per il servizio nell'account. Puoi contattare l'amministratore dell'account per verificare l'accesso che ti è stato assegnato nell'account. Per ulteriori informazioni, vedi [Gestione dell'accesso alle risorse](/docs/iam?topic=iam-iammanidaccser). 
   
 
