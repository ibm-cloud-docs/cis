---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: health checks, origin pools, load balancers, IBM CIS

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Lastausgleichsfunktionen einrichten und konfigurieren
{:#set-up-and-configure-your-load-balancers}
 
 IBM CIS stellt einen globalen Lastausgleich als Service bereit. So sieht das GLB-Dashboard aus:

![ABBILDUNG](images/glb-screen.png)

## GLB-Dashboard
{:#glb-dashboard}

Auf Ihrem Dashboard werden drei Listen angezeigt - für Lastausgleichsfunktionen, für Ursprungspools und für Statusprüfungen. In den Listen werden die neue oder aktualisierte globale Lastausgleichsfunktion oder eine ihrer Komponenten angezeigt. Anfänglich sind die Listen leer und bevor Sie eine Lastausgleichsfunktion erstellen, müssen Sie einige Aktionen ausführen.

Wenn Sie bereits wissen, was Sie tun müssen, finden Sie weitere Informationen im [Leitfaden für den Schnelleinstieg](/docs/infrastructure/cis?topic=cis-global-load-balancer-quick-setup). 

### Erstellen
{:#create-health-check}

<sup>`*`</sup> weist darauf hin, dass dieser Schritt optional ist.
{:note}

1) <sup>`*`</sup>Erstellen Sie eine Statusprüfung, klicken Sie auf **Statusprüfung erstellen**.
  ![ABBILDUNG](images/glb-health-check-list.png)
    <ul>
      <li><b>Pfad</b>: Der Pfad zu dem Endpunkt, an dem die Statusprüfung ausgeführt werden soll.</li> 
      <li><b>Typ</b>: Das Protokoll für die Statusprüfung.</li>
      <li><b>Beschreibung</b>: Vom Benutzer bereitgestellte Beschreibung.</li>
    </ul>

2) Erstellen Sie einen Pool und klicken Sie auf **Pool erstellen**.
  ![ABBILDUNG](images/glb-pool-list.png)
    <ul>
      <li><b>Status</b>: Status des Pools.</li>
      <li><b>Name</b>: Vom Benutzer angegebener Name.</li>
      <li><b>Ursprünge</b>: Anzahl von Ursprüngen in einwandfreiem Zustand im Pool.</li>
      <li><b>Statusprüfung</b>: Pfad der angehängten Statusprüfung, falls vorhanden.</li>
    </ul>

3) Erstellen Sie eine Lastausgleichsfunktion, klicken Sie auf **Lastausgleichsfunktion erstellen**.
  ![ABBILDUNG](images/glb-load-balancer-list.png)
    <ul>
      <li><b>Status</b>: Status der Lastausgleichsfunktion.</li>
      <li><b>Hostname</b>: Dem Domänennamen vorangestellter Name.</li>
      <li><b>Verfügbare Pools</b>: Anzahl von Pools in einwandfreiem Zustand.</li>
      <li><b>TTL</b>: Lebensdauer.</li>
      <li><b>Proxy</b>: Proxy-Datenverkehr aktivieren oder inaktivieren.</li>
      <li><b>Status</b>: Lastausgleichsfunktion aktivieren oder inaktivieren.</li>
    </ul>

Die geografischen Regionen von IBM unterscheiden sich von Cloudflare-Regionen. Weitere Informationen zu den geografischen Regionen, die Cloudflare verwendet, finden Sie unter [Lastausgleich: geografische Regionen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://support.cloudflare.com/hc/en-us/articles/115000540888-Load-Balancing-Geographic-Regions){:new_window}.  
{:note}

### Bearbeiten/Löschen
{:#edit-delete-load-balancer}
Um eine Lastausgleichsfunktion oder eine ihrer Komponenten zu bearbeiten oder zu löschen, klicken Sie auf die Überlaufmenüschaltfläche am rechten Ende jeder Zeile.

Überlaufmenüschaltfläche:

![ABBILDUNG](images/overflow.png)

Folgende Optionen stehen für jede Liste zur Verfügung.

* Statusprüfung
    * **Statusprüfung anzeigen**: Diese Option zeigt eine kurze Zusammenfassung der Statusprüfung mit einem Link an, der Sie zum Bearbeitungsablauf führt. 
    * **Statusprüfung bearbeiten**: Diese Option leitet den Benutzer an den Bearbeitungsablauf weiter. 
    * **Statusprüfung löschen**: Diese Option ruft das Bestätigungsdialogfenster für den Löschablauf auf.

* Pool
    * **Pooldetails anzeigen**: Diese Option ruft ein Modaldialogfenster mit Informationen zu dem Pool auf.
    * **Pool bearbeiten**: Diese Option leitet den Benutzer an den Bearbeitungsablauf weiter.
    * **Pool löschen**: Diese Option ruft das Bestätigungsdialogfenster für den Löschablauf auf.

* Lastausgleichsfunktion
    * **Inaktivieren/Aktivieren**: Lastausgleichsfunktion aktivieren oder inaktivieren.
    * **Lastausgleichsfunktion bearbeiten**: Leitet den Benutzer an den Bearbeitungsablauf weiter. 
    * **Lastausgleichsfunktion löschen**: Diese Option ruft das Bestätigungsdialogfenster für den Löschablauf auf.

## Statusprüfung hinzufügen
{:#add-a-health-check}

Statusprüfungen sind optionale Anhänge für Ursprungspools. Sie setzen ein benutzerdefiniertes Wiederholungsintervall ein, um auf einen bestimmten Antworttext oder Statuscode zu prüfen und so den Status des Pools zu überwachen. Nachdem Statusprüfungen erstellt wurden, können sie einem neuen oder vorhandenen Ursprungspool hinzugefügt werden.

Beim Erstellen einer Statusprüfung ist nur ein Feld erforderlich:
 * **Antwortcode**: Der erwartete HTTP-Antwortcode oder -codebereich der Statusprüfung. Dieser Wert muss zwischen 200 und 299 liegen, wobei Platzhalter durch ein 'x' dargestellt werden.

Zusätzliche optionale Felder:
 * **Pfad**: Der Pfad zu dem Endpunkt, an dem die Statusprüfung durchgeführt werden soll (Standardwert ist '/').
 * **Typ**: Das Protokoll für die Statusprüfung (Standardwert ist 'HTTP').
 * **Beschreibung**: Die Beschreibung der Statusprüfung.
 * **Intervall**: Das Intervall (in Sekunden) zwischen den einzelnen Statusprüfungen. Kürzere Intervalle können die Failoverzeit verbessern, aber die Auslastung der Ursprünge erhöhen, wenn die Prüfungen an mehreren Orten durchgeführt werden (Standardwert ist '60').
 * **Methode**: Die HTTP-Methode für die Statusprüfung (Standardwert ist GET).
 * **Zeitlimit**: Die Zeit (in Sekunden) vor dem Markieren der Statusprüfung als fehlgeschlagen (Standardwert ist '5').
 * **Wiederholungen**: Die Anzahl von Wiederholungen im Fall einer Zeitlimitüberschreitung, bevor der Ursprung als fehlerhaft markiert wird. Wiederholungen werden unmittelbar ausgeführt (Standardwert ist '2').
 * **Antwortteil**: Eine von Groß-/Kleinschreibung unabhängige Teilzeichenfolge, die mit dem Antwortteil abgeglichen werden soll. Wird diese Zeichenfolge nicht gefunden, wird der Ursprung als fehlerhaft markiert.
 * **Anforderungsheader**: Die HTTP-Anforderungsheader, die im Rahmen der Statusprüfung gesendet werden sollen. Wir empfehlen, einen Host-Header standardmäßig festzulegen. Der Header `User-Agent` kann nicht überschrieben werden.

## Pool hinzufügen
{:#add-a-pool}

Für jede bereitgestellte Lastausgleichsfunktion ist mindestens ein Pool erforderlich. Pools gruppieren Ihre Ursprünge für die zu verwendende Lastausgleichsfunktion.

Wenn Sie einen Pool erstellen, sind zwei Felder erforderlich:
 * **Name**: Ein Kurzname (Tag) für den Pool. Es sind nur alphanumerische Zeichen, Bindestriche und Unterstreichungszeichen zulässig.
 * **Ursprünge**: Die Liste von Ursprüngen in diesem Pool. Der an diesen Pool umgeleitete Datenverkehr wird über alle Ursprünge ausgeglichen, die sich aktuell in einwandfreiem Zustand befinden, vorausgesetzt, der Pool selbst ist fehlerfrei.

Zusätzliche optionale Felder:
 * **Beschreibung**: Eine lesbare Beschreibung des Pools.
 * **Aktiviert**: Eine Angabe, ob dieser Pool aktiviert werden soll (Standardeinstellung). Inaktivierte Pools empfangen keinen Datenverkehr und sind von Statusprüfungen ausgeschlossen. Das Inaktivieren eines Pools führt dazu, dass für alle Lastausgleichsfunktionen ein Failover zum nächsten Pool durchgeführt wird, falls vorhanden (Standardeinstellung ist 'wahr').
 * **Schwellenwert für Ursprünge in einwandfreiem Zustand**: Die Mindestanzahl von Ursprüngen, die sich in einwandfreiem Zustand befinden müssen, damit dieser Pool Datenverkehr verarbeiten kann. Wenn die Anzahl der Ursprünge in einwandfreiem Zustand unter diese Zahl fällt, wird der Pool als fehlerhaft markiert und es wird ein Failover zum nächsten verfügbaren Pool durchgeführt (Standardwert ist '1').
 * **Regionen der Statusprüfung**: Region, die von der Statusprüfung überwacht wird. **Hinweis**: Die geografischen Regionen von IBM unterscheiden sich von Cloudflare-Regionen. Weitere Informationen zu den geografischen Regionen, die Cloudflare verwendet, finden Sie unter [Lastausgleich: geografische Regionen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://support.cloudflare.com/hc/en-us/articles/115000540888-Load-Balancing-Geographic-Regions){:new_window}. 
 * **Statusprüfung**: Statusprüfung für die Prüfung von Ursprüngen in diesem Pool (standardmäßig ist keine Statusprüfung festgelegt).
 * **Benachrichtigungs-E-Mail**: Die E-Mail-Adresse, an die Statusbenachrichtigungen gesendet werden sollen. Bei dieser Adresse kann es sich um eine einzelne Mailbox oder um eine Mailing-Liste handeln.

## Lastausgleichsfunktion hinzufügen
{:#add-a-load-balancer}

Lastausgleichsfunktionen helfen Ihnen, Ihren Proxy-Datenverkehr mithilfe einer Umlaufverteilung über mehrere Ursprungspools zu verteilen.

Beim Erstellen einer Lastausgleichsfunktion sind die erforderlichen Felder folgende:
 * **Name**: Der DNS-Hostname, der Ihrer Lastausgleichsfunktion zugeordnet werden soll. Wenn dieser Hostname bereits als DNS-Eintrag im IBM DNS vorhanden ist, hat die Lastausgleichsfunktion Vorrang und der DNS-Datensatz wird nicht verwendet.
 * **Standardpools**: Eine Liste von Pool-IDs. Die Liste ist nach Failoverpriorität geordnet. Hier definierte Pools werden standardmäßig verwendet, oder wenn für eine bestimmte Region keine Regionspools konfiguriert sind.

Optional können die folgenden Felder konfiguriert werden:
 * **Proxy**: Leitet Datenverkehr über den IBM Performance and Metrics Service weiter.
 * **Sitzungsaffinität**: Leitet Datenverkehr immer über dieselbe Instanz des Performance and Metrics Service weiter. Diese Option ist nur verfügbar, wenn ein Proxy aktiviert ist.
 * **TTL**: Lebensdauer (Time to Live, TTL) des DNS-Eintrags für die von dieser Lastausgleichsfunktion zurückgegebene IP-Adresse. Diese Option gilt nur für Nicht-Proxy-Lastausgleichsfunktionen. Andernfalls nimmt sie standardmäßig den Wert `Automatisch` an.
 * **Regionspools**: Zuordnung von Regions- oder Landescodes zu einer Liste von (nach Failoverpriorität sortierten) Pools für die gegebene Region. Alle nicht explizit definierten Regionen verwenden die Standardpools. **Hinweis**: Die geografischen Regionen von IBM unterscheiden sich von Cloudflare-Regionen. Weitere Informationen zu den geografischen Regionen, die Cloudflare verwendet, finden Sie unter [Lastausgleich: geografische Regionen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://support.cloudflare.com/hc/en-us/articles/115000540888-Load-Balancing-Geographic-Regions){:new_window}. 
 
Definitionen von Begriffen, die in diesem Dokument verwendet werden, die allgemein in der gesamten Branche verwendet werden, finden Sie im [Glossar](/docs/infrastructure/cis?topic=cis-glossary).
