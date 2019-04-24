---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain Input information, IBM Cloud Internet Service, Domain Name

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Eingabeinformationen zu Ihrer Domäne
{:#input-information-about-your-domain}

 Geben Sie Informationen zu der Domäne ein, die Sie schützen wollen und für die Sie den globale Lastausgleich bereitstellen möchten. 

1. Klicken Sie auf der linken Seite in der Einführungsanzeige auf **Übersicht**. Geben Sie Ihren Domänenname (oder Unterdomänennamen) ein und klicken Sie auf **Domäne hinzufügen**. 
    
    <img src="images/reliability3.png" alt="Zeichnung" style="width: 300px;"/>
    
    Der IBM Cloud Internet Service ist kein DNS-Registrator. Daher muss diese Domäne (oder Unterdomäne) zuvor erstellt worden sein. {:note}

    Im Abschnitt zu den Servicedetails können Sie feststellen, dass die neu hinzugefügte Domäne zunächst in einem Wartestatus angezeigt wird.  

    <img src="images/reliability4.png" alt="Zeichnung" style="width: 300px;"/>    

2. Navigieren Sie zur Verwaltungsseite für Ihre Domäne mit dem entsprechenden DNS-Registrator und delegieren Sie Ihre Domäne/Unterdomäne in die IBM-Namensserver, indem Sie NS-Datensätze definieren. 

Sie müssen bis zu 24 Stunden warten, bis Ihre Informationen in der DNS-Datenbank repliziert werden. Sobald dies geschehen ist, ändert sich der Status Ihrer Domäne in 'Aktiv'.  

<img src="images/reliability5.png" alt="Zeichnung" style="width: 300px;"/>    
