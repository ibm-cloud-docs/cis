---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Verwalten von IBM CIS zum Zweck einer optimalen Sicherheit

Die Sicherheitseinstellungen von IBM Cloud Internet Services (CIS) umfassen sichere Standardwerte, die darauf ausgelegt sind, Fehlalarme und negative Auswirkungen auf Ihren Datenverkehr zu verhindern. Diese sicheren Standardeinstellungen sind jedoch nicht unbedingt die beste Option für alle Kunden. Führen Sie die folgenden Schritte aus, um sicherzustellen, dass die Konfiguration Ihres CIS-Kontos ausreichende Sicherheit bietet: 

**Empfehlungen und Best Practices:**

* Sichere Ursprungs-IP-Adressen durch Proxys und zusätzliche Verschleierung
* Selektive Konfiguration Ihrer Sicherheitsstufen
* Sichere Aktivierung Ihrer Web Application Firewall (WAF)

## Best Practice 1: Ursprungs-IP-Adressen sichern

Wenn eine Unterdomäne mit IBM CIS weitergeleitet wird, ist der gesamte Datenverkehr geschützt, weil wir aktiv mit für IBM CIS spezifischen IP-Adressen antworten (z. B. stellen alle Ihre Clients zunächst eine Verbindung mit CIS-Proxys her und Ihre Ursprungs-IP-Adressen werden unkenntlich gemacht). 

### IBM CIS-Proxys für alle DNS-Datensätze für HTTP(S)-Datenverkehr von Ihrem Ursprung verwenden

Um die Sicherheit Ihrer Ursprungs-IP-Adressen zu verbessern, sollte der gesamte HTTP(S)-Datenverkehr über einen Proxy geleitet werden. 

**Sehen Sie sich den Unterschied selbst an - fragen Sie einen Nicht-Proxy- und einen Proxy-Datensatz ab:**

```
$ dig greycloud.theburritobot.com +short
1.2.3.4 (Ursprungs-IP-Adresse)

$ dig orangecloud.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (CIS-IP-Adresse)
```

### Nicht-Proxy-Ursprungsdatensätze mit vom Standard abweichenden Namen unkenntlich machen
Alle Datensätze, die nicht über IBM CIS als Proxy geleitet werden können und die noch Ihre Ursprungs-IP verwenden, z. B. FTP, können mithilfe einer zusätzlichen Verschleierung gesichert werden. Verwenden Sie insbesondere, wenn Sie Datensätze für Ihren Ursprung benötigen, die nicht über IBM CIS als Proxy geleitet werden kann, vom Standard abweichende Namen. Verwenden Sie beispielsweise `[beliebiges Wort oder beliebiges Zeichen].beispiel.com` anstelle von `ftp.beispiel.com`. Diese Verschleierung macht es weniger wahrscheinlich, dass bei Wörterverzeichnissuchen in Ihren DNS-Datensätzen Ihre Ursprungs-IP-Adresse offenbart wird. 

### Ggf. separate IP-Bereiche für HTTP- und Nicht-HTTP-Datenverkehr verwenden
Manche Kunden verwenden separate IP-Bereiche für HTTP- und Nicht-HTTP-Datenverkehr. Auf diese Weise können alle Datensätze, die auf ihren HTTP-IP-Bereich verweisen, über einen Proxy geleitet werden, und der gesamte Nicht-HTTP-Datenverkehr mithilfe eines anderen IP-Teilnetzes unkenntlich gemacht werden. 

## Best Practice 2: Sicherheitsstufe selektiv konfigurieren
Ihre **Sicherheitsstufe** legt die Sensitivität unserer **IP-Reputationsdatenbank** fest. IBM CIS lernt über 1 Milliarde eindeutige IP-Adressen pro Monat, von mehr als 7 Millionen Websites. Auf diese Weise kann unser System böswillige Akteure ermitteln und verhindern, dass diese auf Ihre Web-Assets zugreifen. Um negative Interaktionen oder Fehlalarme zu verhindern, konfigurieren Sie Ihre **Sicherheitsstufe** domänenweise, d. h. erhöhen oder verringern Sie die Sicherheit nach Bedarf. 

### Sicherheitsstufe für sensible Bereiche auf 'Hoch' setzen
Sie können diese Einstellung verschärfen, indem Sie eine **Seitenregel** für Verwaltungsseiten oder Anmeldeseiten hinzufügen, um Brute-Force-Angriffe zu reduzieren: 

1. Erstellen Sie eine **Seitenregel** mit dem URL-Muster Ihrer API (z. B. `www.beispiel.com/wp-login`).  
2. Legen Sie die Einstellung für die **Sicherheitsstufe** fest. 
3. Markieren Sie die Einstellung als **Hoch**. 
4. Wählen Sie **Ressource bereitstellen** aus. 

### Niedrigere Sicherheitsstufe für nicht sensible Pfade oder APIs festlegen, um Fehlalarme zu reduzieren
Diese Einstellung kann für allgemeine Seiten und allgemeinen API-Datenverkehr niedriger gewählt werden.  

1. Erstellen Sie eine **Seitenregel** mit dem URL-Muster Ihrer API (z. B. `www.beispiel.com/api/*`). 
2. Legen Sie die Einstellung für die **Sicherheitsstufe** fest. 
3. Wählen Sie die Sicherheitsstufe **Niedrig** oder **Praktisch aus** aus. 
4. Wählen Sie **Ressource bereitstellen** aus. 

### Welche Bedeutung haben die Einstellungen für die Sicherheitsstufe? 
Unsere Einstellungen für die Sicherheitsstufe sind an Bedrohungsbewertungen angelehnt, die bestimmten IP-Adressen aufgrund böswilligen Verhaltens in unserem Netz zugeordnet sind. Eine Bedrohungsbewertung über 10 wird als hoch gewertet. 

* **HOCH**: Bei Bedrohungsbewertungen über 0 wird eine Sicherheitsabfrage angezeigt. 
* **MITTEL**: Bei Bedrohungsbewertungen über 14 wird eine Sicherheitsabfrage angezeigt. 
* **NIEDRIG**: Bei Bedrohungsbewertungen über 24 wird eine Sicherheitsabfrage angezeigt. 
* **PRAKTISCH AUS**: Bei Bedrohungsbewertungen über 49 wird eine Sicherheitsabfrage angezeigt. 

Wir empfehlen, Ihre Einstellungen für die Sicherheitsstufe in regelmäßigen Abständen zu überprüfen. Entsprechende Anweisungen finden Sie im Dokument [Best Practices für die CIS-Konfiguration](best-practices.html). 

## Best Practice 3: Web Application Firewall (WAF) sicher aktivieren
Ihre WAF ist im Abschnitt **Sicherheit** verfügbar. Wir gehen diese Einstellungen in umgekehrter Reihenfolge mit Ihnen durch, um sicherzustellen, dass Ihre WAF möglichst sicher konfiguriert ist, bevor Sie sie für die gesamte Domäne aktivieren. Diese anfänglichen Einstellungen können Fehlalarme reduzieren, indem die für den Datenverkehr zuständige Anwendung mit WAF-Ereignissen für die weitere Optimierung befüllt wird. Ihre WAF wird automatisch aktualisiert, um neue Sicherheitslücken zu beheben, sobald sie erkannt werden. 

Die WAF schützt vor den folgenden Typen von Angriffen: 
* SQL-Injection-Attacke
* Cross-Site Scripting
* Cross-Site Forgery

Die WAF enthält einen Standardregelsatz, der Regeln zum Stoppen der gängigsten Angriffe enthält. Sie können die WAF jetzt entweder aktivieren oder inaktivieren. Im Dokument [WAF-Standardregelsatz](waf-rule-set.html) finden Sie weitere Details zum Standardregelsatz und zum Verhalten der einzelnen Regeln. 

Weitere Informationen zur WAF finden Sie im Dokument [WAF-Konzepte](waf-concept.html). 

## Best Practice 4: TLS-Einstellungen konfigurieren
IBM CIS stellt eine Reihe von Optionen zum Verschlüsseln Ihres Datenverkehrs bereit. Als Reverse Proxy schließen wir TLS-Verbindungen in unseren Rechenzentren und öffnen eine neue TLS-Verbindung mit Ihrem Ursprungsserver. 

TLS bietet vier Betriebsarten: 
* **Aus**: In diesem Modus ist TLS inaktiviert; diese Einstellung wird nicht empfohlen. 
* **Client-zu-Edge**: TLS verschlüsselt Datenverkehr von CIS an Ihre Clients, aber nicht von CIS an Ihre(n) Ursprungsserver. 
* **End-to-End-flexibel**: TLS verschlüsselt den gesamten Datenverkehr. Sie können jedoch ein selbst signiertes Zertifikat verwenden, um den Datenverkehr zwischen CIS und Ihren Ursprungsservern zu sichern. 
* **End-to-End-CA-signiert**: TLS verschlüsselt den gesamten Datenverkehr. Sie müssen ein CA-signiertes Zertifikat verwenden .

Weitere Informationen zu den TLS-Optionen finden Sie in [diesem Dokument](ssl-options.html). 

IBM CIS lässt die Verwendung von benutzerdefinierten Zertifikaten zu. Oder Sie können ein Platzhalterzertifikat verwenden, das Ihnen von CIS bereitgestellt wird. 

### Benutzerdefiniertes Zertifikat hochladen
Sie können Ihr benutzerdefiniertes Zertifikat hochladen, indem Sie auf die Schaltfläche **Zertifikat hinzufügen** klicken und das Zertifikat, den privaten Schlüssel und die Bündelmethode angeben. Wenn Sie Ihr eigenes Zertifikat hochladen, erzielen Sie sofortige Kompatibilität mit verschlüsseltem Datenverkehr und behalten die Kontrolle über Ihr Zertifikat (z. B. ein EV-Zertifikat). Denken Sie daran, dass Sie für die Verwaltung eines benutzerdefinierten Zertifikats selbst verantwortlich sind. Beispielsweise überwacht IBM CIS nicht das Verfallsdatum des Zertifikats.  

![Benutzerdefiniertes Zertifikat](images/upload-custom-certificate.png)

### Bereitgestelltes Zertifikat verwenden
IBM zählt diverse Zertifizierungsstellen (Certificate Authorities, CAs) zu seinen Partnern, um unseren Kunden Platzhalterzertifikate für Domänen bereitstellen zu können. Für die Konfiguration dieser Zertifikate kann eine manuelle Überprüfung erforderlich sein. Ihr Support-Team unterstützt Sie bei diesen zusätzlichen Schritten. 
