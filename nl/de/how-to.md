---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Overview page, page rules, Service Mode

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Verwalten Ihrer IBM CIS-Bereitstellung (Cloud Internet Services)
{:#manage-your-cis-deployment}

Sie beginnen mit der Übersichtsanzeige als Ausgangspunkt für alle weiteren Aktivitäten. Darin finden Sie alle aktuellen Parameter für Ihre Bereitstellung.

Nachdem Sie Ihr DNS eingerichtet und konfiguriert haben, kann es losgehen!

## Übersichtsanzeige verwenden
{:#using-the-overview-screen}

In der Übersichtsanzeige können Sie den Status aller Ihrer Auswahlen sehen. Jede Einstellung ist mit dem Abschnitt der Benutzerschnittstelle verbunden, in dem die Einstellung konfiguriert ist. Um eine Auswahl zu ändern, können Sie durch Klicken auf den Link für die Einstellung dorthin navigieren. Um zum Beispiel die Lastausgleichskonfiguration zu ändern oder eine neue Lastausgleichskonfiguration hinzuzufügen, klicken Sie auf das Feld `Lastausgleichsfunktion`.

In der Übersichtsanzeige können Sie sehen, dass Ihre Domänennamenkonfiguration den Status **Anstehend** oder **Aktiv** hat, wie in der folgenden Abbildung gezeigt.


![Abbildung der Übersichtsanzeige](images/overview-screen-configuration-summary.jpg)

Der Status **Anstehend** zeigt an, dass Ihre Domäne noch nicht vollständig konfiguriert ist. Sie haben Ihren DNS-Provider oder Registrator mit den Nameservern aktualisiert, die als Teil des Einrichtungsprozesses bereitgestellt wurden. 

**Nur Enterprise**: Im Abschnitt **Servicedetails** der Übersicht können Sie auch Domänen zu Ihrer CIS-Instanz hinzufügen und zwischen mehreren Domänen umschalten. 

## Servicemodus ändern
{#changing-the-service-mode}

Auf der Übersichtsseite können Sie das Dropdown-Menü im Abschnitt 'Servicemodus' verwenden, um einen der beiden Modi auszuwählen: 

* Der **Verteidigungsmodus** dient zum Schutz vor vorhandenen oder vorhergesagten DNS-Angriffen. Dieser Modus verhindert, dass der gesamte Datenverkehr Ihre Ursprungsserver über Ihre Domäne erreicht. 
* Mit **Service anhalten** werden alle Sicherheits- und Leistungsvorteile für Ihre Domäne inaktiviert. DNS-Funktionen führen weiterhin Auflösungen für Ihre Website durch, aber der Datenverkehr wird direkt an die konfigurierten Ursprünge gesendet.  

### Schritte beim Festlegen des Servicemodus
{:#steps-to-set-service-mode}

1. Wählen Sie den gewünschten Modus aus dem Dropdown-Menü aus.
1. Klicken Sie auf die Schaltfläche `Aktivieren` .
1. Bestätigen Sie die Auswahl oder stornieren Sie sie im Popup-Fenster für die Bestätigung. 

Auf allen Seiten wird eine Benachrichtigung angezeigt, die besagt, dass entweder 'Service anhalten' oder 'Verteidigungsmodus' aktiviert wurde.
Die Rückkehr zum Regelbetrieb erfolgt über das Klicken auf `Modus inaktivieren` innerhalb des Benachrichtigungsbanners ![Bild der Schaltfläche 'Modus inaktivieren'](images/deactivate-mode.png)


## DNS konfigurieren und verwalten
{:#configure-and-manage-your-dns}

Rufen Sie Ihre DNS-Seite auf und fügen Sie einen Datensatz hinzu (höchstwahrscheinlich ein Datensatz vom Typ A). Geben Sie die Informationen zu Ihrem DNS-Datensatz ein und klicken Sie auf `Datensatz hinzufügen`, um Ihre Änderungen zu implementieren.

![DNS hinzufügen](images/dns/create-a-type-record.png)

Nachdem Sie Ihre Datensätze erstellt haben, überlegen Sie, ob Sie die Einstellung `Proxy` aktivieren sollten. Die meisten Funktionen von CIS erfordern es, dass der Internetdatenverkehr auf Ihre Site über die CIS-Infrastruktur fließt. Mit anderen Worten, sie werden nur auf weitergeleitete Datensätze und Lastausgleichsfunktionen angewendet. Um tatsächliche die Vorteile von CIS voll auszunutzen, sollten Sie sicherstellen, dass Ihre DNS-Datensätze und Lastausgleichsfunktionen die Proxy-Einstellung aktiviert haben. 

## Caching einrichten und verwalten
{:#set-up-and-manage-your-caching}

Als Nächstes können Sie das Caching einrichten. 

![ABBILDUNG](images/caching-screen.png)

Sie können zwischen drei Typen von Caching auswählen, die im Dropdown-Menü der Caching-Ansicht verfügbar sind: 

 * Keine Abfragezeichenfolge: Es werden nur Ressourcen aus dem Cache bereitgestellt, wenn keine Abfragezeichenfolge vorhanden ist.
 * Unabhängig von Abfragezeichenfolge: Übergibt dieselbe Ressource an alle, unabhängig von der Abfragezeichenfolge. (Hinweis: Die Einstellung **Abfragezeichenfolge ignorieren** gilt nur für statische Dateierweiterungen. Diese Einstellung entfernt die Abfragezeichenfolge beim Generieren des Cache-Schlüssels, sodass eine Anforderung `style.css?something` normalisiert wird zu `style.css`, wenn sie den Cache passiert.)
 * Abhängig von Abfragezeichenfolge: Übergibt jedes Mal eine andere Ressource, wenn sich die Abfragezeichenfolge ändert.
  
## Cache löschen
{:#purge-cache-overview}
 
Sie können Ihren Cache jederzeit in Vorbereitung auf Aktualisierungen löschen, indem Sie einfach die URL in das Feld zum Löschen des Cache einfügen. Sie können eine einzelne Datei oder mehrere Dateien (bis zu 30 gleichzeitig) löschen.
 
 ## Verfallsdatum des Browsers
 {:#browser-expiration}
 
Im Dropdown-Menü können Sie das erforderliche Verfallsdatum des Browsers auswählen, z. B. 8 Stunden oder 1 Tag.

Nur Enterprise: Sie können CIS auch anweisen, keine Steuerelemente des Browser-Cache zu überschreiben, indem Sie für diese Einstellung **Vorhandene Header respektieren** festlegen.
 
 ## Entwicklungsmodus verwenden
 {:#using-development-mode}
 
Der **Entwicklungsmodus** ist für die Verwendung bei wichtigen Aktualisierungen oder neuen Dateiuploads vorgesehen, oder wenn Sie vermeiden möchten, dass die Endbenutzer den Cache nutzen, und sie Dateien stattdessen direkt von den Ursprungsservern abrufen sollen. Um den **Entwicklungsmodus** zu verwenden, schalten Sie ihn auf `Aktiviert` um. Wenn Sie den **Entwicklungsmodus** nicht nicht mehr verwenden möchten, schalten Sie ihn zurück auf `Inaktiviert`. Die Aktivierung des **Entwicklungsmodus** läuft automatisch nach drei Stunden ab. 

## Seitenregeln verwalten
{:#managing-your-page-rules}
 
Sie können Seitenregeln verwenden, um bestimmte Einstellung anzugeben, die nur für bestimmte URLs gelten, um beispielsweise unterschiedliche Einstellungen für die Cachesteuerung für bestimmte URL-Pfade zu verwenden. Verwenden Sie dazu die Dropdown-Menüs. Die Regeleinstellungen sind in drei Kategorien unterteilt: **Sicherheit**, **Leistung** und **Zuverlässigkeit**.

Beachten Sie: Wenn bestimmte Regeln aktiviert sind, werden andere Optionen abgeblendet, falls diese in Konflikt zu den eben ausgewählten Regeln stehen. Nachdem Sie die gewünschten Seitenregeln ausgewählt haben, klicken Sie auf **Bereitstellung**, um sie zu aktivieren. Die neuen Regeln werden sofort wirksam und sind auch sofort in der Ansicht 'Seitenregeln' sichtbar.
 
 ![SEITENREGELMENÜS](images/page-rule-dropdown-settings.png)
 
Sie können Ihre Seitenregeln auch in der Tabelle aktivieren oder inaktivieren, die in der Ansicht 'Seitenregeln' enthalten ist. Weitere Informationen finden Sie unter [Seitenregeln verwenden](/docs/infrastructure/cis?topic=cis-use-page-rules).
 
 ## Sicherheitseinstellungen
 {:#security-settings-overview}
 
Standardmäßig ist der DDoS-Schutz für alle DNS-Datensätze oder Lastausgleichsfunktionen mit eingeschalteter Weiterleitung aktiviert.
Die Sicherheitseinstellungen sind:  

* Aktivieren Sie WAF mithilfe des Schalters auf der Seite **Web Application Firewall**. Wenn Sie die Regeln ein- oder ausschalten, werden die Änderungen sofort wirksam.

* **Nur Enterprise**: Die Seite **Drosselung** ermöglicht Ihnen, Regeln für die Drosselung zu konfigurieren, um 'Noisy Neighbor'-Probleme zu vermeiden und DDoS abzuwehren. 

* Auf der Seite **IP-Firewall** können Sie Zugriffsregeln auf Grundlage von IP, Ländercode oder ASN konfigurieren. Sie können auch Regeln konfigurieren, um Benutzeragenten zu blockieren. Im Abschnitt über Domänensperrung dieser Seite, erfahren Sie, wie Sie den Zugriff auf Ihre Domäne auf bestimmte IP-Adressen beschränken können. 

* Sie können die für die Firewall wichtigen Ereignisse auf der Seite **Ereignisse** überprüfen. 

## Zertifikate
{:#certificates-overview}

Wenn Sie eine Domäne konfigurieren, stellt IBM CIS automatisch ein universelles Zertifikat für diese Domäne zur Verfügung. Sie müssen also nichts unternehmen, um in dieser Domäne zertifikatbasierten Schutz zu erhalten. Wenn Sie möchten, können Sie Ihr eigenes Zertifikat hochladen. Sie benötigen ein separates Zertifikat für jede Domäne und Ihnen wird eine Fehlernachricht angezeigt, wenn das Zertifikat, das Sie hochladen, nicht mit Ihrer Domäne übereinstimmt. Auf dieser Seite können Sie auch angepasste Zertifikate anfordern.  

![ABBILDUNG](images/certificates-table.png)
 
 
