---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Advisory, Use of Caching, content caching, Cache-Control header

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# HIPAA-Empfehlung
{:#hipaa-advisory}

Die Verwendung von Caching (CDN) für regulierte Daten (zum Beispiel PHI, ITAR) ist **verboten**. Alle regulierte Datenflüsse, die CIS verwenden, müssen auf **nicht zwischenspeichern** gesetzt werden.
{:important}

Es gibt mehrere Möglichkeiten, das Zwischenspeichern von Inhalten durch das CIS CDN zu verhindern. 
- Der Ursprungsserver kann **nicht zwischenspeichern** für regulären Inhalt im **Cache-Control**-Header festlegen. 
- Verwenden Sie die CIS-Seitenregeln, um das Caching für jeglichen Inhalt auf einem bestimmten Pfad zu inaktivieren, auch wenn der Ursprung nicht **nicht zwischenspeichern** im **Cache-Control**-Header sendet. 
