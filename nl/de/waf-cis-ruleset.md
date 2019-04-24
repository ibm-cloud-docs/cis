---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIS Rule Set, WAF settings, WAF CIS Rules

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# WAF-Einstellungen
{:#waf-settings}

Die folgende Tabelle zeigt die Aktionen, die WAFs (Web Application Firewalls) ausführen können.  


|Aktion| Definition|
|---|---|
|Blockieren | Das Blockieren eines Angriffs führt zum Stoppen aller Aktionen, bevor die Blockierung auf Ihrer Website gemeldet wird. |
|Simulieren | Um falsche positive Werte zu testen, legen Sie für WAF den Simulationsmodus fest, in dem die Antwort auf mögliche Angriffe aufgezeichnet wird, ohne die Anforderung auszuführen oder zu blockieren. |
|Sicherheitsabfrage ausgeben | Eine Sicherheitsabfrage fordert von den Besuchern, ein CAPTCHA zu übergeben, bevor Sie mit der Anzeige Ihrer Website fortfahren können. |
|Einstellung für Schwellenwert oder Sicherheitsstufe| Legt abhängig von der Sicherheitsstufe mehr oder weniger Regeln für Auslöser fest. |

## CIS-Regelsatz für WAF
{:#cis-ruleset-for-waf}

Wählen Sie **CIS-Regeln anzeigen** aus, um die Regelsätze dieses Pakets sichtbar zu machen. Die Regelsätze sind folgende: 
  * Drupal
  * Flash
  * Joomla
  * Magento
  * Sonstige
  * PHP
  * Plone
  * Besondere
  * WHMCS
  * Wordpress

**Besondere** enthält eine Reihe von Regeln, die für nahezu alle Anwendungen und Websites im Internet geeignet sind. Dieser Regelsatz ist das Kernstück der Sicherheit, die unsere WAF mit Regeln, die auf übliche Angriffe wie SQLi, XSS und LFI abzielen, bietet. Wir empfehlen, die Option 'Besondere' immer aktiviert zu lassen. 

Aktivieren Sie nur die Regelsätze, die Ihrem Technologiestack entsprechen. Wenn Sie zum Beispiel Wordpress verwenden aber keine der anderen Technologien, aktivieren Sie nur die Option 'Besondere' und die Wordpress-Regelsätze. Vermeiden Sie es, Regelsätze zu aktivieren, die für Ihren Technologiestack nicht relevant sind. 

Wählen Sie einen der spezifischen Regelsätze aus, um weitere Details zu jeder der enthaltenen Regel anzuzeigen. 

Der CIS-Regelsatz ermöglicht Ihnen die Ausführung von vier Aktionen für jede Regel: 
  1. **Inaktivieren**: Schaltet die Regel aus. 
  2. **Simulieren**: Protokolliert das Ereignis und blockiert den Besucher nicht und führt auch keine Sicherheitsabfrage mit ihm durch (Sie können nach der Durchsicht Ihrer Protokolle immer noch entscheiden, eine Blockierung festzulegen oder eine Sicherheitsabfrage auszugeben). 
  3. **Blockieren**: Die Anfrage wird vollständig blockiert und es gibt für die Anforderung keine Möglichkeit, diese Blockierung zu umgehen. 
  4. **Abfrage**: Zeigt eine Seite mit einer Sicherheitsabfrage (CAPTCHA) an, die ausgefüllt werden muss, bevor der fraglichen Anforderung der Zugriff gewährt wird. 

Sie stellen möglicherweise fest, dass die Namen der Regeln nicht genau angeben, wie diese funktionieren und eher eine allgemeine Zusammenfassung ihrer Funktion darstellen. Das ist gewollt. Aus Sicherheitsgründen, wird der Code (oder andere genauere Informationen), der zum Filtern des Datenverkehrs verwendet wird, nicht offengelegt. Dadurch wird verhindert, dass böswillige Akteure diese Informationen für Reverse Engineering verwenden und unsere Verteidigung umgehen. 
