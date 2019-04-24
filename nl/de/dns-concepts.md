---

copyright:
  years: 2018
lastupdated: "2018-03-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}


# DNS-Konzepte

In diesem Dokument finden Sie Konzepte und Definitionen im Zusammenhang mit dem DNS (Domain Name System) des Internets und wie sich dies auf Ihre IBM CIS-Bereitstellung (Cloud Internet Services) auswirkt.  

Das Domain Name System (DNS) unterstützt das Internet, das wir täglich nutzen. Es arbeitet transparent im Hintergrund, wo es lesbare Websitenamen in für Computer lesbare, numerische IP-Adressen konvertiert, die den [RFC 1918-Richtlinien für IPv4 und den RFC 4193-Richtlinien für IPv6](https://en.wikipedia.org/wiki/Private_network) folgen. Kurz, DNS-Server ordnen Domänennamen wie 'ibm.com' ihren entsprechenden IP-Adressen zu, die die meisten Benutzer nicht kennen müssen. 

Das DNS-System sucht nach diesen IP-Adress- und Hostnameninformationen in einem Netz von verlinkten DNS-Servern im Internet, ganz ähnlich wie Menschen nach bestimmten Orten im Telefonbuch oder auf einer Karte suchen. 

## Namensserver
Ein **Namensserver** implementiert Services, die Antworten auf Abfragen an einen Verzeichnisservice bereitstellen. Er übersetzt aussagekräftige, textbasierte Web- oder Host-IDs in IP-Adressen. 

Die **Namensserverdelegierung** findet statt, wenn ein Namensserver für eine Domäne eine Anforderung nach den Datensätzen einer Unterdomäne empfängt und mit der Referenz des Namensservers zum delegierten Server antwortet. Diese Funktionalität ermöglicht es, die Verwaltung einer großen Domäne (wie `ibm.com`) zu dezentralisieren. 

Ein **benutzerdefinierter Domänennamensserver** ermöglicht es Ihnen, die Server des DNS-Anbieters mit dem benutzerdefinierten Referenznamen Ihrer eigenen Domäne zu nutzen. Sie können beispielsweise Ihren Namensserver als `ns1.cloud.ibm.com` anstelle von `ns1.acme.com` angeben. 

## Secure DNS

**DNSSec** ist eine Technologie zum digitalen Signieren von DNS-Daten, sodass Sie sicher sein können, dass diese gültig sind. Um mögliche Internetsicherheitslücken zu eliminieren, muss 'DNSSec' in jedem Schritt des Suchvorgangs implementiert sein, von der Rootzone bis hin zum finalen Domänennamen (z. B. www.icann.org). 
