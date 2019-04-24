---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: global load balancer configuration, glb configuration

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}

# Konfiguration für globale Lastausgleichsfunktion starten
{:#begin-global-load-balancer-configuration}

Beginnen Sie mit der Konfiguration Ihrer globalen Lastausgleichsfunktion. 

1. Wählen Sie im Abschnitt **Zuverlässigkeit** die Option **Globale Lastausgleichsfunktion** aus. 
    
    <img src="images/reliability6.png" alt="Zeichnung" style="width: 300px;"/>

2. Blättern Sie zum Abschnitt mit den Statusprüfungen.  

   Diese Konfiguration ist optional. Wenn Sie keine angepassten Statusprüfungen definieren, verwendet das System “/” als Standardpfad für die Statusprüfung. {:note}

3. Klicken Sie auf die Schaltfläche **Statusprüfung erstellen**, um eine angepasste Statusprüfung zu definieren.    

   Stellen Sie den gewünschten Pfad zur Verfügung, auf dem Ihre Statusprüfung ausgeführt werden soll. Sie können entweder HTTP- oder HTTPS-Protokolle für Ihre Statusprüfungen verwenden.  
   
4. Unter **Erweiterte Optionen** können Sie andere Parameter wie das Intervall der Statusprüfung, die Anzahl der Wiederholungen, die Anforderungsmethode und den Antworthauptteil in den erweiterten Optionen anpassen.  
   
   <img src="images/reliability7.png" alt="Zeichnung" style="width: 300px;"/>
   
5. Klicken Sie auf **Ressource bereitstellen**, um die Konfiguration Ihrer Statusprüfung abzuschließen.  
