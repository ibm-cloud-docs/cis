---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Verwalten Ihrer IBM CIS-Bereitstellung für eine optimale Zuverlässigkeit

Um eine optimale Zuverlässigkeit Ihrer IBM CIS-Bereitstellung zu erzielen, können Sie eine unterstützende DNS-Konfiguration und globale Lastausgleichsfunktionen (Global Load Balancers. GLBs) einrichten. Für zusätzliche Zuverlässigkeit können Sie mithilfe unserer Seitenregeln sicherstellen, dass Ihre Webinhalte auch dann an Ihre Kunden geliefert werden, wenn mit Ihrem Ursprungsserver oder Cache Probleme auftreten. In diesem Dokument finden Sie Details zu einigen Best Practices für eine optimale Zuverlässigkeit Ihrer IBM CIS-Bereitstellung. 

Allgemein empfehlen wir folgende Best Practices: 

 * Einrichten Ihres DNS zur Nutzung von IBM CIS-Proxy-Servern und anderen Features. 
 * Verwenden mindestens einer globalen Lastausgleichsfunktion zur gleichmäßigen Verteilung Ihres Website-Datenverkehrs. 
 * Einrichten passender Seitenregeln zum Verwalten des Caching und anderer Optionen. 

Jeder dieser Aspekte bietet eine bestimmte Funktionalität, die Sie verwenden können, um eine zuverlässigere CIS-Bereitstellung zu erstellen. 

Beachten Sie, dass die CIS-Schnittstelle in Abschnitte für *Sicherheit*, *Zuverlässigkeit* und *Leistung* unterteilt ist. Das Hauptnavigationsmenü wird in der folgenden Abbildung angezeigt, mit den Menüpunkten 'Globale Lastausgleichsfunktionen' und 'DNS': 

![Linke Navigation, DNS ](images/cis-left-navigation.png)


## Einrichten von DNS
 
 Um mit der Einrichtung Ihrer DNS-Konfiguration zu beginnen, wählen Sie wie bereits gezeigt **DNS** im Navigationsmenü aus. 
 
 Ausführliche Informationen zum Einrichten und Verwalten Ihres DNS für hohe Zuverlässigkeit [finden Sie in diesem Dokument](dns.html#setting-up-your-domain-name-system-dns-for-ibm-cis). 


## Einrichten von globalen Lastausgleichsfunktionen


Zum Einrichten Ihrer globalen Lastausgleichsfunktionen wählen Sie im Navigationsmenü **Globale Lastausgleichsfunktionen** aus. 

Ausführliche Informationen zum Einrichten und Verwalten Ihrer globalen Lastausgleichsfunktionen [finden Sie in diesem Dokument](glb.html#global-load-balancer-glb-concepts). 

## Verwenden von Seitenregeln zum Steigern der Zuverlässigkeit

Im Folgenden finden Sie einige empfohlene Einstellungen für Seitenregeln, um Ihrer Website maximale Zuverlässigkeit zu verleihen: 

 * Immer online
 * Ursprungscachesteuerung
 * Weiterleitungs-URL

 ## Immer online

Sie können die Seitenregeleinstellung **Immer online** verwenden, um eine eingeschränkte Version Ihrer Website online zu halten, wenn Ihr Server ausfällt. 

Ist die Einstellung **Immer online** aktiv, stellt IBM CIS beim Ausfall Ihres Servers Seiten aus unserem Cache bereit, damit Ihre Besucher noch einige der Seiten, die sie aufzurufen versuchen, angezeigt bekommen. Ihren Besuchern wird oben auf der Seite eine Nachricht angezeigt, die sie darüber informiert, dass sie sich im Offline-Browsing-Modus befinden. 'Immer online' gibt den HTTP-Status 503 zurück, der aber auch von vielen anderen Webanwendungen verwendet wird. Sobald Ihr Server wieder online ist, führt IBM CIS die Benutzer nahtlos zu einem normalen Browsing zurück. 

Falls IBM CIS die angeforderte Seite nicht im Cache findet, werden Ihre Besucher auf einer Fehlerseite darüber informiert, dass die gewünschte Seite der Website offline ist. 

### Aktivierung von 'Immer online'

Führen Sie die folgenden Schritte aus, um **Immer online** zu aktivieren: 

 * Wählen Sie im Navigationsmenü unter 'Leistung' das Element 'Seitenregeln' aus. 
 * Erstellen Sie eine Seitenregel mit dem URL-Muster Ihrer Domäne. 
 * Fügen Sie die Einstellung **Immer online** mit aktivierter Umschalttaste hinzu. 
 * Wählen Sie 'Ressource bereitstellen' aus. 

 ### Einschränkungen von 'Immer online'

 * **Immer online** stellt die ersten zehn Links Ihrer Stamm-HTML in den Cache, dann jeweils die ersten Links dieser Seiten und abschließend die ersten Links aller nachfolgenden Seiten. Das bedeutet, dass nur manche Seiten Ihrer Website angezeigt werden können, wenn Ihr Ursprungsserver ausfällt. 

 * Bei kürzlich hinzugefügten Websites ist der Cache noch nicht besonders umfangreich, was dazu führen kann, dass **Immer online** noch nicht funktioniert. 

 * CIS kann keine nicht öffentlichen Inhalte anzeigen oder übergebene Formulare (POSTs) verarbeiten, wenn Ihr Server ausfällt. Besuchern wird auf Check-out-Seiten oder anderen Elementen, die eine Anmeldung erfordern, ein Fehler angezeigt. 

 * Damit **Immer online** getriggert wird, muss Ihr Web-Server einen Standard-HTTP-Fehlercode 502 oder 504 für eine Zeitlimitüberschreitung zurückgeben. 'Immer online' arbeitet auch, wenn Probleme beim Herstellen einer Verbindung mit Ihrem Ursprung auftreten (Fehler 521 & 523), bei Zeitlimitüberschreitungen (522 & 524), bei SSL-Fehlern (525 & 526) oder bei unbekannten Fehlern (520). **Immer online** wird nicht für andere HTTP-Antwortcodes wie 404s, 500, 503, für Datenbankverbindungsfehler, für interne Serverfehler oder für leere Antworten vom Server getriggert. 

 * **Immer online** wird nicht aktiv, wenn die Seitenregel 'Alles zwischenspeichern' mit einer Einstellung 'Ablauf-TTL für Edge-Cache' aktiviert ist, die niedriger ist als die Caching-Frequenz (Kostenlos-Kunden: 7 Tage, Pro-Kunden: 3 Tage und Business- oder Enterprise-Kunden: 1 Tag), da die Einstellung 'Ablauf-TTL für Edge-Cache' vorgibt, dass der **Immer online**-Cache in dem entsprechenden Intervall gelöscht wird. 

## Ursprungscachesteuerung

Mit der Seitenregeleinstellung **Ursprungscachesteuerung** können Sie bestimmen, welche Inhalte von Ihrem Ursprungsserver zwischengespeichert und wie oft die Inhalte aktualisiert werden. Dies wirkt sich auf die Zuverlässigkeit und die Leistung aus. Wenn keine Einstellungen geändert werden und keine Header, die das Zwischenspeichern verhindern würden, vom Ursprungsserver gesendet werden, stellt IBM CIS alle statischen Inhalte mit bestimmten Erweiterungen in den Cache. Zu diesen Arten von Inhalt gehören Bilder, CSS und JavaScript. Dieses Caching dient in erster Linie Leistungszwecken. 

Zum Einrichten von **Ursprungscachesteuerung** würden Sie Seitenregeln verwenden, die bestimmte Header einschalten, die für die einzelnen Ressourcen Ihres Inhalts das gewünschte Verhalten liefern. Um zu verstehen, wie **Ursprungscachesteuerung** verwendet wird, gehen wir zunächst allgemein auf Seitenregeln und das allgemeine Caching-Verhalten für CIS ein, um den Kontext für die nächsten Abschnitte zu liefern. Es gibt drei Methoden, die Sie verwenden können, um Caching im Allgemeinen zu steuern, und **Ursprungscachesteuerung** ist die zweite. 

Das Einrichten von **Ursprungscachesteuerung** ruft Caching-Regeln auf, die sich eng an Internet-Best-Practices und RFCs orientieren, vor allem im Hinblick auf eine erneute Validierung. Zum Beispiel stellt CIS bei der Einstellung `max-age=0` standardmäßig keine Inhalte in den Cache, während die Einstellung **Ursprungscachesteuerung** Inhalte zwischenspeichert, aber immer erneut validiert. 

### Aktivierung von 'Ursprungscachesteuerung'

 * Wählen Sie im Navigationsmenü unter 'Leistung' das Element 'Seitenregeln' aus. 
 * Erstellen Sie eine Seitenregel mit dem URL-Muster, das Ihre Domäne referenziert. 
 * Fügen Sie die Einstellung **Ursprungscachesteuerung** mit aktivierter Umschalttaste hinzu. 
 * Wählen Sie 'Ressource bereitstellen' aus. 

### Rangfolge von Seitenregeln

Zwei bestimmte Seitenregeln haben beim Caching allgemein Vorrang: 

 * Wenn für eine Seitenregel die Option **Cachestufe** auf `Übergehen` gesetzt ist, werden die Ressourcen, die mit der Seitenregel übereinstimmen, nicht zwischengespeichert. IBM CIS agiert weiterhin als Proxy und unsere anderen Leistungsmerkmale bleiben aktiv. Ihr Inhalt wird jedoch nicht aus unserem Cache bereitgestellt, sondern direkt von Ihrem Ursprungsserver abgerufen. 

 * Wenn für eine Seitenregel die Option **Cachestufe** auf `Alles zwischenspeichern` gesetzt ist, werden Ressourcen, die mit der Seitenregel übereinstimmen, zwischengespeichert. **Die Verwendung dieser Seitenregel ist die einzige Möglichkeit, uns anzuweisen, nicht nur solche Ressourcen zwischenzuspeichern, die wir als statisch betrachten, darunter HTML.** 

Wenn keine Seitenregel festgelegt ist, verwenden wir den Caching-Modus `Standard`, der auf der Erweiterung der Ressource basiert. Es werden nur statische Ressourcen zwischengespeichert (wie zuvor erwähnt). 

### Header 'cache-control' vom Ursprungsserver

Die zweite Möglichkeit, zu ändern, welche Inhalte IBM CIS zwischenspeichert, besteht im Caching von Headern, die vom Ursprungsserver gesendet werden. CIS respektiert diese Einstellungen, aber Sie können sie mit der Einstellung für die Seitenregel **Edge-Cache-TTL** außer Kraft setzen. Dies sind die Header, die wir bei unserer Entscheidung, welche Ressourcen von Ihrem Ursprungsserver zwischengespeichert werden sollen, berücksichtigen: 

 * Falls der Header **Cache-Control** auf `private`, `no-store`, `no-cache` oder `max-age=0` gesetzt ist oder falls die Antwort einen Cookie enthält, stellt IBM CIS die Ressource nicht in den Cache. Denken Sie daran, dass sensible Informationen nicht zwischengespeichert werden sollen. Verwenden Sie in solchen Fällen einen dieser Header. 

 * Falls der Header **Cache-Control** auf `public` gesetzt und `max-age` größer als '0' ist oder falls die `Expires`-Header auf einen Zeitpunkt in der Zukunft gesetzt sind, wird die Ressource zwischengespeichert. 

**Hinweis:** Lauf RFC-Regeln hat `Cache-Control: max-age` Vorrang vor `Expires`-Headern. Wenn beide festgelegt sind und in Konflikt zueinander stehen, hat `max-age` Vorrang. 

### Header 's-maxage'

Die dritte Möglichkeit, das Caching-Verhalten und Browser-Caching-Verhalten gemeinsam zu steuern, ist die Verwendung des 'Cache-Control'-Headers `s-maxage`. 

In der Regel respektieren wir die Anweisung `max-age`. 

`Cache-Control: max-age=1000`

Wenn Sie jedoch ein Cachezeitlimit angeben möchten, das sich vom Browser unterscheidet, können Sie `s-maxage` verwenden. Im folgenden Beispiel wird IBM CIS angewiesen, das Objekt für 200 Sekunden zwischenzuspeichern, und der Browser wird angewiesen, das Objekt für 60 Sekunden zwischenzuspeichern. 

`Cache-Control: s-maxage=200, max-age=60`

Grundsätzlich sollen auf `s-maxage` NUR Reverse Proxys folgen (der Browser sollte das also ignorieren), während andererseits IBM CIS `s-maxage` Priorität verleiht, falls angegeben. Wir akzeptieren den höheren Wert: ob Browser-Cacheeinstellung oder Header `max-age`. 

### Zusammenfassung der Cachesteuerungsheader und Seitenregeln für Zuverlässigkeit

Dies sind die relevantesten Bereiche im Hinblick auf die Zuverlässigkeit beim Caching: 

 * Prüfen Sie die Caching-Header Ihres Ursprungsservers, um sicherzustellen, dass keine überschreibenden Header für zwischenspeicherbare Ressourcen vorhanden sind (`Cache-Control` und `Expires`). 

 * CIS stellt statische Inhalte standardmäßig in den Cache, wobei die folgende TTL vom Rückgabecode abhängt. 

```
200 301    120m;
302 303    20m;
403        5m; for reliability
404        5m;
any        0s;
```

 * Wenn Sie mehr Inhalte zwischenspeichern möchten, erstellen Sie eine Seitenregel, deren Option **Cachestufe** für die gewünschte URL auf 'Alles zwischenspeichern' gesetzt ist (falls Ihr Web-Server bei Abfrage dieser URL einen 404-Fehler zurückgibt, wird dieses Ergebnis nur für 5 Minuten zwischengespeichert). 

 * Wenn Sie nicht möchten, dass Inhalte einer URL zwischengespeichert werden, erstellen Sie eine Seitenregel, deren Option **Cachestufe** 'Übergehen' lautet. 


 ## Weiterleitungs-URL

Um sicherzustellen, dass Ihr Inhalt immer verfügbar ist, können Sie eine Seitenregel mit der Einstellung **Weiterleitungs-URL** erstellen, die verwendet werden soll, wenn Ihre Site nicht verfügbar ist. 

 **Hinweis:** Wenn Sie eine **Weiterleitungs-URL** aktivieren, werden alle anderen Einstellungen inaktiviert, weil Sie den gesamten Datenverkehr an eine andere URL senden. 

### Aktivierung einer 'Weiterleitungs-URL'

 * Wählen Sie im Navigationsmenü unter 'Leistung' das Element 'Seitenregeln' aus. 
 * Erstellen Sie eine Seitenregel mit dem URL-Muster, das Ihre Domäne referenziert. 
 * Fügen Sie die Einstellung **Weiterleitungs-URL** hinzu. 
 * Wählen Sie den Weiterleitungstyp aus und geben Sie die Ziel-URL ein. 
 * Wählen Sie 'Ressource bereitstellen' aus. 

### Beispiele für die Weiterleitung: 

Angenommen, Sie möchten es allen potenziellen Besuchern leicht machen, eine URL wie die folgende zu erreichen: 

    *www.beispiel.com/+

    *beispiel.com/+

Dieses Muster passt: 

    http://beispiel.com/+
    http://www.beispiel.com/+
    https://www.beispiel.com/+
    https://blog.beispiel.com/+
    https://www.blog.beispiel.com/+
    usw.

Dieses Muster passt nicht: 

    http://www.beispiel.com/blog/+  [zusätzliches Verzeichnis vor dem +]
    http://www.beispiel.com+  [kein abschließender Schrägstrich]


Nachdem Sie das passende Muster erstellt haben, fügen Sie die Einstellung **Weiterleitungs-URL** hinzu, wählen Sie den Weiterleitungstyp aus und geben Sie die Ziel-URL ein. Beispiel: 

    https://plus.google.com/yourid

Wählen Sie 'Ressource bereitstellen' aus. Innerhalb von wenigen Sekunden werden alle Anforderungen, die mit dem Muster übereinstimmen, an die neue URL mit der angegebenen Umleitung weitergeleitet. 

### Erweiterte Weiterleitungsoptionen:

Wenn Sie eine grundlegende Umleitung verwenden, z. B. die Weiterleitung der Rootdomäne an 'www.yourdomain.com', verlieren Sie alle anderen Informationen in der URL. Sie könnten das Muster wie folgt definieren: 

    beispiel.com

Und eine Weiterleitung hierhin einrichten: 

    http://www.beispiel.com

Aber wenn dann jemand Folgendes eingibt: 

    beispiel.com/eine-bestimmte-Seite.html

Wird er hierhin weitergeleitet: 

    www.beispiel.com

Und nicht hierhin: 

    www.beispiel.com/eine-bestimmte-Seite.html

Die Lösung besteht darin, Variablen zu verwenden. Jedes Platzhalterzeichen entspricht einer Variablen, die in der Weiterleitungsadresse referenziert werden kann. Die Variablen werden als `$`-Zeichen, gefolgt von einer Zahl, dargestellt. Um das erste Platzhalterzeichen zu referenzieren, geben Sie `$1` an, um das zweite Platzhalterzeichen zu referenzieren, geben Sie `$2` an usw. Die Weiterleitung vom Rootelement zu `www` im vorherigen Beispiel können Sie auf dieselbe Weise korrigieren: 

    beispiel.com/*

Anschließend richten Sie die folgende URL ein, an die der Datenverkehr weitergeleitet werden soll: 

    http://www.beispiel.com/$1

Wenn jetzt jemand die folgende URL aufruft: 

    beispiel.com/eine-bestimmte-Seite.html

Wird er hierhin weitergeleitet: 

    http://www.beispiel.com/eine-bestimmte-Seite.html
