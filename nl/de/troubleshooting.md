---
copyright:
  years: 2018
lastupdated: "2018-03-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Fehlerbehebung Ihrer CIS-Netzverbindung

## Woher weiß ich, dass meine Daten über meine IBM CIS-Verbindung übergeben werden?

IBM Cloud Internet Services (CIS) verwendet HTTP-Header, die gelesen, hinzugefügt oder geändert werden können. Anhand des Headers und einer CF-Ray-Zahl können wir die Route einer Anforderung nachvollziehen. Die CF-Ray-Zahl kann mit einem `curl`-Befehl oder mit einem Google Chrome-Plug-in namens 'Claire' abgerufen werden. 

Um festzustellen, ob Daten über IBM CIS übergeben wurden, machen Sie die `Ray ID` ausfindig, die für jedes Paket angegeben wird. 

**Unix-Befehlszeilentools:**

 * curl für HTTP:
`$ curl -vso /dev/null http://beispiel.com`

 * dig für DNS:
`$ dig www.beispiel.com`

 * traceroute für das Netz:
`$ traceroute beispiel.com`

**Beispiel: **

Terminalbefehl:  `curl -svo /dev/null IHRE_URL_HIER. -L`

Ergebnis: `CF-RAY: 1ca349b6c1300da3-SJC`

## Wie kann ich eine Route nachvollziehen? 

Um nachzuvollziehen, ob eine Route entlang Ihrem IBM CIS-Pfad verläuft, können Sie einen 'dig'-Befehl in einem Terminalfenster für Mac oder Linux ausführen
oder `nslookup` in der Windows-Eingabeaufforderung absetzen. 

Falls das Paket einen CF-Ray-Wert hat, hat es CIS passiert. 

Der Befehl `traceroute` zeigt den gesamten Pfad an, den eine IP-Anforderung genommen hat. 

Das Support-Team nutzt diese Befehle, um Ihnen Hilfestellung zu geben. 

## Wenn eine Datenschutzwarnung angezeigt wird: 

Die Zertifikate, die von IBM CIS ausgestellt werden, decken die Rootdomäne (`beispiel.com`) und eine Unterdomäne (`*.beispiel.com`) ab. Wenn Sie versuchen, eine Unterdomäne der zweiten Ebene (`*.*.beispiel.com`) zu erreichen, wird in Ihrem Browser eine Warnung zum Datenschutz angezeigt, da diese Hostnamen nicht zum SAN hinzugefügt werden. 

Es kann bis zu 15 Minuten dauern, bis eine unserer Partnerzertifizierungsstellen ein neues Zertifikat ausstellt. Solange Ihr neues Zertifikat noch nicht ausgestellt wurde, wird in Ihrem Browser eine Warnung zum Datenschutz angezeigt. 

## Was kann ich tun, wenn ich Ziel eines DDoS-Angriffs bin?

 * **Schritt 1:** Schalten Sie in Ihrem Dashboard den 'Verteidigungsmodus' ein. 
 * **Schritt 2:** Legen Sie für Ihre DNS-Datensätze maximale Sicherheit fest. 
 * **Schritt 3:** Drosseln Sie Anforderungen von IBM CIS nicht. 
 
Im Verteidigungsmodus wird jedem neuen Besucher eine Captcha-Sicherheitsabfrage angezeigt, die sie bestehen müssen, bevor ein Cookie für den ungehinderten Zugriff ausgestellt wird. Auf diese Weise wird Botnet-Datenverkehr blockiert, bis der 'Verteidigungsmodus' ausgeschaltet wird. Besucher, die die Sicherheitsabfrage nicht bestehen, werden zur IP-Reputationsdatenbank hinzugefügt. 

## Mögliche andere Probleme: 

Im Folgenden finden Sie einige gängige Fehlernachrichten, die Ihnen oder Ihrem Support-Team angezeigt werden können: 

| Fehlercode    | Grund |
| ------------- | ------------- |
| 1001  | DNS-Auflösungsfehler. Entweder hat sich der Kunde erst kürzlich angemeldet und seine DNS-Informationen wurden noch nicht weitergegeben, oder bei der DNS-Verwaltung ist ein Fehler aufgetreten. |
| 521  | Ursprungs-Web-Server hat die Verbindung vom CIS abgelehnt. Entweder ist der Ursprungs-Web-Server nicht aktiv oder die IBM CIS-IP-Adressen werden blockiert. |
| 522  | Überschreitung des Verbindungszeitlimits zum Ursprungsserver (Standardwert ist 30 Sekunden). Entweder wurde die Übertragungsrate von CIS eingeschränkt oder der Web-Server verbraucht alle Ressourcen (gemeinsam genutzter Server) oder es gibt Netzkonnektivitätsprobleme zwischen dem Web-Server und IBM CIS. |
| 523  | Ursprungsserver ist nicht erreichbar. Stellen Sie sicher, dass die Ursprungs-IP-Adresse für den DNS-Datensatz dieselbe ist wie diejenige, die auf der Seite mit den CIS-DNS-Einstellungen angezeigt wird. |
| 524  | IBM CIS konnte eine TCP-Verbindung herstellen, hat aber keine Antwort vom Web-Server empfangen. Eine Anwendung mit langer Laufzeit oder eine Datenbankabfrage funkt dazwischen. |

### Kein Netzverkehr

Wenn nicht erkennbar ist, dass Daten ausgetauscht werden, und Sie einen CNAME verwenden, stellen Sie sicher, dass eine Weiterleitung eingerichtet ist, damit der Datenverkehr nicht an die Rootdomäne geleitet wird. Denken Sie daran, dass manche DNS-Weitergaben bis zu 48 Stunden dauern können. 

### Website offline

Folgendes wird möglicherweise angezeigt: 

`IBM CIS cannot connect to the origin server (Fehler 521, 522, 523)`.

**Website offline - keine zwischengespeicherte Version**

1. Der Server ist online, aber er blockiert die IBM CIS-Anforderung.
2. Der Ursprungsserver ist offline, und IBM CIS hat kein Backup-Website-Image.  

Sie können Folgendes tun: 

* Überprüfen Sie, dass die IBM CIS-IP-Adressen in der Whitelist aufgeführt sind. 
* Stellen Sie sicher, dass IBM CIS-IPs nicht gedrosselt werden. 
* Dies ist die Liste der [IPs, die in der Whitelist aufgeführt werden müssen](whitelisted-ips.html). 

### 502-Fehler

Dies ist einer der gängigsten Fehler. Er tritt in der Regel auf, wenn ein Teil eines Netzes nicht verfügbar ist, z. B. zu Beginn eines DDoS-Angriffs. Ein bestimmtes Rechenzentrum kann für einen gewissen Zeitraum nicht verfügbar sein. Der Datenverkehr wird umgeleitet. Setzen Sie einen 'traceroute'-Befehl ab.  

Folgendes wird möglicherweise angezeigt: `Error 502 - bad gateway error`

Das ist passiert: 

* Ein Teil des IBM CIS-Netzes hat ein Problem.
* In der Regel ist das Problem auf einen Server in einem Rechenzentrum beschränkt.
* Es betrifft nur einen Teil der Besucher der Website.
* Das IBM CIS Technical Operations-Team kümmert sich darum.

Das können Sie tun: 

* Senden Sie die Ergebnisse von `www.IHRE_DOMÄNE.com/cdn-cgi/trace` in einem Ticket an den [Support](https://console.bluemix.net/docs/support/index.html#contacting-support).
* Schalten Sie Ihre DNS-Datensätze temporär aus (kein Proxy). 

