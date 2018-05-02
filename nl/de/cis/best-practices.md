---
  
copyright:
   years: 2018
lastupdated: "2018-03-13"
 
---


# Best Practices für die CIS-Konfiguration

Da sich IBM CIS in der Peripherie Ihres Netzes befindet, müssen Sie einige Schritte ausführen, um eine reibungslose Integration in Ihre Cloud Internet Services zu garantieren. Im Folgenden gehen wir auf eine Auswahl von Best Practices für die Integration von CIS mit Ihren Ursprungsservern ein.  

Sie können diese Schritte ausführen, bevor oder nachdem Sie Ihr DNS geändert und unseren Proxy-Service aktiviert haben. Diese Empfehlungen ermöglichen eine ordnungsgemäße Verbindung von IBM CIS mit Ihren Ursprungsservern. Sie helfen Ihnen, Probleme mit dem API- oder HTTPS-Datenverkehr auszuschließen, und sorgen dafür, dass Ihre Protokolle die richtigen IP-Adressen Ihrer Kunden erfassen und nicht die dem Schutz dienenden CIS-IP-Adressen. 

Folgendes müssen Sie tun: 

 * Best Practice 1: Ursprungs-IPs Ihrer Kunden wiederherstellen
 * Best Practice 2: CIS-IP-Adressen einbauen
 * Best Practice 3: Sicherstellen, dass Ihre Sicherheitseinstellungen nicht den API-Datenverkehr beeinträchtigen
 * Best Practice 4: Ihre Sicherheitseinstellungen möglichst streng konfigurieren
 
## Best Practice 1: Ursprungs-IPs Ihrer Kunden wiederherstellen

Als Reverse Proxy stellen wir die Ursprungs-IP in diesen Headern bereit: 

  * `CF-Connecting-IP`
  * `X-Forwarded-For`
  * `True-Client-IP` (optional)

Sie können Benutzer-IP-Adressen mit einer Reihe von Tools für Infrastrukturen wie Apache, Windows IIS und NGINX wiederherstellen. 

## Best Practice 2: CIS-IP-Adressen für eine reibungslose Integration einbauen

Führen Sie diese beiden Schritte aus: 

  * Entfernen Sie ggf. die Drosselung von CIS-IP-Adressen. 
  * Richten Sie Ihre ACLs so ein, dass nur CIS-IP-Adressen und andere vertrauenswürdige Parteien zugelassen werden. 

Die aktualisierte Liste von IP-Bereichen für IBM CIS finden Sie [hier](whitelisted-ips.html). 

## Best Practice 3: Sicherheitseinstellungen überprüfen, um sicherzustellen, dass sie den API-Datenverkehr nicht beeinträchtigen

IBM CIS beschleunigt den Datenverkehr üblicherweise, indem der Zusatzaufwand für Verbindungen reduziert wird. Allerdings kann die Standardsicherheitseinstellung viele API-Aufrufe beeinträchtigen. Wir empfehlen, die folgenden Aktionen auszuführen, um eine Beeinträchtigung Ihres API-Datenverkehrs zu vermeiden, sobald die Weiterleitung über Proxys aktiv ist.

 * Inaktivieren Sie bestimmte Sicherheitsfunktionen mithilfe von **Seitenregeln**. 
   * Erstellen Sie eine Seitenregel mit dem URL-Muster Ihrer API, z. B. `api.beispiel.com`. 
   * Fügen Sie die folgenden Regelverhalten hinzu: 
      * Legen Sie **Sicherheitsstufe** auf **Praktisch aus** fest. 
      * Legen Sie **TLS** auf **Aus** fest. 
      * Legen Sie **Browserintegritätsprüfung** auf **Aus** fest. 
   * Wählen Sie **Ressource bereitstellen** aus. 

 * Alternativ können Sie die **Web Application Firewall** global auf der Seite 'Sicherheit' inaktivieren.

| *Was macht die Einstellung 'Browserintegritätsprüfung'?* | 
|------------------------------------------------|
| *Die Integritätsprüfung des Browsers sucht nach HTTP-Headern, die oft von Spammern verwendet werden. Sie verweigert Datenverkehr mit diesen Headern den Zugriff auf Ihre Seite. Sie blockiert außerdem Besucher, die keinen Benutzeragenten haben oder einen vom Standard abweichenden Benutzeragenten hinzufügen (diese Taktik wird oft von böswilligen Bots, Crawlern oder APIs eingesetzt).* |

## Best Practice 4: Ihre Sicherheitseinstellungen möglichst streng konfigurieren

CIS stellt eine Reihe von Optionen zum Verschlüsseln Ihres Datenverkehrs bereit. Als Reverse Proxy schließen wir TLS-Verbindungen in unseren Rechenzentren und öffnen eine neue TLS-Verbindung mit Ihren Ursprungsservern. Sie können ein benutzerdefiniertes Zertifikat aus Ihrem Konto hochladen bzw. ein von CIS bereitgestelltes Platzhalterzertifikat verwenden. 

### Benutzerdefiniertes Zertifikat hochladen
 
Sie können Ihren öffentlichen und privaten Schlüssel hochladen, wenn Sie eine Unternehmensdomäne erstellen. Wenn Sie Ihr eigenes Zertifikat hochladen, erzielen Sie sofortige Kompatibilität mit verschlüsseltem Datenverkehr und behalten die Kontrolle über Ihr Zertifikat (z. B. ein EV-Zertifikat). Denken Sie daran, dass Sie für die Verwaltung eines benutzerdefinierten Zertifikats selbst verantwortlich sind. Beispielsweise überwacht IBM CIS nicht das Verfallsdatum des Zertifikats.  
 
### Alternativ ein von CIS bereitgestelltes Zertifikat verwenden
 
IBM CIS zählt diverse Zertifizierungsstellen (Certificate Authorities, CAs) zu seinen Partnern, um unseren Kunden standardmäßig Platzhalterzertifikate für Domänen bereitstellen zu können. Für die Konfiguration dieser Zertifikate kann eine manuelle Überprüfung erforderlich sein und Ihr Support-Team unterstützt Sie bei diesen zusätzlichen Schritten. 
 
### TLS-Einstellung in **End-to-End-CA-signiert** ändern
 
Ein Großteil unserer Unternehmenskunden verwenden die Sicherheitseinstellung 'End-to-End-CA-signiert'. Für diese Einstellung muss ein gültiges, CA-signiertes Zertifikat auf Ihrem Web-Server installiert sein. Das Verfallsdatum des Zertifikats muss in der Zukunft liegen und es muss einen übereinstimmenden *Hostnamen* oder *SAN* (Subject Alternative Name, alternativer Name für Subjekt) aufweisen. 

