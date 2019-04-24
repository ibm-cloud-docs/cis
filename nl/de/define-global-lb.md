---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: global load balancer, global load balancer configuration

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Globale Lastausgleichsfunktion definieren
{:#define-the-global-load-balancer}

Definieren Sie Ihre Konfiguration des globalen Lastausgleichs durch Angabe des Hostnamens und Hinzufügen und Anpassen Ihrer Ursprungspools und Definition weiterer Regeln, um zu steuern, wie der Datenverkehr an die Clients gesendet wird. 

1. Erstellen Sie Ihre globale Lastausgleichsfunktion durch Klicken auf die Schaltfläche 'Lastausgleichsfunktion erstellen' rechts.   

2. Geben Sie den Hostnamen für Ihre Domäne an, passen Sie den TTL-Wert (Lebensdauer) bei Bedarf an (der Standardwert beträgt 60 Sekunden) und verwenden Sie **Pool hinzufügen**, um Ihre Ursprungspools hinzuzufügen.  

   <img src="images/reliability11.png" alt="Zeichnung" style="width: 300px;"/>
   
   **HINWEIS:** Hostnamen in Kombination mit Domänennamen bilden vollständig qualifizierte Domänennamen (FQDN) für Ihre Anwendung. Ihre Endbenutzer stellen über diesen FQDN eine Verbindung zu Ihrer Anwendung her. 
   
3. Passen Sie die relativen Prioritäten Ihrer Ursprungspools durch Klicken auf die Aufwärts- und Abwärtspfeile links vom Pools an. Die Anwendungsanforderungen von Endbenutzern werden im Umlaufverfahren von diesen Ursprungspools bedient.  
   
   <img src="images/reliability12.png" alt="Zeichnung" style="width: 300px;"/>   
   
4. Optional können Sie weitere Regeln definieren, um zu steuern, wie Datenverkehr für Clients aus verschiedenen geografischen Regionen zur Verfügung gestellt wird. Im folgenden Beispiel werden Kunden aus dem südlichen Südamerika an den Ursprungspool an der Westküste der USA weitergeleitet. Sie können diese Regeln verwenden, um Kunden in die nächstgelegene Region weiterzuleiten. Wenn eine dieser Regionen ausfällt, werden die Anforderungen an andere verfügbare Standorte in einwandfreiem Zustand weitergeleitet, sodass die Endbenutzer nicht von der Ausfallzeit betroffen sind.  

   <img src="images/reliability13.png" alt="Zeichnung" style="width: 300px;"/>   
   
5. Klicken Sie auf **Ressourcen bereitstellen**, um die Konfiguration Ihrer globalen Lastausgleichsfunktion abzuschließen.  
6. Überprüfen Sie schließlich die Konnektivität Ihrer Anwendung durch Eingabe von `FQDN URL` in einem mobilen Browserfenster. Wenn Sie eine Verbindung herstellen können, wird eine Willkommensnachricht angezeigt.
