---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Page Rule Use, Cache-Tag Purge, web content

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Verwalten Ihrer IBM CIS-Bereitstellung für eine optimale Leistung
{:#manage-your-cis-deployment-for-best-performance}

IBM Cloud Internet Services (CIS) bietet Ihren Kunden eine besonders schnelle Benutzererfahrung, weil es Ihre Images optimiert und Ihre Webinhalte möglichst nahe am Endbenutzer speichert. Ihre Inhalte werden von Proxy-Edge-Servern geladen (wodurch die Latenzzeit reduziert wird).

Mit IBM CIS können Sie die Leistung Ihrer Website weiter verbessern, indem Sie Best Practices einsetzen, die das Laden von Webinhalten beschleunigen. Im Folgenden finden Sie einige spezifische Best Practices für die Verbesserung der Leistung Ihrer Webinhalte in CIS.

**Empfehlungen und Best Practices:**

 * Stellen Sie einen möglichst großen Teil Ihrer statischen und halbstatischen Webinhalte in den Zwischenspeicher.
 * Löschen Sie für ereignisgesteuerte Inhalte Ihren Cache mithilfe der API.
 
## Best Practice 1: Einen möglichst großen Teil Ihrer statischen und halbstatischen Inhalte in den Zwischenspeicher stellen
{:#best-practice-cache-static-content}

  * Aktivieren Sie für statische HTML-Webseiten die Option **Alles zwischenspeichern**.
  * Legen Sie für Inhalte, die sich nur gelegentlich ändern, eine konservative **TTL** (Time-to-Live, Lebensdauer) fest.

### Konservative Lebensdauer (TTL) für Inhalte, die sich nur gelegentlich ändern
{:#utilize-conservative-ttl}

Wenn sich Inhalte nur gelegentlich ändern, können Sie eine konservative Lebensdauer festlegen, um den Cache optimal zu nutzen. Bei einem hohen Prozentsatz an Neuvalidierungsanforderungen können Sie die Lebensdauer Ihrer Inhalte erhöhen, ohne dass sich dies negativ auf Ihre Kunden auswirkt. Indem Sie den Cache effektiver nutzen, verbessern Sie die Leistung, weil seltener Neuvalidierungen durchgeführt werden müssen.

### Woran kann ich erkennen, dass Elemente zwischengespeichert werden?
{:#how-do-i-tell-if-items-are-being-cached}

IBM CIS fügt den Antwortheader `CF-Cache-Status` hinzu, wenn versucht wird, ein Objekt zwischenzuspeichern. Falls das Caching erfolgreich ist, gibt der Wert dieses Headers den Status mit einem der folgenden Schlüsselworte an:

* **MISS:** Das Asset war noch nicht im Cache oder die Lebensdauer (TTL) war abgelaufen (d. h. die maximale Gültigkeitsdauer (cache-control) von '0' wurde erreicht).
* **HIT:** Das Asset wurde aus dem Cache bereitgestellt.
* **EXPIRED:** Dieses Asset wurde aus dem Cache bereitgestellt, aber die nächste Anforderung erfordert eine Neuvalidierung.
* **REVALIDATED:** Das Asset wurde aus dem Cache bereitgestellt. Die Lebensdauer (TTL) war abgelaufen, aber eine Anforderung `If-Modified-Since` an den Ursprung hat festgestellt, dass sich das Asset nicht geändert hat. Aus diesem Grund wird die Version im Cache wieder als gültig betrachtet.

## Best Practice 2: Für ereignisgesteuerte Inhalte den Cache mithilfe der API löschen
{:#best-practice-api-purge-cache}

Beispiel: Jedes Mal, wenn in Ihrem Blog ein neuer Beitrag hinzugefügt wird, können Sie den CIS-Cache einfach mithilfe eines API-Befehls löschen. Es ist üblich, ereignisgesteuerte Inhalte anzuzeigen, und wir machen es Ihnen einfach, dass Ihren Benutzern keine veralteten Inhalte bereitgestellt werden. Im Folgenden führen wir die Befehle zum sofortigen Löschen des Cache in unserem gesamten globalen Netz auf. Sie können unsere Caching-Anwendung oder die API verwenden.

  * Löschen des Cache mithilfe eines Cache-Tags
  * Globales Löschen des Cache
  * Löschen des Cache anhand von Seitenregeln
  * Verwenden erweiterter Caching-Funktionen

### Löschen des Cache mithilfe eines Cache-Tags
{:#purge-cache-by-cache-tag}

Mit Cache-Tags können Sie Gruppen von Inhalten definieren, die Sie löschen möchten. Es ist eine hervorragende Methode, Objekte zu kombinieren, die üblicherweise gleichzeitig geändert werden. Beispielsweise können ein HTML-Blogbeitrag und alle zugehörigen Bildinhalte mit demselben Tag versehen werden. Rein mobile Inhalte können auch mithilfe von Cache-Tags gebündelt werden, damit Sie alles löschen können, wenn Sie eine Aktualisierung in Ihrer mobilen Domäne vornehmen.

### Globales Löschen des Cache
{:#purge-cache-globally}

Sie haben auch die Möglichkeit, eine Neuvalidierung für den gesamten Cache zu erzwingen. Sie können alle im Cache gespeicherten Objekte zurücksetzen, sodass jede Anforderung an den Ursprungsserver weitergeleitet wird.

### Löschen des Cache anhand von Seitenregeln
{:#purge-cache-by-page-rule}

Mit Seitenregeln können Sie den gesamten Cache basierend auf einem regulären Ausdruck löschen. Sie können eine vordefinierte Seitenregel verwenden und alle Treffer für diese Seitenregel neuvalidieren. Sie können bis zu 50 Seitenregeln pro Seite erstellen.

### Verwenden erweiterter Caching-Funktionen
{:#use-advanced-caching-features}

**Cacheumgehung bei Cookie:** Wenn Sie diese Funktion in einer Seitenregel konfigurieren, können Sie ein zwischengespeichertes Objekt bereitstellen, es sei denn, es wird ein Cookie mit einem bestimmten Namen gefunden. Beispielsweise wird eine zwischengespeicherte Version der Homepage bereitgestellt, es sei denn, ein Cookie `SessionID` ist vorhanden, das angibt, dass der Kunde angemeldet ist und ihm deshalb personalisierter Inhalt angezeigt werden soll.
