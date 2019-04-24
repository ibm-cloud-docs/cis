---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM CIS deployment, query strings, HTML files

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Caching-Konzepte
{:#caching-concepts}

In diesem Dokument finden Sie Konzepte und Definitionen im Zusammenhang mit Caching und wie es sich auf Ihre IBM CIS-Bereitstellung auswirkt.

## Was ist Caching?
{:#what-is-caching}

Caching ist der Prozess des Speicherns von Dateien auf unseren Edge-Servern zum Zweck einer Verbesserung der Antwortzeit beim Bereitstellen dieser Dateien für Kunden. Indem die Dateien räumlich näher zum Kunden gespeichert werden, können wir die Zeit verringern, die erforderlich ist, um die Daten über das Netz zu streamen. Man spricht hier üblicherweise von der **Latenz**.

Zwischengespeicherte Dateien haben eine angegebene Verfallszeit, die **Lebensdauer** (Time-to-live, TTL), nach deren Ablauf sie aus dem Cache gelöscht werden. Es ist auch möglich, Dateien manuell aus dem Cache zu löschen. Nachdem die Dateien aus dem Cache entfernt wurden, kehrt CIS zum Ursprungsserver zurück, um Ihre Dateien erneut zu laden und den Cache mit den neuesten Versionen zu aktualisieren.

Eine fundiertere Erläuterung der Cacheeinstellungen und Ihrer Caching-Optionen finden Sie im [Lernprogramm 'Caching und Seitenregeln'](/docs/infrastructure/cis?topic=cis-use-page-rules-with-caching). 

### Welche Inhalte werden im Cache gespeichert?
{:#what-content-is-cached}

Standardmäßig speichern wir **statische Dateien** zwischen. Dazu zählen viele Typen von Bild- und Textdateien (Nicht-HTML-Dateien). Dies umfasst nur Dateien von Ihren Websites und keine Ressourcen anderer Anbieter von Social-Networking-Sites etc. Wir führen außerdem momentan kein Caching nach MIME-Typ durch. 

### Wie kann ich HTML in den Cache stellen? 
{:#how-do-i-cache-html}

Wir speichern standardmäßig keine HTML-Dateien im Cache, da wir sie nicht als statisch betrachten. Wenn statisches HTML klar von dynamischem HTML unterschieden werden kann, ist es möglich, HTML-Dateien [mithilfe der Seitenregelfunktion](/docs/infrastructure/cis?topic=cis-use-page-rules) in den Cache zu stellen.


## Sortieren der Abfragezeichenfolgen
{:#query-string-sorting}

**Nur Enterprise** CIS behandelt URLs mit Abfragezeichenfolgen in einer anderen Reihenfolge als Einzeldateien im Cache. Dies bedeutet, wenn ein Benutzer Folgendes anfragt:

`/video/123456?title=0&byline=0&portrait=0&color=987654`

und ein anderer Benutzer Folgendes anfragt: 

`/video/123456?byline=0&color=987654&portrait=0&title=0`

dass CIS wieder an den Ursprung zurückkehrt, auch wenn wir die Datei in unserem Cache haben. 

Durch das 'Sortieren der Abfragezeichenfolgen' werden Abfragezeichenfolgen sortiert, _bevor_ sie in unseren Cache gelangen, was zu einer höheren Cachetrefferrate führt. Aktivieren Sie das 'Sortieren der Abfragezeichenfolge' mit dem Schalter auf der Seite **Caching**.

## Nicht aktuellen Inhalt speichern
{:#serve-stale-content-caching}

Hält eine eingeschränkte Version der Website online, wenn der Server ausfällt. Auch wenn der Inhalt abgelaufen ist, fährt CIS damit fort, Benutzern Inhalte aus dem Cache bereitzustellen, wenn die Ursprungsserver offline sind. 
