---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Use Page Rules, Page Rule

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Verwenden von Seitenregeln
{:#use-page-rules}

Eine Seitenregel gibt Einstellungen und Werte an, die Sie auf ein bestimmtes URL-Muster anwenden können, das Ihre Domäne referenziert. Seitenregeln unterstützen Sie beim Verwalten der Sicherheit, Leistung und Zuverlässigkeit basierend auf den einzelnen URLs in Ihrer Website. Die folgende Tabelle beschreibt die Seitenregeln, die für alle Kunden zur Verfügung stehen, das bezweckte Verhalten und was Sie berücksichtigen sollten, bevor Sie sie verwenden.

## Sicherheit
{:#page-rules-security}

| **Einstellung** | **Verhalten** | **Hinweise** |
|-----------|----------|----------------|
|**Browserintegritätsprüfung**|Sucht nach gängigen HTTP-Headern, die von Spammern verwendet werden, und verweigert den Zugriff auf Ihre Seite. Diese Einstellung blockiert außerdem Besucher, die keinen Benutzeragenten haben oder einen vom Standard abweichenden Benutzeragenten hinzufügen (wird oft von böswilligen Bots, Crawlern oder APIs eingesetzt). | |
|**Sicherheit inaktivieren**|Inaktiviert die folgenden Funktionen: <ul><li>E-Mail-Verschleierung</li> <li>Serverseitige Ausschlüsse</li> <li>WAF</li></ul>|Wenn eine Regel die Sicherheit inaktiviert und eine andere die WAF aktiviert, hat die WAF-Regel Vorrang, unabhängig von der Reihenfolge ihres Auftauchens.|
|**E-Mail-Verschleierung**|Schaltet die E-Mail-Verschleierung ein oder aus. | |
|**IP-Geoortungs-Header**|Schließt den Landescode des Standorts des Benutzers in alle Anforderungen an Ihre Website ein. Die Informationen befinden sich im HTTP-Header `CF-IPCountry`. | |  
|**Sicherheitsstufe**|Steuert, wie hoch die Bedrohungsbewertung eines Kunden sein muss, damit eine Sicherheitsabfrage ausgegeben wird. Diese Einstellung kann verwendet werden, damit Besuchern Ihrer Website immer die **Verteidigungsmodus**-Sicherheitsabfrage angezeigt wird. | |
|**Serverseitige Ausschlüsse**|Schaltet die serverseitigen Ausschlüsse ein oder aus.  | |
|**TLS**|Steuert, welcher TLS-Modus verwendet wird. | |
|**WAF**|Schaltet die WAF ein oder aus. | |  
|**Automatische HTTPS-Umschreibevorgänge**|Schaltet automatische HTTPS-Umschreibevorgänge ein oder aus.  | |
|**Opportunistische Verschlüsselung**|Schaltet die opportunistische Verschlüsselung ein oder aus.  | |
|**Cache-Täuschungsschutz**|Schaltet den Cache-Täuschungsschutz ein oder aus.  | |
|**Immer HTTPS verwenden**|Konvertiert alle `http://`-URLs in `https://`-URLs, indem eine `301`-Umleitung eingerichtet wird. |Diese Einstellung inaktiviert die Konfiguration aller anderen Einstellungen für die Regel, weil IBM CIS für die Anforderung eine Umleitung an `HTTPS` erzwingt, wodurch eine neue Anforderung entsteht, die dann gegen die Seitenregeln ausgewertet wird. |
|**Header mit gültiger Client-IP**|CIS sendet die IP-Adresse des Endbenutzers im Header mit der gültigen Client-IP (`True-Client-IP`-Header).  |Nur Enterprise |

## Leistung
{:#page-rules-performance}

| **Einstellung** | **Verhalten** | **Hinweise** |
|-----------|----------|----------------|
|**Browser-Cache-TTL**|Steuert, wie lange Ressourcen, die von Client-Browsern zwischengespeichert werden, gültig sind. | |
|**Cacheumgehung bei Cookie**|Stellt ein zwischengespeichertes Objekt bereit, wenn nicht ein Cookie mit einem bestimmten Namen vorhanden ist. Beispielsweise wird eine zwischengespeicherte Version der Homepage bereitgestellt, es sei denn, ein Cookie `SessionID` ist vorhanden, das angibt, dass der Kunde angemeldet ist und ihm deshalb personalisierter Inhalt angezeigt werden soll. | |
|**Cachestufe**|**Umgehen** - Ressourcen, die mit der Seitenregel übereinstimmen, werden nicht zwischengespeichert.<br>**Keine Abfragezeichenfolge** - Es werden nur Ressourcen aus dem Cache bereitgestellt, wenn keine Abfragezeichenfolge vorhanden ist.<br>**Abfragezeichenfolge ignorieren** - Stellt allen dieselbe Ressource bereit, unabhängig von der Abfragezeichenfolge.<br>**Standard** - Übergibt jedes Mal eine andere Ressource, wenn sich die Abfragezeichenfolge ändert.<br> **Alles zwischenspeichern** - Ressourcen, die mit der Seitenregel übereinstimmen, werden nicht zwischengespeichert.|Standardmäßig wird HTML-Inhalt nicht zwischengespeichert. Eine Seitenregel zum Zwischenspeichern statischen HTML-Inhalts muss geschrieben werden. |
|**Edge-Cache-TTL**|Steuert, wie lange IBM CIS Dateien in unserem Cache aufbewahrt. |Diese Einstellung ist bei der Angabe einer Cachestufe optional. |
|**Überschreibung auflösen**|Ändert die URL oder IP, in die die Anforderung aufgelöst wird, die mit der Seitenregel übereinstimmt. ||
|**Caching bei Cookie**|Wendet die Option `Alles zwischenspeichern` (Einstellung `Cachestufe`) auf Grundlage der Übereinstimmung eines regulären Ausdrucks mit einem Cookienamen an. Wenn Sie beide Einstellungen und `Cacheumgehung bei Cookie` zu derselben Seitenregel hinzufügen, hat `Cacheumgehung bei Cookie` Vorrang vor `Caching bei Cookie`.|Nur Enterprise|
|**Leistung inaktivieren**|Ausschalten von:<ul><li>`Webinhalte komprimieren`</li><li>`Bildlastoptimierung`</li><li>`Optimierung der Bildgröße`</li><li>`Scriptlastoptimierung`</li></ul> |Nur Enterprise|
|**Webinhalte komprimieren**|HTML-, CSS- und/oder JavaScript-Dateien durch Entfernen aller unnötigen Zeichen aus diesen Dateien komprimieren. |Nur Enterprise|
|**Bildlastoptimierung**|Verbessert die Ladezeit für Seiten mit Bildern auf Grundlage der Netzverbindung und des Einheitentyps durch: <ul><li>**Bildvirtualisierung** - Ersetzt Bilder durch Platzhalterbilder mit geringer Auflösung, die dieselben Dimensionen wie das Original aufweisen (einschließlich Bilder anderer Anbieter). Sobald die Seite vollständig wiedergegeben wird, werden die Bilder mit voller Auflösung mit wenig Aufwand geladen (wobei die Bilder im Darstellungsfeld des Browsers die höchste Priorität haben). Dieser Prozess ermöglicht es, Seiten schnell wiederzugeben und minimiert den Rückfluss an den Browser. </li><li>**Anforderungen rationalisieren** - Kombiniert mehrere einzelne Netzanforderungen für Bilder in einer einzigen Anforderung. </li></ul> |Nur Enterprise|
|**Optimierung der Bildgröße**|Verringert die Größe der Bilddatei, indem Metadaten (Datum und Uhrzeit, Kamerahersteller und -modell, etc). entfernt werden und indem Bilder nach Möglichkeit komprimiert werden. Kleinere Dateigrößen bedeuten schnellere Ladezeiten für Bilder und Webseiten. |Nur Enterprise|
|**Abfragezeichenfolge sortieren**|Behandelt Dateien mit denselben Abfragezeichenfolgen als dieselbe Datei im Cache. Dies erfolgt unabhängig von der Reihenfolge der Abfragezeichenfolgen. |Nur Enterprise|
|**Antwortpufferung**|Aktivieren oder Inaktivieren der Pufferung von Antworten vom Ursprungsserver. Standardmäßig sendet CIS Pakete an den Client, sobald diese empfangen werden. Die Aktivierung der Antwortpufferung bedeutet, dass CIS wartet, bis die gesamte Datei vorhanden ist, bevor sie an den Endbenutzer weitergeleitet wird. |Nur Enterprise|
|**Scriptlastoptimierung**|Verbessert die Füllzeiten durch asynchrones Laden Ihrer Javascripts, einschließlich Scripts anderer Anbieter, sodass sie die Wiedergabe des Inhalts Ihrer Webseiten nicht blockieren. |Nur Enterprise|

## Zuverlässigkeit
{:#page-rules-reliability}

| **Einstellung** | **Verhalten** | **Hinweise** |
|-----------|----------|----------------|
|**Nicht aktuellen Inhalt speichern**|Hält eine eingeschränkte Version der Website online, wenn der Server ausfällt. |Weitere Informationen finden Sie unter [Verwalten Ihrer IBM CIS-Bereitstellung für eine optimale Zuverlässigkeit](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability). |
|**Ursprungscachesteuerung**|Bestimmt, welche Inhalte vom Ursprung zwischengespeichert werden und wie oft der Inhalt aktualisiert wird. |Weitere Informationen finden Sie unter [Verwalten Ihrer IBM CIS-Bereitstellung für eine optimale Zuverlässigkeit](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability). |
|**Weiterleitungs-URL** |URL, die verwendet werden soll, wenn die Website nicht verfügbar ist. |Diese Einstellung inaktiviert die Konfiguration aller anderen Einstellungen, weil Sie die Anforderung an eine andere Stelle weiterleiten. Weitere Informationen finden Sie unter [Verwalten Ihrer IBM CIS-Bereitstellung für eine optimale Zuverlässigkeit](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability).|
|**Überschreibung des Host-Headers**|Ersetzt den Host-Header durch einen URI, der mit der Seitenregel für den angegebenen Wert übereinstimmt. Dies wird normalerweise für Inhalt verwendet, der in einem S3-Bucket gehostet wird. |
|**Apps inaktivieren**|Inaktiviert alle CIS-Apps. |Nur Enterprise|
|**Durchgriff zu Ursprungsfehlerseite**|Inaktiviert CIS-Fehlerseiten, die das Senden von Problemen vom Ursprungsserver auslösen, und zeigt stattdessen die Fehlerseite im Ursprung an. |Nur Enterprise||

## URL-Muster von Seitenregeln
{:#page-rule-url-patterns}

Eine Seitenregel tritt für ein gegebenes URL-Muster in Kraft, wobei das folgende Format verwendet wird:

`<scheme>://<hostname><:port>/<path>`

Ein Beispiel, das alle Komponenten verwendet, sähe so aus:

`https://www.beispiel.com:80/image.png`

Die *Schema*- und *Port*-Komponenten sind optional. Falls das Schema nicht angegeben wird, sind beide Protokolle - `http://` und `https://` - abgedeckt. Falls der Port nicht angegeben ist, stimmt die Regel mit allen Ports überein. Sie können grundlegende Platzhalterabgleiche ausführen, indem Sie das Symbol '*' in Ihrem Regelmuster verwenden, sodass es mit einer Reihe von ähnlichen Mustern statt mit nur einem übereinstimmt.

Diese drei Punkte sollten Sie im Hinterkopf behalten, wenn Sie mit Seitenregeln arbeiten:

 * Es kann immer nur eine Seitenregel für eine gegebene Anforderung in Kraft treten.
 * Die Priorität von Seitenregeln entspricht der Reihenfolge, in der sie aufgeführt sind.
 * Sobald eine URL mit einer Regel übereinstimmt, wird nur diese Regel angewendet. Das heißt, wenn bereits eine Seitenregel auf eine Anforderung angewendet wurde, sind alle nachfolgenden Regeln, die ebenfalls mit dem URL-Muster übereinstimmen, nicht wirksam. Grundsätzlich empfehlen wir, zunächst die besonders spezifischen Seitenregeln aufzuführen und dann erst die weniger spezifischen.

Seitenregeln können inaktiviert werden. Dann treten sie nicht mehr in Kraft. Aber sie sind weiterhin in der Liste enthalten und können bearbeitet werden. Wenn Sie die Option **Aktiviert** auf **Aus** setzen, wird eine Seitenregel erstellt, die ursprünglich inaktiviert ist.

Weitere Informationen finden Sie im Dokument zu [Caching und Seitenregeln](/docs/infrastructure/cis?topic=cis-use-page-rules-with-caching).
