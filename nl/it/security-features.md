---
copyright:
  years: 2018
lastupdated: "2018-03-16"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Come IBM Cloud Internet Services (CIS) mantiene il tuo lavoro sicuro

IBM CIS è un servizio cloud distribuito globalmente che blocca le minacce e limita i crawler e i bot abusivi, che possono sprecare la tua larghezza di banda e le risorse server. IBM CIS funziona come un proxy inverso HTTP(S) globale e un provider del servizio DNS gestito. Il tuo traffico web viene instradato tramite la nostra rete globale intelligente per ottimizzare sia le prestazioni che la sicurezza.

![security-graphic.png](images/security-graphic.png)

Questa è una rapida panoramica sulla funzione:

## Funzioni di sicurezza

 * WAF (Web Application Firewall)
 * Mitigazione DDoS illimitata

## Piattaforma e standard di sicurezza

 * TLS (SHA2 e SHA1)
 * IPv6
 * HTTP/2 e SPDY

## DNS

 * Rete anycast globale 
 * DNSSEC

## Mitigazione e attacchi di rete

Generalmente, copriamo gli attacchi che rientrano in due categorie

| Attacchi di livello 3 o 4 | Attacchi di livello 7 |
|------------------------------|-----------------|
|Questi attacchi sono formati da un flusso di traffico al livello ISO 3 (il livello della rete, come i flussi ICMP) o al livello 4 (il livello del trasporto, come i flussi TCP SYN o i flussi UDP riflessi) |Questi sono attacchi che inviano richieste di livello ISO 7 dolose (il livello dell'applicazione), come i flussi GET.  |
| Bloccato automaticamente nel nostro perimetro | Li gestiamo con le impostazioni “Defense Mode,” WAF e Security level |

## Riepilogo

 * Defense Mode verifica le funzioni del browser che non hanno molti client dolosi
 * WAF blocca o affronta i modelli della richiesta conosciuti che potrebbero essere dolosi
