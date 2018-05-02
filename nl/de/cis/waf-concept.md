---
copyright:
  years: 2018
lastupdated: "2018-03-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Web Application Firewall-Konzepte - Fragen & Antworten

Die Web Application Firewall (WAF) schützt vor ISO-Layer-7-Angriffen, die sehr heikel sein können. Im Folgenden erhalten Sie genauere Angaben. 

## Was ist eine Web Application Firewall (WAF)?
Eine WAF oder Web Application Firewall verbessert den Schutz von Webanwendungen durch das Filtern und Überwachen des HTTP-Datenverkehrs zwischen einer Webanwendung und dem Internet. Eine WAF ist ein ISO-Protokoll-Layer-7-Schutz (im [OSI-Modell ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://en.wikipedia.org/wiki/OSI_model)). Sie ist nicht dafür konzipiert, alle Typen von Angriffen abzuwehren.  

Die Implementierung einer WAF vor einer Webanwendung entspricht dem Platzieren eines Schilds zwischen der Webanwendung und dem Internet. Ein Proxy-Server schützt die Identität eines Clientsystems mithilfe eines Intermediärs (für abgehenden Datenverkehr), aber eine WAF ist eine Art Reverse Proxy, die den Server vor Gefahren schützt, indem der Datenverkehr des Clients die WAF passiert, bevor er den Server erreicht (für eingehenden Datenverkehr). 

## Welche Typen von Angriffen kann eine WAF verhindern?
Eine WAF schützt Webanwendungen typischerweise vor Angriffen wie Cross-Site Forgery, Cross-Site Scripting (XSS), Dateieinschluss und SQL-Injection. Normalerweise ist eine WAF Teil einer Suite von Tools, die gemeinsam einen umfassenden Schutz vor einer Reihe von Angriffsvektoren bieten. 

## Wie funktioniert eine WAF?

Eine WAF wird mithilfe einer Reihe von Regeln ausgeführt, die oft als Richtlinien bezeichnet werden. Diese Richtlinien sollen vor Sicherheitslücken in den Anwendungen schützen, indem sie böswilligen Datenverkehr herausfiltern.  

Der Nutzen einer WAF ergibt sich aus der Geschwindigkeit und einfachen Durchführbarkeit, mit der die Richtlinienänderungen implementiert werden können, wodurch eine schnellere Antwort auf verschiedenste Angriffsvektoren möglich wird. Beispielsweise kann während eines [DDoS-Angriffs ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://en.wikipedia.org/wiki/Denial-of-service_attack) durch eine Änderung der WAF-Richtlinien eine Drosselung des Datenverkehrs erzielt werden. 
