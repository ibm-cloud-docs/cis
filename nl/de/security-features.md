---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIDR blocks, Whitelist Block Challenge, IBM Cloud Internet Services, security features

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Informationen zur Sicherheit mit IBM Cloud Internet Services (CIS)
{:#how-cis-keeps-your-work-secure}

IBM CIS ist ein global verteilter Cloud-Service, der Bedrohungen blockiert und böswillige Bots und Crawler abwehrt, die sich negativ auf Ihre Bandbreite und Serverressourcen auswirken können. IBM CIS fungiert als globaler HTTP(S)-Reverse Proxy und als verwalteter DNS-Serviceanbieter. Ihr Webdatenverkehr wird über unser intelligentes globales Netz geleitet, um Ihre Leistung und Sicherheit zu optimieren.

![Sicherheitsgrafik.png](images/security-graphic.png)

Dies sind die wichtigsten Merkmale kurz zusammengefasst:

## Sicherheitsmerkmale
{:#cis-security-features}

 * Weiterleiten von [DNS-Datensätzen](/docs/infrastructure/cis?topic=cis-dns-concepts#proxying-dns-records) oder [GLB](/docs/infrastructure/cis?topic=cis-global-load-balancer-glb-concepts) zur Verwendung der Sicherheitsfunktionen. Dadurch kann der Datenverkehr durch unsere Server fließen und die Daten können überwacht werden.
### Web Application Firewall (WAF)
{:#cis-web-application-firewall}

 * WAF wird über zwei Regelsätze implementiert: [OWASP](/docs/infrastructure/cis?topic=cis-owasp-rule-set-for-waf) und [CIS](/docs/infrastructure/cis?topic=cis-waf-settings#cis-rule-set-for-waf).
### Uneingeschränkte DDoS-Risikominderung
{:#cis-unlimited-ddos-mitigation}

 * Die DDoS-Risikominderung ist in der Regel ein teurer Service, dessen Kosten bei einem Angriff noch steigen können. In CIS ist eine unbegrenzte DDoS-Risikominderung ohne Zusatzkosten eingeschlossen. 

## Sicherheitsstandards und -plattform
{:#security-standards-and-platform}

 * TLS (SHA2 und SHA1)
 * IPv6
 * HTTP/2 und SPDY

## DNS
{:#cis-dns}

 * Globales Anycast-Netz
 * DNSSEC

## Netzangriffe und Risikominderung
{:#network-attacks-and-mitigation}

Allgemein lassen sich Angriffe in zwei Kategorien unterteilen:

| Layer-3- oder Layer-4-Angriffe | Layer-7-Angriffe |
|------------------------------|-----------------|
|Diese Angriffe bestehen aus einer Flut von Datenverkehr an ISO Layer 3 (der Netzschicht), z. B. ICMP-Flooding, oder an Layer 4 (der Transportschicht), z. B. TCP-SYN-Flooding oder reflektiertes UDP-Flooding. |Diese Angriffe senden böswillige ISO-Layer-7-Anforderungen (Anwendungsschicht), z. B. GET-Flooding.  |
| Automatisch an unserem Edge blockiert. | Wir setzen dafür die Einstellungen 'Verteidigungsmodus', 'WAF' und 'Sicherheitsstufe' ein. |

## IP-Firewall
{:#cis-ip-firewall}

IBM Cloud Internet-Services bietet mehrere Tools zur Steuerung Ihres Datenverkehrs, sodass Sie Ihre Domänen, URLs und Verzeichnisse gegen große Mengen an Datenverkehr, bestimmte Anforderergruppen und bestimmte Anforderungs-IPs schützen können. In diesem Abschnitt werden die Details der verfügbaren Tools genauer erläutert. 

### IP-Regeln
{:#cis-ip-rules}

Die IP-Regeln ermöglichen Ihnen den Zugriff für bestimmte IP-Adressen, IP-Bereiche, bestimmte Länder, bestimmte ASNs und bestimmte CIDR-Blöcke zu steuern. Verfügbare Aktionen für eingehende Anforderungen sind: 
  * Whitelist 
  * Blockieren  
  * Abfrage (Captcha) 
  * JavaScript-Abfrage (IUAM-Abfrage)

Wenn Sie zum Beispiel bemerken, dass eine bestimmte IP-Adresse schädliche Anforderung stellt, können Sie diesen Benutzer über die IP-Adresse blockieren. 

### Blockierungsregeln für Benutzeragenten
{:#user-agent-blocking-rules}

Die Blockierungsregeln für Benutzeragenten ermöglichen es Ihnen, eine Aktion mit einer beliebigen, von Ihnen ausgewählten Zeichenfolge eines Benutzeragenten  auszuführen. Dies funktioniert wie bei einer zuvor beschriebenen Domänensperrung. Der Unterschied besteht darin, dass die eingehende Zeichenfolge des Benutzeragenten und nicht die IP untersucht wird. Sie können mithilfe derselben Liste von Aktionen, die Sie bei den IP-Regeln etabliert haben (Blockieren, Sicherheitsabfrage und JS-Abfrage ausgeben), auswählen, wie eine übereinstimmende Anforderung verarbeitet werden soll. Beachten Sie, dass das Blockieren von Benutzeragenten für Ihre gesamte Zone gilt. Sie können hier keine Unterdomäne wie bei der Domänensperrung angeben. 

Dieses Tool ist zum Blockieren von Zeichenfolgen von Benutzeragenten sinnvoll, die Sie als verdächtig einschätzen.  

### Domänensperrung
{:#cis-domain-lockdown}

Die Domänensperrung ermöglicht Ihnen, bestimmte IP-Adressen und IP-Bereiche auf eine Whitelist zu setzen, sodass alle anderen IPs mit Sperrvermerken versehen sind.  Die Domänensperrung unterstützt: 

  * Bestimmte Unterdomänen. Sie ermöglichen der IP `1.2.3.4` beispielsweise Zugriff auf die Domäne `foo.example.com` und der IP `5.6.7.8` Zugriff auf die Domäne `bar.example.com`, ohne dass die Umkehrung zugelassen werden muss. 
  * Bestimmte URLs. Sie können zum Beisiel der IP `1.2.3.4` Zugriff auf das Verzeichnis `example.com/foo/*` ermöglichen und der IP `5.6.7.8` Zugriff auf das Verzeichnis `example.com/bar/*`, ohne dass die Umkehrung zugelassen werden muss.
Diese Funktion ist sinnvoll, wenn Sie eine höhere Granularität in Ihren Zugriffsregeln benötigen, da Sie mit den IP-Regeln entweder alle Unterdomänen der aktuellen Domäne oder alle Domänen in Ihrem Konto blockieren und keine spezifischen URIs angeben können. 

### Sicherheitsabfrage durchlaufen
{:#cis-challenge-passage}

Diese Einstellung in den **erweiterten** Sicherheitseinstellungen ermöglicht Ihnen zu steuern, wie lange ein Besucher, der eine Sicherheitsabfrage oder eine JavaScript-Abfrage absolviert hat, Zugriff auf Ihre Site erhält, bevor er erneut eine solche Abfrage absolvieren muss. Dies basiert auf der IP des Besuchers und gilt daher nicht für Abfragen, die von WAF-Regeln gestellt werden, da diese auf einer Aktion beruhen, die der Benutzer auf Ihrer Site ausführt. 

### Browserintegritätsprüfung
{:#cis-browser-integrity-check}

Diese Einstellung befindet sich in den **erweiterten** Sicherheitseinstellungen. Die Browserintegritätsprüfung sucht nach HTTP-Headern, die normalerweise von Spammern missbraucht werden. Sie verweigert Datenverkehr mit diesen Headern den Zugriff auf Ihre Seite. Ferner werden Besucher ohne Benutzeragent oder Benutzer, die einen vom Standard abweichenden Benutzeragenten hinzufügen (diese Taktik wird häufig von Bots, Crawlern oder APIs verwendet), blockiert oder einer Sicherheitsabfrage unterzogen. 
