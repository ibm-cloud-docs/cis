---
copyright:
  years: 2018
lastupdated: "2018-03-16"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# DDoS-Angriffskonzepte (Distributed Denial of Service)

DDoS-Angriffe zählen zu den gängigsten Arten von Internetangriffen, die Ihre Website oder Ihren Host treffen können. 

## Was ist ein DDoS-Angriff?
Ein DDoS-Angriff ist ein böswilliger Versuch, den normalen Datenverkehr eines Servers, Service oder Netzes zu unterbrechen, indem das Ziel oder die umgebende Infrastruktur mit einer Flut von Internetdatenverkehr überlastet wird. DDoS-Angriffe sind sehr effektiv, indem sie viele beeinträchtigte Computersysteme als Quellen für den Angriffsdatenverkehr nutzen. Solchermaßen zweckentfremdete Systeme können Computer oder andere Netzressourcen wie IoT-Geräte (Internet of Things, Internet der Dinge) sein. Übergeordnet betrachtet ähnelt ein DDoS-Angriff einem Verkehrsstau, der eine Autobahn blockiert und so verhindert, dass der reguläre Verkehr sein Ziel erreicht. 

## Wie funktioniert ein DDoS-Angriff?
Ein Angreifer gewinnt die Kontrolle über ein Netz von Onlinesystemen, um einen DDoS-Angriff zu starten. Computer und andere Systeme (wie IoT-Geräte) werden mit Malware infiziert und zu einem Bot (oder Zombie) umfunktioniert. Der Angreifer steuert die Gruppe von Bots, die als _Botnet_ bezeichnet wird.  

Nachdem das Botnet erstellt wurde, steuert der Angreifer die Systeme, indem er an die einzelnen Bots per Fernsteuerung aktualisierte Anweisungen übermittelt. Eine Ziel-IP-Adresse empfängt möglicherweise Anforderungen von einer Vielzahl von Bots, wodurch der Zielserver oder das Zielnetz überlastet wird. Dies führt zu einem Denial of Service, einer Dienstverweigerung, für den normalen Datenverkehr. Da die einzelnen Bots legitime Internetgeräte sind, kann es schwierig sein, den Angriffsdatenverkehr von normalem Datenverkehr zu unterscheiden.  

## Was sind gängige Typen von DDoS-Angriffen? 
DDoS-Angriffsvektoren zielen auf unterschiedliche Komponenten einer Netzverbindung ab. Zwar haben beinahe alle DDoS-Angriffe die Überlastung eines Zielgeräts oder Zielnetzes zum Ziel, sie lassen sich aber in drei Kategorien unterteilen. Ein Angreifer kann einen oder mehrere Angriffsvektoren verwenden und er kann diese Angriffsvektoren sogar abwechselnd einsetzen, abhängig davon, welche Gegenmaßnahmen die angegriffene Partei ergreift. 

Gängige Typen sind: 

 * Angriffe auf die Anwendungsschicht (Layer 7)
 * Protokollangriffe (Layer 3 und 4)
 * Volumetrische Angriffe (Verstärkungsangriffe)

###	Angriffe auf die Anwendungsschicht
Ein Angriff auf die Anwendungsschicht wird manchmal auch als _Layer-7-DDoS-Angriff_ bezeichnet (in Bezug auf die 7. Schicht des OSI-Modells). Das Ziel dieser Angriffe ist, die Ressourcen des Opfers vollständig zu erschöpfen, indem die Schicht angesprochen wird, auf der Webseiten auf dem Server generiert und Besuchern als Antwort auf HTTP-Anforderungen bereitgestellt werden (die Anwendungsschicht). Layer-7-Angriffe sind eine Herausforderung, weil sich der Datenverkehr nur schwer als böswillig identifizieren lässt. 

###	Protokollattacken
Protokollattacken nutzen Schwachstellen in Schicht 3 und Schicht 4 des ISO-Protokollstacks aus, um das Ziel unzugänglich zu machen. Diese Angriffe, die auch als State-Exhaustion-Angriffe bezeichnet werden, verursachen eine Serviceunterbrechung, indem sie die gesamte verfügbare Kapazität der _Statustabellen_ von Webanwendungsservern oder von zwischengeschalteten Ressourcen wie Firewalls und Lastausgleichsfunktionen in Anspruch nehmen.  
  
###	Volumetrische Angriffe
Diese Kategorie von Angriffen versucht, eine Überlastung zu erzeugen, indem die gesamte verfügbare Bandbreite zwischen dem Ziel und dem Internet belegt wird. Große Datenmengen werden unter Ausnutzung des sogenannten Verstärkungsfaktors an ein Ziel gesendet. Oder es werden andere Mittel zur Erzeugung eines massiven Datenverkehrs eingesetzt, wie z. B. Anforderungen von einem Botnet.  


## Was kann ich tun, wenn ich Ziel eines DDoS-Angriffs bin?

**Schritt 1:** Aktivieren Sie in der Anzeige **Übersicht** den 'Verteidigungsmodus'.  

![Verteidigungsmodus](images/defense-mode.png)

**Schritt 2:** Legen Sie für Ihre DNS-Datensätze maximale Sicherheit fest. 

**Schritt 3:** Drosseln Sie die Anforderungen von IBM CIS nicht, wir benötigen eine möglichst große Bandbreite, um Sie in Ihrer Situation zu unterstützen. 

**Schritt 4:** Blockieren Sie ggf. bestimmte Länder und Besucher. 
