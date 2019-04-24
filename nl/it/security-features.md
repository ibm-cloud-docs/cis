---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIDR blocks, Whitelist Block Challenge, IBM Cloud Internet Services, security features

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Come IBM Cloud Internet Services (CIS) mantiene il tuo lavoro sicuro
{:#how-cis-keeps-your-work-secure}

IBM CIS è un servizio cloud distribuito globalmente che blocca le minacce e limita i crawler e i bot abusivi, che possono sprecare la tua larghezza di banda e le risorse server. IBM CIS funziona come un proxy inverso HTTP(S) globale e un provider del servizio DNS gestito. Il tuo traffico web viene instradato tramite la nostra rete globale intelligente per ottimizzare sia le prestazioni che la sicurezza.

![security-graphic.png](images/security-graphic.png)

Questa è una rapida panoramica sulla funzione:

## Funzioni di sicurezza
{:#cis-security-features}

 * Proteggi con proxy i [record DNS](/docs/infrastructure/cis?topic=cis-dns-concepts#proxying-dns-records) o [GLB](/docs/infrastructure/cis?topic=cis-global-load-balancer-glb-concepts) per utilizzare le funzioni di sicurezza. Ciò consente di poter monitorare il traffico che fluisce tramite i nostri server e i dati. 
### WAF (Web Application Firewall)
{:#cis-web-application-firewall}

 * WAF viene implementato tramite due serie di regole: [OWASP](/docs/infrastructure/cis?topic=cis-owasp-rule-set-for-waf) e [CIS](/docs/infrastructure/cis?topic=cis-waf-settings#cis-rule-set-for-waf).
### Mitigazione DDoS illimitata
{:#cis-unlimited-ddos-mitigation}

 * Di norma, la mitigazione DDoS è un servizio costoso il cui costo può aumentare quando si verificano attacchi. Includiamo una mitigazione DDoS illimitata con CIS senza costi aggiuntivi. 

## Piattaforma e standard di sicurezza
{:#security-standards-and-platform}

 * TLS (SHA2 e SHA1)
 * IPv6
 * HTTP/2 e SPDY

## DNS
{:#cis-dns}

 * Rete anycast globale
 * DNSSEC

## Mitigazione e attacchi di rete
{:#network-attacks-and-mitigation}

Generalmente, copriamo gli attacchi che rientrano in due categorie

| Attacchi di livello 3 o 4 | Attacchi di livello 7 |
|------------------------------|-----------------|
|Questi attacchi sono formati da un flusso di traffico al livello ISO 3 (il livello della rete, come i flussi ICMP) o al livello 4 (il livello del trasporto, come i flussi TCP SYN o i flussi UDP riflessi) |Questi sono attacchi che inviano richieste di livello ISO 7 dolose (il livello dell'applicazione), come i flussi GET.  |
| Bloccato automaticamente nel nostro perimetro | Li gestiamo con le impostazioni “Defense Mode,” WAF e Security level |

## IP Firewall
{:#cis-ip-firewall}

IBM Cloud Internet Services offre diversi strumenti per controllare il tuo traffico in modo da consentirti di proteggere i tuoi domini, i tuoi URL e le tue directory da volumi di traffico, da determinati gruppi di richiedenti e da particolari IP richiedenti. Questa sezione illustra in dettaglio gli strumenti disponibili. 

### Regole IP
{:#cis-ip-rules}

Le regole IP ti consentono di controllare l'accesso per specifici indirizzi IP, intervalli di IP, specifici paesi, specifici ASNs e determinati blocchi CIDR. Le azioni disponibili sulle richieste in entrata sono: 
  * Whitelist 
  * Block  
  * Challenge (Captcha) 
  * JavaScript Challenge (IUAM challenge)

Ad esempio, se noti che un particolare IP sta causando richieste dolose, puoi bloccare tale utente tramite l'indirizzo IP. 

### Regole di blocco User-Agent
{:#user-agent-blocking-rules}

Le regole di blocco User-Agent ti consentono di eseguire un'azione su qualsiasi stringa User-Agent selezionata. Questa funzionalità funziona come il blocco del dominio descritto in precedenza, ad eccezione del fatto che il blocco esamina la stringa User-Agent in entrata invece dell'IP. Puoi scegliere come gestire una richiesta corrispondente con lo stesso elenco di azioni che hai stabilito nelle regole IP (Block, Challenge e JS Challenge). Tieni presente che il blocco User-Agent si applica alla tua intera zona. Non puoi specificare domini secondari nello stesso modo in cui puoi farlo per i blocchi del dominio. 

Questo strumento è utile per bloccare tutte le stringhe User-Agent che ritieni sospette.  

### Blocco del dominio
{:#cis-domain-lockdown}

Il blocco del dominio ti consente di inserire nella whitelist specifici indirizzi IP e specifici intervalli IP in modo che tutti gli altri IP vengano inseriti nella blacklist. Il blocco del dominio supporta:

  * Domini secondari specifici. Ad esempio, poi consentire all'IP `1.2.3.4` di accedere al dominio `foo.example.com` e di consentire all'IP `5.6.7.8` di accedere al dominio `bar.example.com`, senza necessariamente consentire il contrario. 
  * URL specifici. Ad esempio, puoi consentire all'IP `1.2.3.4` di accedere alla directory `example.com/foo/*` e di consentire all'IP `5.6.7.8` di accedere alla directory `example.com/bar/*`, ma non necessariamente consentire il contrario.
Questa funzionalità è utile quando hai bisogno di applicare una maggiore granularità alle tue regole di accesso perché, con le regole IP, puoi applicare il blocco a tutti i domini secondari del dominio corrente oppure a tutti i domini nel tuo account e non puoi specificare URI.

### Challenge Passage
{:#cis-challenge-passage}

Ubicata nelle impostazioni di sicurezza **Advanced**, questa impostazione ti consente di controllare per quanto tempo un visitatore che ha superato una verifica o una verifica JavaScript otterrà l'accesso al tuo sito prima di essere sottoposto di nuovo a verifica. Si basa sull'IP del visitatore e quindi non si applica alle verifiche presentate dalle regole WAF in quanto si basano su un'azione eseguita dall'utente sul tuo sito. 

### Browser Integrity Check
{:#cis-browser-integrity-check}

Questa impostazione si trova nelle impostazioni di sicurezza **Advanced**. Il controllo di integrità del browser ricerca le intestazioni HTTP che vengono comunemente sfruttate dagli spammer. Nega al traffico con queste intestazioni di accedere alla tua pagina. Inoltre, blocca o verifica i visitatori che non dispongono di un agent utente o chi aggiunge un agent utente non standard (questa tattica è comunemente utilizzata dallo sfruttamento di bot, crawler e API). 
