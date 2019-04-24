---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain Input information, IBM Cloud Internet Services, Global Load balancing

subcollection: cis

---


{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Anwendungszuverlässigkeit und Skalierbarkeit mit dem globalen Lastausgleich von IBM Cloud Internet Services verbessern
{:#improving-application-reliability-and-scalability-with-global-load-balancing-from-ibm-cloud-internet-services}

Wenn Sie über eine E-Commerce-Site verfügen oder eine Anwendung hosten, die für Ihre Endbenutzer jederzeit zugänglich sein muss, dann ist die ständige Verfügbarkeit (24*7) und Leistungsfähigkeit Ihrer Anwendung ein wichtiger Aspekt für Sie.  

Die globale Lastausgleichsfunktion, die mit IBM Cloud Internet Services (CIS) zur Verfügung steht, unterstützt Sie bei der Verbesserung der Zuverlässigkeit und Skalierbarkeit während sie gleichzeitig die bestmögliche Endbenutzerfunktionalität bietet. Dieser Leitfaden spielt die Konfiguration des globalen Lastausgleichs beispielhaft durch.   

## Aufgaben, die Sie ausführen werden
{:#what-you-accomplish}

In dieser Schritt-für-Schritt-Anleitung erfahren Sie, wie Sie eine ähnliche Einrichtung wie unten dargestellt konfigurieren können. 

<img src="images/reliability1.png" alt="Zeichnung" style="width: 300px;"/>

In diesem Beispiel werden die Anwendungsressourcen in zwei Rechenzentren implementiert, wobei sich eines an der Westküste und eines an der Ostküste der USA befindet. Die Endnutzer können auf diese Anwendung von einem beliebigen Standort auf der ganzen Welt zugreifen. 

Task  |  Beschreibung
------------- | -------------
[CIS-Instanz erstellen](/docs/infrastructure/cis?topic=cis-create-your-ibm-cloud-internet-services-cis-instance) | Beginnen Sie mit dem Erstellen Ihrer CIS-Instanz (CIS, IBM Cloud Internet Services), indem Sie das IBM Customer Portal verwenden.|
[Eingabeinformationen zu Ihrer Domäne](/docs/infrastructure/cis?topic=cis-input-information-about-your-domain) | Geben Sie Informationen zu der Domäne ein, die Sie schützen wollen und für die Sie den globalen Lastausgleich bereitstellen möchten. 
[Mit der Konfiguration des globalen Lastausgleichs beginnen](/docs/infrastructure/cis?topic=cis-begin-global-load-balancer-configuration) |Beginnen Sie mit der Konfiguration Ihrer globalen Lastausgleichsfunktion. 
[Ihre Anwendungsressource angeben](/docs/infrastructure/cis?topic=cis-identify-your-application-resources) | Geben Sie Ihre Anwendungsressourcen wie Ursprungspools und Mechanismen zur Statusprüfung an. 
[Globale Lastausgleichsfunktion definieren](/docs/infrastructure/cis?topic=cis-define-the-global-load-balancer) | Definieren Sie Ihre Konfiguration des globalen Lastausgleichs durch Angabe des Hostnamens und Hinzufügen und Anpassen Ihrer Ursprungspools und Definition weiterer Regeln, um zu steuern, wie der Datenverkehr an die Clients gesendet wird. 
