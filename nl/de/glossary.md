---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Glossary, load balancer, pool, health check

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Glossar
{:#glossary}

Dieses Glossar enthält Definitionen für allgemeine Begriffe, die bei der Arbeit mit Global Load Balancer (GLB) vorkommen können.

## Lastausgleichsfunktion
{:#glossary-load-balancer}

Eine Lastausgleichsfunktion ist eine Einheit, die als Reverse Proxy agiert und den Netz- oder Anwendungsdatenverkehr über mehrere Server verteilt. Lastausgleichsfunktionen werden verwendet, um die Systemkapazität (die Anzahl der gleichzeitig angemeldeten Benutzer) zu erhöhen und die Zuverlässigkeit von Anwendungen zu verbessern.

## Pool
{:#glossary-pool}

Ein Pool ist eine Gruppe von Ursprungsservern, an die der Datenverkehr intelligent weitergeleitet wird, wenn sie mit einer globalen Lastausgleichsfunktion verknüpft sind. Die Mindestanzahl der verfügbaren Ursprungsserver für den Pool, die als einwandfrei markiert werden müssen, kann vom Benutzer zusammen mit der zu verwendenden spezifischen Statusprüfung konfiguriert werden. Der Ursprungspool kann einer bestimmten Region zugeordnet sein oder er kann für alle Regionen verfügbar gemacht werden.

## Statusprüfung
{:#glossary-health-check}

Eine Statusprüfung hilft Ihnen dabei, Einblick in die Verfügbarkeit von Pools zu erhalten, damit der Datenverkehr an die Pools in einwandfreiem Zustand weitergeleitet werden kann. Diese Prüfungen senden regelmäßig HTTP/HTTPS-Anforderungen und überwachen die Antworten. Sie können mit angepassten Intervallen, Zeitlimits, Statuscodes und mehr konfiguriert werden. Sobald ein Pool als fehlerhaft markiert ist, wird der Verkehr auf intelligente Weise zu einen anderen verfügbaren Pool weitergeleitet, falls ein solcher verfügbar ist.

## Ursprungsserver
{:#glossary-origin-servers}

Ein Ursprungsserver verarbeitet eingehende Anforderungen von Clients und antwortet auf diese Anforderungen. Er wird in der Regel mit Caching-Servern verwendet. Ursprungsserver führen ein oder mehrere Programme aus, die zum Überwachen und Verarbeiten eingehender Internet-Anforderungen konzipiert sind. Der physische Abstand zwischen dem Ursprungsserver und dem Client, der eine Anforderung stellt, erhöht die Latenzzeit der Verbindung und damit die Ladezeit. Durch die Verwendung von Caching-Servern wird diese Latenzzeit reduziert.


