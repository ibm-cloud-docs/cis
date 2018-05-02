---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

# Caching-Konzepte

In diesem Dokument finden Sie Konzepte und Definitionen im Zusammenhang mit Caching und wie es sich auf Ihre IBM CIS-Bereitstellung auswirkt. 

## Was ist Caching?

Caching ist der Prozess des Speicherns von Dateien auf unseren Edge-Servern zum Zweck einer Verbesserung der Antwortzeit beim Bereitstellen dieser Dateien für Kunden. Indem die Dateien räumlich näher zum Kunden gespeichert werden, können wir die Zeit verringern, die erforderlich ist, um die Daten über das Netz zu streamen. Man spricht hier üblicherweise von der **Latenz**. 

Standardmäßig speichern wir **statische Dateien** zwischen. Dazu zählen viele Typen von Bild- und Textdateien (Nicht-HTML-Dateien). Wir speichern keine HTML-Dateien zwischen, weil wir sie nicht als statisch betrachten. Es ist jedoch möglich, HTML-Dateien [mithilfe von Seitenregeln](using-page-rules.html) zwischenzuspeichern. 

Zwischengespeicherte Dateien haben eine angegebene Verfallszeit, die **Lebensdauer** (Time-to-live, TTL), nach deren Ablauf sie aus dem Cache gelöscht werden. Es ist auch möglich, Dateien manuell aus dem Cache zu löschen. Nachdem die Dateien aus dem Cache entfernt wurden, kehrt CIS zum Ursprungsserver zurück, um Ihre Dateien erneut zu laden und den Cache mit den neuesten Versionen zu aktualisieren. 

Eine fundiertere Erläuterung der Cacheeinstellungen und Ihrer Caching-Optionen finden Sie im [Lernprogramm 'Caching und Seitenregeln'](caching-with-page-rules.html). 
