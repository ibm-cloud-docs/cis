---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Caching, IBM Cloud Internet Services, Web Application Firewall

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 

# Informationen zu IBM Cloud Internet Services (CIS)
{:#about-ibm-cloud-internet-services-cis}

IBM Cloud Internet Services (CIS), powered by Cloudflare, bietet einen schnellen, in höchstem Maße leistungsfähigen, zuverlässigen und sicheren Internet-Service für Kunden, die ihr Geschäft in IBM Cloud ausführen.    

IBM CIS erleichtert Ihnen den Einstieg, indem es schnell Standardwerte für Sie festlegt, die Sie problemlose über die API oder die Benutzerschnittstelle ändern können. Im Folgenden sind einige häufig geänderte Parameter aufgeführt:

 * **DNS-Einstellungen**: Sie können IBM CIS verwenden, um Ihr DNS zu hosten, oder Sie können CNAME-Datensätze erstellen.
 * **Verschlüsselungseinstellungen (TLS)**: Der Standardwert ist der `flexible` Modus, der die Verbindung zwischen Ihrem Host und dem IBM CIS-Edge-Server, aber nicht die Kommunikation zwischen dem IBM CIS-Edge-Server und dem Ursprungsserver verschlüsselt.

## Web Application Firewall (WAF)
{:#about-waf}

IBM CIS stellt eine Web Application Firewall-Funktionalität (WAF) bereit, die den Webdatenverkehr auf verdächtige Aktivitäten überprüft. Sie kann unzulässigen Datenverkehr automatisch - basierend auf Regelsätzen - herausfiltern, um GET- und POST-basierte Webanforderungen zu untersuchen. Sie können verschiedene Regelsätze verwenden, um zu bestimmen, welche Art von Datenverkehr blockiert, abgefragt oder übergeben werden soll. WAF kann Spam, Cross-Site Scripting-Angriffe und SQL-Injections blockieren.

Sie können die WAF nach Belieben aktivieren oder inaktivieren. Wir empfehlen, die Funktionalität immer aktiviert zu lassen.

## Schutz vor DDoS-Attacken
{:#ddos-protection}

IBM CIS stellt Ihrer Website DDoS-Schutz vor Angreifern bereit, unabhängig von der Größe oder der Dauer des Angriffs.

## Lastausgleich
{:#about-load-balancing}

IBM CIS-Lastausgleich arbeitet auf der Ebene des autoritativen DNS. Er umfasst erweiterte Statusprüfungen, um den Status der Ursprünge zu überwachen und DNS-Antworten dynamisch anzupassen. Darüber hinaus können Sie Georichtlinien für den globalen Lastausgleich (Global Load Balancing, GLB) konfigurieren.

### Statusprüfungen
{:#about-health-checks}

Statusprüfungen des Lastausgleichs werden mithilfe von periodischen HTTP- oder HTTP-Anforderungen für spezifische URLs durchgeführt und sind mit anpassbaren Intervallen, Zeitlimits und Statuscodes konfiguriert. Wenn ein Ursprungsserver als fehlerhaft markiert wird, werden Besucher mithilfe unserer schnellen Failover-Route umgeleitet, um Ausfälle zu vermeiden.
 
### Georichtlinien und globaler Lastausgleich
{geo-policies-and-glb}

Georichtlinien geben Ihnen abhängig von dem Standort eines Clients die Kontrolle über die Ursprungsserver, an die dieser Client geleitet wird. Sie können Ihre Georichtlinien beispielsweise so konfigurieren, dass Besucher in Europa an den nächstgelegenen europäischen Ursprungsserver für Ihre Website oder Anwendung geleitet werden, Besucher in den USA an einen Ursprungsserver in Nordamerika usw.

## Caching
{:#about-caching}

Caching ist eine Möglichkeit, Ihre statischen Webinhalte räumlich möglichst nahe bei Ihren Websitebesuchern zu speichern und so die Leistung der Website signifikant zu verbessern. Unsere weltweit verteilte Bereitstellungsumgebung ermöglicht es Webinhaltsbesitzern, weltweit ein nahtloses Erlebnis zu bieten.  
 
## Verschlüsselung mit TLS
{:#encryption-with-tls}

Verschlüsseln Sie die Kommunikation mit Ihrer Website mithilfe von Transport Layer Security (TLS). Nach der Inbetriebnahme Ihrer Website kann es bis zu 24 Stunden dauern, bis die neuen Zertifikate ausgestellt sind.

Weitere Informationen zu TLS finden Sie in unseren [FAQ](/docs/infrastructure/cis?topic=cis-faq).
