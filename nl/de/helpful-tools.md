---
copyright:
  years: 2018
lastupdated: "2018-03-01"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Hilfreiche Tools zur Verwaltung Ihrer CIS-Bereitstellung

Es gibt eine Reihe von Unix-Systemverwaltungstools für öffentliche Domänen, die Sie bei der Verwaltung Ihrer IBM CIS-Bereitstellung unterstützen können. 

## Sysadmin-Tools

 * whois (Tool zur Identifizierung von Domänen)
 * dig (DNS-Tool)
 * curl (HTTP- und HTTPS-Tool)
 * netcat (IP- und Porttool)
 * traceroute (Netztool)

## Kommerzielle Tools für externe und ferne Tests:

 * GTMetrix (http)
 * Webseitentest (http)
 * WhatsMyDNS (DNS-Tool)
 * G Suite Toolbox (DNS und HTTP)

## Tools zum Untersuchen von Protokollen und Verlauf

 * HTTP Archive-Dateien (HAR-Dateien)


### `whois`

`whois` ist ein Befehlszeilentool des UNIX-Systems, mit dem Sie nach Registratorinformationen für einen gegebenen Domänennamen oder eine gegebene IP-Adresse suchen können, z. B. nach den gegebenen autoritativen Servern einer Domäne oder dem Eigner einer bestimmten IP-Adresse. 

Beispiele:

`whois beispiel.com`

`whois 8.8.8.8`

### `dig`

`dig` ist ein UNIX-Befehlszeilentool, das DNS-Abfragen durchführen und DNS-Datensätze für eine bestimmte Domäne prüfen kann. Es ähnelt `nslookup`. 

Das Schema dieses Befehls lautet: dig <datensatztyp> <domänenname> <optionen>

**Beispiele:**

`dig beispiel.com`

`dig mein.beispiel.com`

`dig beispiel.com +trace`

`dig NS beispiel.com`

`dig beispiel.com @ns.beispiel.com`

### `cURL`

`cURL` ist ein UNIX-Befehlszeilentool, mit dem Sie Daten unter Verwendung der URL-Syntax übertragen können. Es wird häufig verwendet, um HTTP-Anforderungen zu stellen oder Serverantworten zu vergleichen. 

Das Schema für diesen Befehl lautet: curl -option1 -option2 http://beispiel.com/url

**Beispiele:**

`curl -svo /dev/null http://www.beispiel.com`

`curl -svo /dev/null -A “USER_AGENT_STRING” http://www.beispiel.com`

`curl -svo /dev/null -H “host: www.beispiel.com” http://ORIGIN_IP`

`curl -svo /dev/null -H https://www.beispiel.com --resolve www.beispiel.com:443:ORIGIN_IP`

### `mtr` und `traceroute`

MTR und `traceroute` sind UNIX-Befehlszeilentools, mit denen Sie die Leistung oder Latenz entlang eines spezifischen Netzpfads bis zu einem angegebenen Host oder Zielserver messen können. 

**Beispiele:**

`mtr -rwc 20 beispiel.com -T -4`
`mtr -rwc 20 8.8.8.8 -T -6`

`traceroute beispiel.com -T -4`

`traceroute 8.8.8.8 -T -6`

| Option | Definition |
|---------|-----------|
| -c | Legt die Anzahl der gesendeten Pingsignale fest. |
| -T | Erzwingt eine TCP-Traceroute (normalerweise ICMP). |
| -4 | Erzwingt die Verwendung von IPv4. |
| -6 | Erzwingt die Verwendung von IPv6. |

### HAR-Datei generieren

Eine HAR-Datei ist eine Aufzeichnung von HTTP-Anforderungen von einem Web-Browser. Browser wie Chrome verfügen über einen Entwicklertools-Abschnitt, in dem Sie Informationen zum Erstellen einer HAR-Datei finden können. 
