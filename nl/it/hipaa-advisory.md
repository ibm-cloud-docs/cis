---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Advisory, Use of Caching, content caching, Cache-Control header

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Informativa HIPAA
{:#hipaa-advisory}

L'utilizzo della memorizzazione nella cache (CDN) per i dati regolamentati (ad esempio, PHI, ITAR) è **proibito**. Tutti i flussi dei dati regolamentati che utilizzano CIS devono essere impostati su **not cache**.
{:important}

Esistono diversi modi per disabilitare la memorizzazione nella cache del contenuto per CDN CIS. 
- Il server di origine può impostare **no-cache** nell'intestazione **Cache-Control** per il contenuto regolamentato. 
- Utilizza le regole della pagina CIS per disabilitare la memorizzazione nella cache del contenuto in un percorso specificato, anche se l'origine non invia un'intestazione **Cache-Control** **no-cache**. 
