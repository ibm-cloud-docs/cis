---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-26"

keywords: IBM CIS, optimal security, Security Level

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Verwalten von IBM CIS zum Zweck einer optimalen Sicherheit
{:#manage-your-ibm-cis-for-optimal-security}
Die Sicherheitseinstellungen von IBM Cloud Internet Services (CIS) umfassen sichere Standardwerte, die darauf ausgelegt sind, Fehlalarme und negative Auswirkungen auf Ihren Datenverkehr zu verhindern. Diese sicheren Standardeinstellungen sind jedoch nicht unbedingt die beste Option für alle Kunden. Führen Sie die folgenden Schritte aus, um sicherzustellen, dass die Konfiguration Ihres CIS-Kontos ausreichende Sicherheit bietet. 

**Empfehlungen und Best Practices:**

* Sichere Ursprungs-IP-Adressen durch Proxys und zusätzliche Verschleierung
* Selektive Konfiguration Ihrer Sicherheitsstufen
* Sichere Aktivierung Ihrer Web Application Firewall (WAF)

## Best Practice 1: Ursprungs-IP-Adressen sichern
{:#best-practice-secure-origin-ip-address}

Wenn eine Unterdomäne mit IBM CIS weitergeleitet wird, ist der gesamte Datenverkehr geschützt, weil wir aktiv mit für IBM CIS spezifischen IP-Adressen antworten (z. B. stellen alle Ihre Kunden zunächst eine Verbindung mit CIS-Proxys her und Ihre Ursprungs-IP-Adressen werden unkenntlich gemacht).

### IBM CIS-Proxys für alle DNS-Datensätze für HTTP(S)-Datenverkehr von Ihrem Ursprung verwenden
{:#use-cis-proxies-for-dns-records}

Um die Sicherheit Ihrer Ursprungs-IP-Adressen zu verbessern, sollte der gesamte HTTP(S)-Datenverkehr über einen Proxy geleitet werden.

**Sehen Sie sich den Unterschied selbst an - fragen Sie einen Nicht-Proxy- und einen Proxy-Datensatz ab:**

```
$ dig nonproxied.theburritobot.com +short
1.2.3.4 (The origin IP address)

$ dig proxied.theburritobot.com +short
104.16.22.6 , 104.16.23.6 (CIS IP addresses)
```

### Nicht-Proxy-Ursprungsdatensätze mit vom Standard abweichenden Namen unkenntlich machen
{:#obsure-non-proxied-origin-records-with-non-standard-names}
Alle Datensätze, die nicht über IBM CIS als Proxy geleitet werden können und die noch Ihre Ursprungs-IP verwenden, z. B. FTP, können mithilfe einer zusätzlichen Verschleierung gesichert werden. Verwenden Sie insbesondere, wenn Sie einen Datensatz für Ihren Ursprung benötigen, der nicht über IBM CIS als Proxy geleitet werden kann, vom Standard abweichende Namen. Verwenden Sie beispielsweise `[beliebiges Wort oder beliebiges Zeichen].beispiel.com` anstelle von `ftp.beispiel.com`. Diese Verschleierung macht es weniger wahrscheinlich, dass bei Wörterverzeichnissuchen in Ihren DNS-Datensätzen Ihre Ursprungs-IP-Adresse offenbart wird. 

### Ggf. separate IP-Bereiche für HTTP- und Nicht-HTTP-Datenverkehr verwenden
{:#use-separate-ipranges-for-traffic}
Manche Kunden verwenden separate IP-Bereiche für HTTP- und Nicht-HTTP-Datenverkehr. Auf diese Weise können alle Datensätze, die auf ihren HTTP-IP-Bereich verweisen, über einen Proxy geleitet werden, und der gesamte Nicht-HTTP-Datenverkehr mithilfe eines anderen IP-Teilnetzes unkenntlich gemacht werden.

## Best Practice 2: Sicherheitsstufe selektiv konfigurieren
{:#best-practice-configure-security-level-selectively}
Ihre **Sicherheitsstufe** legt die Sensitivität unserer **IP-Reputationsdatenbank** fest. Um negative Interaktionen oder Fehlalarme zu verhindern, konfigurieren Sie Ihre **Sicherheitsstufe** domänenweise, d. h. erhöhen oder verringern Sie die Sicherheit nach Bedarf.

### Sicherheitsstufe für sensible Bereiche auf 'Hoch' setzen
{:#increase-security-level-for-sensitive-areas}
Sie können diese Einstellung auf der Seite für erweiterte Sicherheit für Ihre Domäne verschärfen oder Sie können eine **Seitenregel** für Verwaltungsseiten oder Anmeldeseiten hinzufügen, um Brute-Force-Angriffe zu reduzieren: 

1. Erstellen Sie eine **Seitenregel** mit dem URL-Muster Ihrer API (z. B. `www.beispiel.com/wp-login`). 
2. Legen Sie die Einstellung für die **Sicherheitsstufe** fest.
3. Markieren Sie die Einstellung als **Hoch**.
4. Wählen Sie **Ressource bereitstellen** aus.

### Niedrigere Sicherheitsstufe für nicht sensible Pfade oder APIs festlegen, um Fehlalarme zu reduzieren
{:#decrease-security-level-non-sensitive-paths-reduce-false-positives}
Diese Einstellung kann für allgemeine Seiten und allgemeinen API-Datenverkehr niedriger gewählt werden. 

1. Erstellen Sie eine **Seitenregel** mit dem URL-Muster Ihrer API (z. B. `www.beispiel.com/api/*`).
2. Legen Sie die Einstellung für die **Sicherheitsstufe** fest.
3. Wählen Sie die Sicherheitsstufe **Niedrig** oder **Praktisch aus** aus.
4. Wählen Sie **Ressource bereitstellen** aus.

### Welche Bedeutung haben die Einstellungen für die Sicherheitsstufe?
{:#what-do-security-level-settings-mean}
Unsere Einstellungen für die Sicherheitsstufe sind an Bedrohungsbewertungen angelehnt, die bestimmten IP-Adressen aufgrund böswilligen Verhaltens in unserem Netz zugeordnet sind. Eine Bedrohungsbewertung über 10 wird als hoch gewertet.

* **HOCH**: Bei Bedrohungsbewertungen über 0 wird eine Sicherheitsabfrage angezeigt.
* **MITTEL**: Bei Bedrohungsbewertungen über 14 wird eine Sicherheitsabfrage angezeigt.
* **NIEDRIG**: Bei Bedrohungsbewertungen über 24 wird eine Sicherheitsabfrage angezeigt.
* **PRAKTISCH AUS**: Bei Bedrohungsbewertungen über 49 wird eine Sicherheitsabfrage angezeigt.
* **AUS**: *Nur Enterprise* 
* **WIRD ATTACKIERT**: Sollte nur verwendet werden, wenn Ihre Website einer DDoS-Attacke ausgesetzt ist. Besucher erhalten für die Dauer von ca. fünf Sekunden eine Interstitial-Seite angezeigt, während CIS den Datenverkehr und das Verhalten analysiert, um sicherzustellen, dass es sich um einen berechtigten Besucher handelt, der versucht, auf die Webseite zuzugreifen. **WIRD ATTACKIERT** kann einige Aktionen in Ihrer Domäne wie beispielsweise eine API betreffen. Sie können eine angepasste Sicherheitsstufe für Ihre API oder einen beliebigen anderen Teil Ihrer Domäne festlegen, indem Sie eine Seitenregel für diesen Abschnitt erstellen. 

Wir empfehlen, Ihre Einstellungen für die Sicherheitsstufe in regelmäßigen Abständen zu überprüfen. Entsprechende Anweisungen finden Sie im Dokument [Best Practices für die CIS-Konfiguration](/docs/infrastructure/cis?topic=cis-best-practices-for-cis-setup).

## Best Practice 3: Web Application Firewall (WAF) sicher aktivieren
{:#best-practice-activate-waf-safely}
Ihre WAF ist im Abschnitt **Sicherheit** verfügbar. Wir gehen diese Einstellungen in umgekehrter Reihenfolge mit Ihnen durch, um sicherzustellen, dass Ihre WAF möglichst sicher konfiguriert ist, bevor Sie sie für die gesamte Domäne aktivieren. Diese anfänglichen Einstellungen können Fehlalarme reduzieren, indem die **Sicherheitsereignisse** für die weitere Optimierung befüllt werden. Ihre WAF wird automatisch aktualisiert, um neue Sicherheitslücken zu beheben, sobald sie erkannt werden.

Die WAF schützt vor den folgenden Typen von Angriffen:
* SQL-Injection-Attacke
* Cross-Site Scripting
* Cross-Site Forgery

Die WAF enthält einen Standardregelsatz, der Regeln zum Stoppen der gängigsten Angriffe enthält. Sie können die WAF jetzt entweder aktivieren oder inaktivieren und bestimmte Regeln in den WAF-Regelsätzen optimieren. Im Dokument [WAF-Standardregelsatz](/docs/infrastructure/cis?topic=cis-waf-default-rule-set) finden Sie weitere Details zum Standardregelsatz und zum Verhalten der einzelnen Regeln.

Weitere Informationen zur WAF finden Sie im Dokument [WAF-Konzepte](/docs/infrastructure/cis?topic=cis-web-application-firewall-concepts-q-a).

## Best Practice 4: TLS-Einstellungen konfigurieren
{:#best-practice-configure-tls-settings}
IBM CIS stellt eine Reihe von Optionen zum Verschlüsseln Ihres Datenverkehrs bereit. Als Reverse Proxy schließen wir TLS-Verbindungen in unseren Rechenzentren und öffnen eine neue TLS-Verbindung mit Ihrem Ursprungsserver. 

TLS bietet vier Betriebsarten:
* **Aus**: In diesem Modus ist TLS inaktiviert; diese Einstellung wird nicht empfohlen.
* **Client-zu-Edge**: TLS verschlüsselt Datenverkehr von CIS an Ihre Kunden, aber nicht von CIS an Ihre(n) Ursprungsserver.
* **End-to-End-flexibel**: TLS verschlüsselt den gesamten Datenverkehr. Sie können jedoch ein selbst signiertes Zertifikat verwenden, um den Datenverkehr zwischen CIS und Ihren Ursprungsservern zu sichern.
* **End-to-End-CA-signiert**: TLS verschlüsselt den gesamten Datenverkehr. Sie müssen ein CA-signiertes Zertifikat verwenden .

Weitere Informationen zu den TLS-Optionen finden Sie in [diesem Dokument](/docs/infrastructure/cis?topic=cis-tls-options).

IBM CIS lässt die Verwendung von benutzerdefinierten Zertifikaten zu. Oder Sie können ein Platzhalterzertifikat verwenden, das Ihnen von CIS bereitgestellt wird.

### Benutzerdefinierte Zertifikate hochladen
{:#upload-custom-certs}
Sie können Ihr benutzerdefiniertes Zertifikat hochladen, indem Sie auf die Schaltfläche **Zertifikat hinzufügen** klicken und das Zertifikat, den privaten Schlüssel und die Bündelmethode angeben. Wenn Sie Ihr eigenes Zertifikat hochladen, erzielen Sie sofortige Kompatibilität mit verschlüsseltem Datenverkehr und behalten die Kontrolle über Ihr Zertifikat (z. B. ein EV-Zertifikat). Denken Sie daran, dass Sie für die Verwaltung eines benutzerdefinierten Zertifikats selbst verantwortlich sind. Beispielsweise überwacht IBM CIS nicht das Verfallsdatum des Zertifikats.  

![Benutzerdefiniertes Zertifikat](images/upload-custom-certificate.png)

### Dedizierte Zertifikate bestellen
{:#order-dedicated-certs}
CIS vereinfacht die Verwaltung Ihrer Zertifikate durch die Bereitstellung dedizierter Zertifikate. Sie müssen nicht mehr private Schlüssel generieren, Zertifikatsignieranforderungen (CSR) erstellen oder daran denken, Zertifikate zu verlängern. Sie können ein dediziertes Zertifikat bestellen, indem Sie auf die Schaltfläche **Zertifikat hinzufügen** klicken und ein Platzhalterzertifikat bestellen oder Hostnamen eingeben, um ein dediziertes angepasstes Zertifikat zu bestellen. Die Zertifikattypen sind: 

 * Signiertes SHA-2/ECDSA-Zertifikat mit P-256-Schlüssel, 
 * signiertes SHA-2/RSA-Zertifikat mit RSA 2048-Bit-Schlüssel und  
 * signiertes SHA-1/RSA-Zertifikat mit RSA 2048-Bit-Schlüssel. 
 
CIS kann Zertifikate für alle TLDs außer für `.cu`, `.iq`, `.ir`, `.kp`, `.sd`, `.ss` und `.ye` ausstellen. CIS verwaltet das Ablaufdatum. Um die Hostnamen in Ihrem dedizierten, angepassten Zertifikat zu bearbeiten, müssen Sie diese neu bestellen und dann löschen. Sie bestellen zum Beispiel ein dediziertes, angepasstes Zertifikat mit dem Hostnamen `alpha.yourdomain.com`. Um den Hostnamen `beta.yourdomain.com` zu Ihrem dedizierten, angepassten Zertifikat hinzuzufügen, bestellen Sie ein anderes dediziertes, angepasstes Zertifikat mit den Hostnamen `alpha.yourdomain.com` und `beta.yourdomain.com`. Anschließend _müssen_ Sie das ursprüngliche, dedizierte, angepasste Zertifikat löschen. 

Wenn Sie zum ersten Mal ein dediziertes Zertifikat bestellen, wird der DCV-Prozess (Certificate Domain Control Validation) ausgeführt, der einen entsprechenden TXT-Datensatz generiert. Wenn Sie den TXT-Datensatz löschen, wird der DCV-Prozess erneut ausgeführt, wenn Sie ein anderes dediziertes Zertifikat bestellen. Wenn Sie ein dediziertes Zertifikat löschen, wird der entsprechende TXT-Datensatz für den DCV-Prozess nicht gelöscht.
{:note}

Es folgen einige gängige Fehler, die bei der Bestellung dedizierter Zertifikate auftreten können. 
* `Fehler beim Herstellen der Verbindung zum Zertifikatsservice.`
* `Fehler bei der Anforderung vom Zertifikatsservice. `
{:note}

Wenn ein Fehler beim Bestellen des Zertifikats auftritt, aktualisieren Sie die Seite und versuchen Sie es erneut. 

![Dediziertes Zertifikat](images/order-dedicated-certificate.png)

### Bereitgestelltes Zertifikat verwenden
{:#utilize-provisioned-certificate}
IBM zählt diverse Zertifizierungsstellen (Certificate Authorities, CAs) zu seinen Partnern, um unseren Kunden Platzhalterzertifikate für Domänen bereitstellen zu können. Für die Konfiguration dieser Zertifikate kann eine manuelle Überprüfung erforderlich sein. Ihr Support-Team unterstützt Sie bei diesen zusätzlichen Schritten.

### Zertifikatspriorität auf Ihrer Seite
{:#certificate-prioirity-at-our-edge}
Die Priorität mit der die Zertifikate auf Ihrer Seite angezeigt werden: 
1. Hochgeladen und angepasst
2. Dediziert und angepasst
3. Dediziert und Platzhalter
4. Universell

### Mindestversion von TLS
{:#security-minimum-tls-version}
Siehe [Mindestversion von TLS](/docs/infrastructure/cis?topic=cis-tls-options#minimum-tls-version). Höhere Versionen von TLS bieten mehr Sicherheit, verhindern aber möglicherweise, dass Kunden Ihre Site erreichen. 
