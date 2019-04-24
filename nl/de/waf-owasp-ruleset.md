---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: OWASP Rule Set, Rule Set

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# OWASP-Regelsatz für WAF
{:#owasp-rule-set-for-waf}

Der OWASP-Regelsatz enthält generische Regeln zur Angriffserkennung. Die OWASP-Regeln schützen vor vielen gängigen Angriffskategorien einschließlich SQL-Injection, Cross-Site Scripting, Locale File Inclusion und vielen anderen. IBM CIS stellt diese Regeln zur Verfügung, wählt Sie jedoch nicht aus. OWASP ist ein Industriestandard, der ein gute Sicherheitsbasis bietet. Weitere Informationen finden Sie unter den folgenden Links: 
  * [OWASP on Github](https://github.com/SpiderLabs/owasp-modsecurity-crs)
  * [OWASP.org](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project)

## OWASP verwalten
{:#managing-owasp}

Im Gegensatz zum [CIS-Regelsatz](/docs/infrastructure/cis?topic=cis-cis-rule-set-for-waf), ermöglicht OWASP die Einstellung einer Sicherheitsstufe.
Eine Anforderung kann eine Reihe von OWASP-Regeln auslösen, denen eine hohe oder niedrige Sicherheitsbewertung zugeordnet ist. Die endgültige Bewertung wird auf Grundlage aller ausgelösten Regeln berechnet. Nach der Berechnung der endgültigen Bewertung vergleicht CIS diese mit dem Schwellenwert für die Sicherheitsstufe, der zu Beginn ausgewählt wurde, und lässt dann entweder die Anforderung zu oder blockiert sie.


|Sicherheitsstufe |Auslöserschwellenwert|
|-------|---------------|
|Niedrig|   60 und mehr |
|Mittel |   40 und mehr |
|Hoch   |   25 und mehr |

Es wird empfohlen, für die OWASP-Sicherheitsstufe `Niedrig` festzulegen. Wenn Sie `Hoch` festlegen, überprüfen Sie die Protokolle von CIS und optimieren Sie den OWASP-Regelsatz, um ihn an Ihre Anwendung anzupassen. 

Beachten Sie, dass OWASP-Regeln nur _ein_- oder _aus_geschaltet werden können. Für die CIS-Regelsätze dagegen können Sie _Inaktivieren_, _Simulieren_, _Sicherheitsabfrage ausgeben_ oder _Blockieren_ festlegen.

## Wie werden Fehlalarme behandelt? 
{:#owasp-false-positives}

Fehlalarme treten auf, wenn Variablen oder Werte als _wahr_ oder _positiv_ ausgewertet werden, tatsächlich aber negativ sind. Im Zusammenhang mit unserer WAF bedeutet ein falsch positiver Wert, dass eine Anforderung blockiert wird, weil sie fälschlicherweise als schädlich eingestuft wurde. 

Um mit Fehlalarmen umzugehen und sie in Zukunft zu vermeiden, müssen Sie wissen, wie Sie sie erkennen und korrigieren können. Überprüfen Sie die Protokolle der blockierten Anforderungen und werten Sie dann aus, ob diese Anforderungen aus guten Gründen innerhalb des Kontexts von erwartetem und normalem Datenverkehr auf Ihrer Website blockiert wurden. 
