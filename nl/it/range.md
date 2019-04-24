---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: range application, tls encryption, ddos protection, global tcp proxy

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Range
{:#cis-range}

La funzione Range offre la protezione DDoS, il bilanciamento del carico e l'accelerazione del contenuto in qualsiasi protocollo basato su TCP.
Range è un proxy TCP globale in esecuzione sui nodi edge di CIS/Cloudflare. 

Range può essere utilizzato per: 
* Proteggere le tue porte e i tuoi protocolli TCP da attacchi **DDoS di livello 2 e 4**. 
* Ridurre la capacità degli aggressori di eseguire lo snooping e il furto di dati sensibili abilitando la **codifica TLS**.
* Integrarsi con CIS IP Firewall che ti consente di bloccare o verificare indirizzi IP o interi intervalli di IP, non consentendo loro di raggiungere i servizi TCP.  
* Configurare i programmi di bilanciamento del carico con controlli di integrità TCP, failover e politiche di indirizzamento che indicano dove deve fluire il traffico. 

## Introduzione a Range
{:#getting-started-with-range}

Range è disponibile solo per i clienti Enterprise con un costo aggiuntivo e il prezzo viene stabilito in base all'utilizzo della larghezza di banda.
{:note}

### Aggiungi un'applicazione
{:#range-add-an-application}
Segui questi passi per aggiungere un'applicazione. 

1. Passa a **Security > Range**
1. Fai clic sul pulsante **Add application** 
1. Immetti il nome dell'applicazione nel primo campo di input. La tua applicazione viene associata a un nome DNS nel tuo dominio CIS.
1. Immetti la porta edge nel campo di input successivo. Ascolteremo su questa porta le connessioni in entrata a questi indirizzi. Le connessioni a questi indirizzi sono protette da proxy nella tua origine. (La protezione con proxy è supportata su tutte le porte ad eccezione della porta 21.)
1. Nella sezione Origin, immetti l'IP di origine e la porta della tua applicazione TCP. Puoi anche selezionare un programma di bilanciamento del carico esistente. 
1. Abilita IP Firewall. Quando abilitato, le regole del firewall con un'azione "block" o "whitelist" vengono applicate per questa applicazione. Le regole basate sul paese o su ASN non sono ancora supportate. 
1. Abilita Proxy Protocol se hai un proxy incorporato che supporta PROXY Protocol v1. Questa funzione è utile se stai eseguendo un servizio che deve conoscere l'IP client effettivo. Nella maggior parte dei casi, questa impostazione deve rimanere disabilitata. 
1. Fai clic su **Provision**

Proxy Protocol antepone a ogni connessione un'intestazione che riporta l'indirizzo IP del client e la porta. Un'intestazione Proxy Protocol ha questo formato: 
  * PROXY_STRING + spazio singolo + INET_PROTOCOL + spazio singolo + CLIENT_IP + spazio singolo + PROXY_IP + spazio singolo + CLIENT_PORT + spazio singolo + PROXY_PORT + "\r\n"
  * Di seguito viene riportata una riga Proxy Protocol di esempio per un indirizzo IPv4:
    `PROXY TCP4 192.0.2.0 192.0.2.255 42300 443\r\n`
  * Di seguito viene riportata una riga Proxy Protocol di esempio per un indirizzo IPv6:
    `PROXY TCP6 2001:db8:: 2001:db8:ffff:ffff:ffff:ffff:ffff:ffff 42300 443\r\n`
   
Il provisioning di un'applicazione Range comporterà costi aggiuntivi, basati sulla quantità di larghezza di banda utilizzata per applicazione.
{:note}

Ora la tua applicazione è visibile in un tile con le seguenti proprietà:
  * Nome applicazione
  * Porta edge
  * Origine e porta
  * Connessioni nell'ultima ora (polling eseguito ogni minuto)
  * Velocità effettiva nell'ultima ora (polling eseguito ogni minuto)
  * Il menu Overflow (in alto a destra) consente di 
    * Modificare l'applicazione
    * Visualizzare le metriche per l'applicazione specificata
    * Eliminare l'applicazione 
    
Quando viene creata un'applicazione Range, le viene assegnato un indirizzo IPv4 e IPv6 univoco. Questi indirizzi IP non sono statici e possono essere soggetti a modifica. Puoi determinare l'indirizzo IP assegnato utilizzando DNS. Il nome DNS restituirà sempre l'indirizzo IP assegnato all'applicazione.      
    
### Visualizza le metriche
{:#range-view-metrics}
Ora la tua applicazione è pronta per trasmettere il traffico TCP tramite proxy attraverso Cloudflare/CIS.

Passa a **Metrics > Range** per visualizzare il tuo numero di connessioni alle applicazioni e la velocità effettiva del traffico.
I grafici mostrano le metriche per massimo 10 applicazioni.
{:note}

Le metriche dell'applicazione possono essere attivate tramite la chiave del grafico oppure facendo clic sul pulsante **Select applications**. L'intervallo di data/ora delle metriche può essere modificato utilizzando il menu a discesa. 

## Tile dell'applicazione di Range
{:#range-apptiles}
Una volta create alcune applicazioni, la pagina **Security > Range** verrà popolata con i tile delle applicazioni. I tile dell'applicazione contengono le seguenti informazioni: 
* Nome applicazione
* Porta edge
* Origine e porta
* Connessioni nell'ultima ora (polling eseguito ogni minuto)
* Velocità effettiva nell'ultima ora (polling eseguito ogni minuto)


Il tile dell'applicazione contiene anche un menu di overflow nell'angolo superiore (3 puntini). Il menu di overflow fornisce agli utenti l'opzione per: 
* modificare l'applicazione
* visualizzare le metriche per l'applicazione specificata
  * ciò porta l'utente alla pagina **Metrics > Range**, che mostra le metriche relative solo a tale applicazione
* eliminare l'applicazione


## Esempi di utilizzo di API
{:#range-api-usage-examples}
Quelli che seguono sono esempi per creare ed elencare le applicazioni utilizzando Range.

### Crea l'applicazione tramite Range
{:#create-range-app}
Esistono due modi in cui puoi designare un'origine in un'applicazione in un'applicazione Range
1. IP origine - utilizzando il parametro `origin_direct`
2. Programma di bilanciamento del carico - utilizzando i parametri `origin_dns` e `origin_port`

**Richiesta:**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_direct":["tcp://172.0.2.1:22"],"proxy_protocol":true,"ip_firewall":true}'

```
**Risposta:**
```
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_direct": [
            "tcp://172.0.2.1:22"
        ],
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:33:09.190606Z",
        "modified_on": "2019-01-09T17:33:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```

**Richiesta:**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_dns": {"name": "test"},"proxy_protocol":true,"ip_firewall":true, "origin_port": 43}'

```
**Risposta:**
```
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_dns": {
          "name": "test"
        },
        "origin_port": 43,
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:39:09.190606Z",
        "modified_on": "2019-01-09T17:39:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```

**DNS Name:** la tua applicazione viene associata a un nome DNS nel tuo dominio. 

**Protocol/Edge port:** si tratta della porta su cui è in esecuzione la tua applicazione. Le connessioni a questi indirizzi sono protette da proxy nella tua origine. 

**Origin direct:** si tratta dell'IP su cui è in esecuzione la tua applicazione e la porta tramite cui desideri fluisca il traffico dall'edge alla tua origine. 

**IP Firewall:** se abilitato, le regole del firewall con un'azione Block vengono applicate a questa applicazione Range. 

**PROXY Protocol:** abilitalo se hai un proxy incorporato che supporta PROXY Protocol v1. Nella maggior parte dei casi, questa impostazione rimane disabilitata. 

**Origin DNS:** si tratta del nome del programma di bilanciamento del carico che desideri impostare come tua origine. 

**Origin Port:** si tratta della porta del tuo servizio.  

### Elenca tutte le applicazioni
{:#range-list-all-apps}

**Richiesta:**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps
```

**Risposta:**
```
{
    "result": [
        {
            "id": "4f70c3d4f20546b79135b898295e8093",
            "protocol": "tcp/22",
            "dns": {
                "type": "CNAME",
                "name": "ssh.example.com"
            },
            "origin_direct": [
                "tcp://172.0.2.1:22"
            ],
            "ip_firewall": true,
            "proxy_protocol": true,
            "created_on": "2019-01-09T17:33:09.190606Z",
            "modified_on": "2019-01-09T17:33:09.190606Z"
        }
    ],
    "success": true,
    "errors": [],
    "messages": []
}
```

### Elenca un'applicazione Range specifica
{:#range-list-a-specific-range-app}
**Richiesta:**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps/4f70c3d4f20546b79135b898295e8093
```

**Risposta:**
Applicazione che utilizza l'IP origine
```
{
    "result": {
        "id": "4f70c3d4f20546b79135b898295e8093",
            "protocol": "tcp/22",
            "dns": {
                "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_direct": [
            "tcp://172.0.2.1:22"
        ],
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:33:09.190606Z",
        "modified_on": "2019-01-09T17:33:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
} 
```

Applicazione che utilizza il programma di bilanciamento del carico
```
{
    "result": {
        "id": "555359036e7f4acc82d69b916f62caba",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_dns": {
          "name": "test_update"
        },
        "origin_port": 76,
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-10T22:26:47.167008Z",
        "modified_on": "2019-01-10T22:26:47.167008Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}

```
