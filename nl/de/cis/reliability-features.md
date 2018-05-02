---
copyright:
  years: 2018
lastupdated: "2018-03-06"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Informationen zur Zuverlässigkeit mit IBM Cloud Internet Services (CIS)

IBM Cloud Internet Services (CIS) verbessern die Zuverlässigkeit Ihrer Web-Services und Anwendungen, weil sie Ausfallzeiten aufgrund von Anwendungs- und Infrastrukturausfällen verhindern. Mit globalen Lastausgleichsfunktionen können Sie beispielsweise Ihre Web-Services und Anwendungen in mehreren Regionen bereitstellen. IBM CIS leitet Ihre Kundenanforderungen an die nächstgelegenen verfügbaren Regionen weiter, wenn ein globaler Lastausgleich aktiviert ist. Falls eine Region ausfällt, werden die Anforderungen an den nächstgelegenen Standort weitergeleitet, damit Ihre Kunden von der Ausfallzeit nicht betroffen sind. Wenn Ihre Website oder API fehlschlägt, sendet IBM CIS Ihnen automatisch Benachrichtigungen, ebenso wenn die Wiederherstellung erfolgreich war. 


![Zuverlässigkeitsgrafik.png](images/reliability-graphic.png)

Dies sind die wichtigsten Merkmale kurz zusammengefasst: 

## Zuverlässigkeitsmerkmale

 * Globaler Serverlastausgleich 
 * Proxy- und Nicht-Proxy-Optionen für den Lastausgleich
 * Ursprungspools und Statusüberwachungen
 * DNS-Verwaltung
 
### Zusammenfassung
 
  * Statusüberwachungen prüfen, ob Ihre Ursprungspools in einwandfreiem Zustand sind. 
  * Falls die Statusüberwachung Fehler feststellt, werden Ihre Anforderungen an Ursprünge in einwandfreiem Zustand weitergeleitet. 
  * Sie werden informiert, wenn Ihr Web-Service oder Ihre API fehlschlagen und wenn sie wiederhergestellt wurden. 
