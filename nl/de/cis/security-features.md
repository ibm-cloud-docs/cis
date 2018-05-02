---
copyright:
  years: 2018
lastupdated: "2018-03-16"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Informationen zur Sicherheit mit IBM Cloud Internet Services (CIS)

IBM CIS ist ein global verteilter Cloud-Service, der Bedrohungen blockiert und böswillige Bots und Crawler abwehrt, die sich negativ auf Ihre Bandbreite und Serverressourcen auswirken können. IBM CIS fungiert als globaler HTTP(S)-Reverse Proxy und als verwalteter DNS-Serviceanbieter. Ihr Webdatenverkehr wird über unser intelligentes globales Netz geleitet, um Ihre Leistung und Sicherheit zu optimieren. 

![Sicherheitsgrafik.png](images/security-graphic.png)

Dies sind die wichtigsten Merkmale kurz zusammengefasst: 

## Sicherheitsmerkmale

 * Web Application Firewall (WAF)
 * Uneingeschränkte DDoS-Risikominderung

## Sicherheitsstandards und -plattform

 * TLS (SHA2 und SHA1)
 * IPv6
 * HTTP/2 und SPDY

## DNS

 * Globales Anycast-Netz
 * DNSSEC

## Netzangriffe und Risikominderung

Allgemein lassen sich Angriffe in zwei Kategorien unterteilen:

| Layer-3- oder Layer-4-Angriffe | Layer-7-Angriffe |
|------------------------------|-----------------|
|Diese Angriffe bestehen aus einer Flut von Datenverkehr an ISO Layer 3 (der Netzschicht), z. B. ICMP-Flooding, oder an Layer 4 (der Transportschicht), z. B. TCP-SYN-Flooding oder reflektiertes UDP-Flooding. |Diese Angriffe senden böswillige ISO-Layer-7-Anforderungen (Anwendungsschicht), z. B. GET-Flooding.  |
| Automatisch an unserem Edge blockiert. | Wir setzen dafür die Einstellungen 'Verteidigungsmodus', 'WAF' und 'Sicherheitsstufe' ein. |

## Zusammenfassung

 * Der Verteidigungsmodus testet Browserfunktionen, die vielen böswilligen Clients fehlen. 
 * Die WAF blockiert bekannte Anforderungsmuster, die wahrscheinlich böswillig sind, oder gibt Sicherheitsabfragen aus. 
