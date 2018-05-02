---

copyright:
  years: 2018
lastupdated: "2018-03-05"

---

# Konzepte für globale Laustausgleichsfunktionenn (Global Load Balancer, GLB) 

In diesem Dokument finden Sie Konzepte und Definitionen im Zusammenhang mit globalen Lastausgleichsfunktionen und wie diese sich auf Ihre IBM CIS-Bereitstellung auswirken. 

## Globale Lastausgleichsfunktion

Globale Lastausgleichsfunktionen verwalten Datenverkehr über Serverressourcen in mehreren Regionen hinweg. Sie nutzen einen Pool, um den Datenverkehr an mehrere Ursprünge zu verteilen. Dies birgt viele Vorteile, darunter die folgenden: 

  * Kürzere Antwortzeiten
  * Höhere Verfügbarkeit durch Redundanz
  * Maximaler Datenverkehrsdurchsatz

## Pool

Ein Pool ist eine Gruppe von Ursprungsservern, an die der Datenverkehr intelligent weitergeleitet wird, wenn sie mit einer globalen Lastausgleichsfunktion verknüpft sind. Die Mindestanzahl der verfügbaren Ursprungsserver für den Pool, die als einwandfrei markiert werden müssen, kann vom Benutzer zusammen mit der zu verwendenden spezifischen Statusprüfung konfiguriert werden. Der Ursprungspool kann einer bestimmten Region zugeordnet sein oder er kann für alle Regionen verfügbar gemacht werden. 

## Statusprüfung

Eine Statusprüfung hilft Ihnen dabei, Einblick in die Verfügbarkeit von Pools zu erhalten, damit der Datenverkehr an die Pools in einwandfreiem Zustand weitergeleitet werden kann. Diese Prüfungen senden regelmäßig HTTP/HTTPS-Anforderungen und überwachen die Antworten. Sie können mit angepassten Intervallen, Zeitlimits, Statuscodes und mehr konfiguriert werden. Sobald ein Pool als fehlerhaft markiert ist, wird der Verkehr auf intelligente Weise zu einen anderen verfügbaren Pool weitergeleitet, falls ein solcher verfügbar ist. 
