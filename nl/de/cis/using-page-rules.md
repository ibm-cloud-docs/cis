---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Verwenden von Seitenregeln

Eine Seitenregel gibt Einstellungen und Werte an, die Sie auf ein bestimmtes URL-Muster anwenden können, das Ihre Domäne referenziert. Seitenregeln unterstützen Sie beim Verwalten der Sicherheit, Leistung und Zuverlässigkeit basierend auf den einzelnen URLs in Ihrer Website. Die folgende Tabelle beschreibt die Seitenregeln, die für alle Kunden zur Verfügung stehen, das bezweckte Verhalten und was Sie berücksichtigen sollten, bevor Sie sie verwenden. 

## Sicherheit

| **Einstellung** | **Verhalten** | **Hinweise** |
|-----------|----------|----------------|
|**Browserintegritätsprüfung**|Sucht nach gängigen HTTP-Headern, die von Spammern verwendet werden, und verweigert den Zugriff auf Ihre Seite. Diese Einstellung blockiert außerdem Besucher, die keinen Benutzeragenten haben oder einen vom Standard abweichenden Benutzeragenten hinzufügen (wird oft von böswilligen Bots, Crawlern oder APIs eingesetzt). | |
|**Sicherheit inaktivieren**|Inaktiviert die folgenden Funktionen: <ul><li>E-Mail-Verschleierung</li> <li>Serverseitige Ausschlüsse</li> <li>WAF</li></ul>|Wenn eine Regel die Sicherheit inaktiviert und eine andere die WAF aktiviert, hat die WAF-Regel Vorrang, unabhängig von der Reihenfolge ihres Auftauchens. |
|**E-Mail-Verschleierung**|Schaltet die E-Mail-Verschleierung ein oder aus. | |
|**IP-Geoortungs-Header**|Schließt den Landescode des Standorts des Benutzers in alle Anforderungen an Ihre Website ein. Die Informationen befinden sich im HTTP-Header `CF-IPCountry`. | |  
|**Sicherheitsstufe**|Steuert, wie hoch die Bedrohungsbewertung eines Clients sein muss, damit eine Sicherheitsabfrage angezeigt wird. Diese Einstellung kann verwendet werden, damit Besuchern Ihrer Website immer die **Verteidigungsmodus**-Sicherheitsabfrage angezeigt wird. | |
|**Serverseitige Ausschlüsse**|Schaltet die serverseitigen Ausschlüsse ein oder aus. | |
|**TLS**|Steuert, welcher TLS-Modus verwendet wird. | |
|**WAF**|Schaltet die WAF ein oder aus. | |  
|**Automatische HTTPS-Umschreibevorgänge**|Schaltet automatische HTTPS-Umschreibevorgänge ein oder aus. | |
|**Opportunistische Verschlüsselung**|Schaltet die opportunistische Verschlüsselung ein oder aus. | |
|**Cache-Täuschungsschutz**|Schaltet den Cache-Täuschungsschutz ein oder aus. | |
|**Immer HTTPS verwenden**|Konvertiert alle `http://`-URLs in `https://`-URLs, indem eine `301`-Umleitung eingerichtet wird. |Diese Einstellung inaktiviert die Konfiguration aller anderen Einstellungen für die Regel, weil IBM CIS für die Anforderung eine Umleitung an `HTTPS` erzwingt, wodurch eine neue Anforderung entsteht, die dann gegen die Seitenregeln ausgewertet wird. |

## Leistung
| **Einstellung** | **Verhalten** | **Hinweise** |
|-----------|----------|----------------|
|**Browser-Cache-TTL**|Steuert, wie lange Ressourcen, die von Client-Browsern zwischengespeichert werden, gültig sind. | |
|**Cacheumgehung bei Cookie**|Stellt ein zwischengespeichertes Objekt bereit, wenn nicht ein Cookie mit einem bestimmten Namen vorhanden ist. Beispielsweise wird eine zwischengespeicherte Version der Homepage bereitgestellt, es sei denn, ein Cookie `SessionID` ist vorhanden, das angibt, dass der Kunde angemeldet ist und ihm deshalb personalisierter Inhalt angezeigt werden soll. | |
|**Cachestufe**|**Umgehen** - Ressourcen, die mit der Seitenregel übereinstimmen, werden nicht zwischengespeichert. <br>**Keine Abfragezeichenfolge** - Es werden nur Ressourcen aus dem Cache bereitgestellt, wenn keine Abfragezeichenfolge vorhanden ist. <br>**Abfragezeichenfolge ignorieren** - Stellt allen dieselbe Ressource bereit, unabhängig von der Abfragezeichenfolge. <br>**Standard** - Übergibt jedes Mal eine andere Ressource, wenn sich die Abfragezeichenfolge ändert. <br> **Alles zwischenspeichern** - Ressourcen, die mit der Seitenregel übereinstimmen, werden nicht zwischengespeichert. |Standardmäßig wird HTML-Inhalt nicht zwischengespeichert. Eine Seitenregel zum Zwischenspeichern statischen HTML-Inhalts muss geschrieben werden. |
|**Edge-Cache-TTL**|Steuert, wie lange IBM CIS Dateien in unserem Cache aufbewahrt. |Diese Einstellung ist bei der Angabe einer Cachestufe optional. |

## Zuverlässigkeit
| **Einstellung** | **Verhalten** | **Hinweise** |
|-----------|----------|----------------|
|**Immer online**|Hält eine eingeschränkte Version der Website online, wenn der Server ausfällt. |Weitere Informationen finden Sie unter [Verwalten Ihrer IBM CIS-Bereitstellung für eine optimale Zuverlässigkeit](managing-for-reliability.html). |
|**Ursprungscachesteuerung**|Bestimmt, welche Inhalte vom Ursprung zwischengespeichert werden und wie oft der Inhalt aktualisiert wird. |Weitere Informationen finden Sie unter [Verwalten Ihrer IBM CIS-Bereitstellung für eine optimale Zuverlässigkeit](managing-for-reliability.html). |
|**Weiterleitungs-URL** |URL, die verwendet werden soll, wenn die Website nicht verfügbar ist. | Diese Einstellung inaktiviert die Konfiguration aller anderen Einstellungen, weil Sie die Anforderung an eine andere Stelle weiterleiten. Weitere Informationen finden Sie unter [Verwalten Ihrer IBM CIS-Bereitstellung für eine optimale Zuverlässigkeit](managing-for-reliability.html). |

## URL-Muster von Seitenregeln

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

Weitere Informationen finden Sie im Dokument zu [Caching und Seitenregeln](caching-with-page-rules.html). 
