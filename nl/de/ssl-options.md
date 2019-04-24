---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: TLS Options, secure connection, Automatic HTTPS

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# TLS-Optionen
{:#cis-tls-options}

Mit TLS-Optionen können Sie steuern, ob Besucher auf Ihrer Website über eine sichere Verbindung navigieren können, und wie CIS in diesem Fall eine Verbindung zu Ihrem Ursprungsserver herstellt.

## Automatische HTTPS-Neuschreibung
{:#automatic-https-rewrite}

Die automatische HTTPS-Neuschreibung unterstützt die Korrektur von gemischten Inhalten durch die Änderung von “http” in “https” für alle Ressourcen oder Links auf Ihrer Website, die mit HTTPS bereitgestellt werden können. Diese Einstellung befindet sich auf der Seite mit der **erweiterten** Sicherheitskonfiguration. 

## TLS-Verschlüsselungsmodi
{:#tls-encryption-modes}

Diese Optionen werden beginnend mit der unsichersten (Aus) und endend mit der sichersten (End-to-End-CA-signiert) aufgeführt. 
 * Aus (nicht empfohlen)
 * Client-zu-Edge (Verbindung vom Edge zum Ursprung nicht verschlüsselt, selbst signierte Zertifikate werden nicht unterstützt) 
 * End-to-End-flexibel (Zertifikate von Edge zum Ursprung können selbst signiert sein) 
 * End-to-End-CA-signiert (empfohlene Standardeinstellung) 
 * Nur HTTPS-Origin-Pull (nur Enterprise)

### Aus 
{:#tls-encryption-modes-off}
Keine sichere Verbindung zwischen Ihrem Besucher und CIS und keine sichere Verbindung zwischen CIS und Ihrem Web-Server. Besucher können Ihre Seite nur über HTTP aufrufen und alle Besucher, die versuchen, eine HTTPS-Verbindung herzustellen, werden mit einem `HTTP 301 Redirect` zur normalen HTTP-Version Ihrer Website umgeleitet.

### Client-zu-Edge
{:#tls-encryption-modes-client-to-edge}

Eine sichere Verbindung zwischen Ihrem Besucher und CIS, aber keine sichere Verbindung zwischen CIS und Ihrem Web-Server. Sie müssen kein TLS-Zertifikat auf Ihrem Web-Server haben, aber Ihren Besuchern wird die Website trotzdem als HTTPS-fähig angezeigt. Diese Option wird nicht empfohlen, wenn Sie sensible Inhalte auf Ihrer Website bereitstellen. Diese Einstellung funktioniert nur für Port 443 -> 80. Sie sollte nur als letzte Möglichkeit in Betracht gezogen werden, wenn Sie TLS nicht auf Ihrem eigenen Web-Server einrichten können. Sie ist _weniger sicher_ als alle anderen Optionen (sogar weniger sicher als die Einstellung “Aus”) und könnte Probleme bereiten, wenn Sie entscheiden, zu einer anderen Einstellung zu wechseln.

### End-to-End-flexibel
{:#tls-encryption-modes-end-to-end-flexible}

Eine sichere Verbindung zwischen Ihrem Besucher und CIS und eine sichere (aber nicht authentifizierte) Verbindung zwischen CIS und Ihrem Web-Server. Sie müssen Ihren Server so konfiguriert haben, dass er auf HTTPS-Verbindungen mindestens mit einem selbst signierten Zertifikat antwortet. Die Authentizität des Zertifikats wird nicht verifiziert: aus Sicht von CIS (wenn wir eine Verbindung mit Ihrem Ursprungs-Web-Server herstellen) entspricht dies dem Umgehen dieser Fehlernachricht. Solange die Adresse Ihres Ursprungs-Web-Servers in Ihren DNS-Einstellungen korrekt ist, können Sie sich darauf verlassen, dass wir eine Verbindung mit Ihrem Web-Server herstellen und nicht mit einem fremden.

### End-to-End-CA-signiert
{:#tls-encryption-modes-end-to-end-ca-signed}

Empfohlene Standardeinstellung. Eine sichere Verbindung zwischen Ihrem Besucher und CIS und eine sichere und authentifizierte Verbindung zwischen CIS und Ihrem Web-Server. Sie müssen Ihren Server so konfiguriert haben, dass er auf HTTPS-Verbindungen mit einem gültigen TLS-Zertifikat antwortet. Dieses Zertifikat muss von einer Zertifizierungsstelle signiert sein, ein Ablaufdatum in der Zukunft haben und für den Namen der Anforderungsdomäne (Hostnamen) antworten. Wir empfehlen, dass Sie diesen TLS-Modus als bewährtes Sicherheitsverfahren weiter verwenden, es sei denn, Sie verstehen die möglichen Sicherheitsbedrohungen, die eine Änderung in einen weniger strikten Modus mit sich bringt. 

### Nur HTTPS-Origin-Pull
{:#tls-encryption-modes-origin-only-pull}

*Nur Enterprise*. Dieser Modus hat dieselben Zertifikatanforderungen wie End-to-End-CA-signiert und aktualisiert auch alle Verbindungen zwischen CIS und Ihrem Ursprungs-Web-Server von HTTP auf HTTPS, auch wenn der Originalinhalt über HTTP angefordert wird. 

## Mindestversion von TLS
{:#minimum-tls-version}

Dies legt die Mindestversion von TLS für Datenverkehr fest, der versucht, eine Verbindung zu Ihrer Site herzustellen. Standardmäßig ist dieser Wert auf 1.0 festgelegt. Höhere TLS-Versionen bieten zusätzliche Sicherheit, werden jedoch möglicherweise nicht von allen Browsern unterstützt. Dies kann dazu führen, dass einige Kunden keine Verbindung zu Ihrer Site aufbauen können. 
