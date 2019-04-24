---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: origin pools, application resources, Origin Pools section

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Anwendungsressourcen angeben
{:#identify-your-application-resources}

 Geben Sie Ihre Anwendungsressourcen wie Ursprungspools und Mechanismen zur Statusprüfung an. 
 
1. Navigieren Sie zum Abschnitt **Ursprungspools** und klicken Sie auf **Pool erstellen**, um einen neuen Ursprungspool zu definieren.  

   Ursprungspools sind Serverressourcen, die Anwendungen für Ihre Kunden bereitstellen. 
   
2. Ordnen Sie einen Namen zu Ihrem Ursprungspool hinzu und wählen Sie den Mechanismus für die Statusprüfung aus, der zuvor definiert wurde. Fügen Sie Ihren Anwendungsserver als Ihren Ursprung hinzu. Sie können einen oder mehrere Ursprünge hinzufügen, indem Sie auf **Ursprung hinzufügen** klicken. 

   Wenn Ihre Anwendungsserver sich hinter einer lokalen Lastausgleichsfunktion wie IBM Cloud Load Balancer befinden, dann fügen Sie den FQDN der Lastausgleichsfunktion oder die virtuelle IP als Ihren Ursprung hinzu, anstatt Ihre einzelnen Server hinzuzufügen. {:note}
   
3. Klicken Sie auf **Ressource bereitstellen**, um die Erstellung Ihres Ursprungspools abzuschließen.   

   <img src="images/reliability8.png" alt="Zeichnung" style="width: 300px;"/>
   
   Der Ursprungspool wird anfänglich als **Fehlerhaft** dargestellt. Sein Status ändert sich in **In einwandfreiem Zustand**, nachdem eine erfolgreiche Statusprüfung durch das System erfolgt ist. Sie müssen möglicherweise Ihren Browser aktualisieren, damit die Statusänderung sichtbar wird.  
   
   <img src="images/reliability9.png" alt="Zeichnung" style="width: 300px;"/>
   
   Wenn Sie über mehrere Ursprünge innerhalb Ihres Ursprungspools verfügen, dann verwenden Sie den Schwellenwert für den Ursprung in einwandfreiem Zustand, um die Mindestanzahl der Ursprünge anzugeben, die in einwandfreiem Zustand sein müssen, bevor für den Pool angegeben werden kann, dass er sich in einwandfreiem Zustand befindet. {:note}
   
4. Definieren Sie so viele Ursprungspools, dass ihre Anzahl der Anzahl der Anwendungsfarmen entspricht. Diese Farmen können sich innerhalb derselben oder in verschiedenen geografischen Regionen befinden. In unserem Beispiel erstellen wir zwei Ursprungspools, die eine Anwendungsfarm an der Westküste der USA und eine Anwendungsfarm an der Ostküste der USA darstellen.  

   <img src="images/reliability10.png" alt="Zeichnung" style="width: 300px;"/>
