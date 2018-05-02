---
copyright:
  years: 2018
lastupdated: "2018-02-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# TLS-Optionen
Mit TLS-Optionen können Sie steuern, ob Besucher auf Ihrer Website über eine sichere Verbindung navigieren können, und wie CIS in diesem Fall eine Verbindung zu Ihrem Ursprungsserver herstellt. 

Diese Optionen werden beginnend mit der unsichersten (Aus) und endend mit der sichersten (End-to-End-CA-signiert) aufgeführt.  

TLS-Verschlüsselungsmodi:

 * Aus (nicht empfohlen)
 * Client-zu-Edge (Verbindung vom Edge zum Ursprung nicht verschlüsselt, selbst signierte Zertifikate werden nicht unterstützt) 
 * End-to-End-flexibel (Zertifikate für die Verbindung vom Edge zum Ursprung können selbst signiert sein) 
 * End-to-End-CA-signiert (empfohlen)

## Aus 
Keine sichere Verbindung zwischen Ihrem Besucher und CIS und keine sichere Verbindung zwischen CIS und Ihrem Web-Server. Besucher können Ihre Seite nur über HTTP aufrufen und alle Besucher, die versuchen, eine HTTPS-Verbindung herzustellen, werden mit einem `HTTP 301 Redirect` zur normalen HTTP-Version Ihrer Website umgeleitet. 

## Client-zu-Edge
Eine sichere Verbindung zwischen Ihrem Besucher und CIS, aber keine sichere Verbindung zwischen CIS und Ihrem Web-Server. Sie müssen kein TLS-Zertifikat auf Ihrem Web-Server haben, aber Ihren Besuchern wird die Website trotzdem als HTTPS-fähig angezeigt. Diese Option wird nicht empfohlen, wenn Sie sensible Inhalte auf Ihrer Website bereitstellen. Diese Einstellung funktioniert nur für Port 443 -> 80. Sie sollte nur als letzte Möglichkeit in Betracht gezogen werden, wenn Sie TLS nicht auf Ihrem eigenen Web-Server einrichten können. Sie ist _weniger sicher_ als alle anderen Optionen (sogar weniger sicher als die Einstellung “Aus”) und könnte Probleme bereiten, wenn Sie entscheiden, zu einer anderen Einstellung zu wechseln. 

## End-to-End-flexibel
Eine sichere Verbindung zwischen Ihrem Besucher und CIS und eine sichere (aber nicht authentifizierte) Verbindung zwischen CIS und Ihrem Web-Server. Sie müssen Ihren Server so konfiguriert haben, dass er auf HTTPS-Verbindungen mindestens mit einem selbst signierten Zertifikat antwortet. Die Authentizität des Zertifikats wird nicht verifiziert: aus Sicht von CIS (wenn wir eine Verbindung mit Ihrem Ursprungs-Web-Server herstellen) entspricht dies dem Umgehen dieser Fehlernachricht. Solange die Adresse Ihres Ursprungs-Web-Servers in Ihren DNS-Einstellungen korrekt ist, können Sie sich darauf verlassen, dass wir eine Verbindung mit Ihrem Web-Server herstellen und nicht mit einem fremden. 

## End-to-End-CA-signiert
Empfohlen. Eine sichere Verbindung zwischen Ihrem Besucher und CIS und eine sichere und authentifizierte Verbindung zwischen CIS und Ihrem Web-Server. Sie müssen Ihren Server so konfiguriert haben, dass er auf HTTPS-Verbindungen mit einem gültigen TLS-Zertifikat antwortet. Dieses Zertifikat muss von einer Zertifizierungsstelle signiert sein, ein Ablaufdatum in der Zukunft haben und für den Namen der Anforderungsdomäne (Hostnamen) antworten.
