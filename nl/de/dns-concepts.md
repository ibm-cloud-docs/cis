---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain name system, DNS servers, match domain names, DNS Concepts

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}


# DNS-Konzepte
{:#dns-concepts}

In diesem Dokument finden Sie Konzepte und Definitionen im Zusammenhang mit dem DNS (Domain Name System) des Internets und wie sich dies auf Ihre IBM CIS-Bereitstellung (Cloud Internet Services) auswirkt. 

Das Domain Name System (DNS) unterstützt das Internet, das wir täglich nutzen. Es arbeitet transparent im Hintergrund, wo es lesbare Websitenamen in für Computer lesbare, numerische IP-Adressen konvertiert, die den [RFC 1918-Richtlinien für IPv4 und den RFC 4193-Richtlinien für IPv6](https://en.wikipedia.org/wiki/Private_network) folgen. Kurz, DNS-Server ordnen Domänennamen wie `ibm.com` ihren entsprechenden IP-Adressen zu, die die meisten Benutzer nicht kennen müssen. 

Das DNS-System sucht nach diesen IP-Adress- und Hostnameninformationen in einem Netz von verlinkten DNS-Servern im Internet, ganz ähnlich wie Menschen nach bestimmten Angaben im Telefonbuch oder nach Orten auf einer Karte suchen.

## Namensserver
{:#dns-concepts-nameservers}

Ein **Namensserver** implementiert Services, die Antworten auf Abfragen an einen Verzeichnisservice bereitstellen. Er übersetzt aussagekräftige, textbasierte Web- oder Host-IDs in IP-Adressen.

Die **Namensserverdelegierung** findet statt, wenn ein Namensserver für eine Domäne eine Anforderung nach den Datensätzen einer Unterdomäne empfängt und mit der Referenz des Namensservers zum delegierten Server antwortet. Diese Funktionalität ermöglicht es, die Verwaltung einer großen Domäne (wie `ibm.com`) zu dezentralisieren.

Ein **benutzerdefinierter Domänennamensserver** ermöglicht es Ihnen, die Server des DNS-Anbieters mit dem benutzerdefinierten Referenznamen Ihrer eigenen Domäne zu nutzen. Sie können beispielsweise Ihren Namensserver als `ns1.cloud.ibm.com` anstelle von `ns1.acme.com` angeben.

## Secure DNS
{:#dns-concepts-secure-dns}

**DNSSec** ist eine Technologie zum digitalen Signieren von DNS-Daten, sodass Sie sicher sein können, dass diese gültig sind. Um mögliche Internetsicherheitslücken zu eliminieren, muss 'DNSSec' in jedem Schritt des Suchvorgangs implementiert sein, von der Rootzone bis hin zum finalen Domänennamen (z. B. www.icann.org). 

## CNAME-Vereinfachung für Rootdatensätze
{:#dns-concepts-root-record-cname-flattening}

IBM CIS unterstützt eine Funktion mit dem Namen "CNAME-Vereinfachung". Mit dieser Methode können Rootdatensätze die IETF-RFC-Einschränkung überwinden, die  besagt, dass ein Rootdatensatz, der ein CNAME ist, keine anderen Datensätze für diese Domäne haben kann. Maßgebliche CIS-Server überwinden diese Einschränkung durch Rückgabe der A-Datensätze, die dem CNAME-Ziel entsprechen, anstelle der Rückgabe des CNAME selbst, wodurch der CNAME wirksam verborgen wird. Diese Technik ermöglicht, dass andere Datensätze wie beispielsweise XM-Datensätze zur Domäne auch dann hinzugefügt werden können, wenn der Rootdatensatz ein CNAME ist. 

## Proxying für DNS-Datensätze
{:#dns-concepts-proxying-dns-records}

IBM CIS unterstützt die Möglichkeit des Umschaltens, je nachdem ob ein Datensatz weitergeleitet wird oder nicht. Wenn es sich um einen weitergeleiteten Datensatz handelt, bedeutet dies, dass der Datenverkehr direkt über IBM CIS erfolgt. Momentan können Datensätze der Typen **A**, **AAAA** oder **CNAME** weitergeleitet werden. 
