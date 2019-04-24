---
copyright:
  years: 2018
lastupdated: "2018-03-17"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Verwalten Ihrer IBM CIS-Bereitstellung (Cloud Internet Services)

Sie beginnen mit der Übersichtsanzeige als Ausgangspunkt für alle weiteren Aktivitäten. Darin finden Sie alle aktuellen Parameter für Ihre Bereitstellung. 

Nachdem Sie Ihr DNS eingerichtet und konfiguriert haben, kann es losgehen! 

## Übersichtsanzeige verwenden

In der Übersichtsanzeige können Sie den Status aller Ihrer Auswahlen sehen. Sie können die Einstellungen direkt in der Übersichtsanzeige ändern, indem Sie einfach auf den unterstrichenen Namen der Einstellung klicken, die Sie ändern möchten. Sie können beispielsweise auf das Feld mit den `Lastausgleichsfunktionen` klicken, um eine Lastausgleichsfunktion hinzuzufügen. 

In der Übersichtsanzeige können Sie sehen, dass Ihre Domänennamenkonfiguration den Status **Anstehend** oder **Aktiv** hat, wie in der folgenden Abbildung gezeigt. 

![Abbildung der Übersichtsanzeige](images/overview-screen-configuration-summary.png)


## DNS konfigurieren und verwalten

Rufen Sie Ihre DNS-Seite auf und fügen Sie einen Datensatz hinzu (höchstwahrscheinlich ein Datensatz vom Typ A). Geben Sie die Informationen zu Ihrem DNS-Datensatz ein und klicken Sie auf `Datensatz hinzufügen`, um Ihre Änderungen zu implementieren. 

![DNS hinzufügen](images/dns/create-a-type-record.png)

## Caching einrichten und verwalten

Als Nächstes können Sie das Caching einrichten.  

![ABBILDUNG](images/caching-screen.png)

Sie können zwischen drei Typen von Caching auswählen, die im Dropdown-Menü der Caching-Ansicht verfügbar sind:  

 * Keine Abfragezeichenfolge: Es werden nur Ressourcen aus dem Cache bereitgestellt, wenn keine Abfragezeichenfolge vorhanden ist. 
 * Unabhängig von Abfragezeichenfolge: Übergibt dieselbe Ressource an alle, unabhängig von der Abfragezeichenfolge. (Hinweis: Die Einstellung **Abfragezeichenfolge ignorieren** gilt nur für statische Dateierweiterungen. Diese Einstellung entfernt die Abfragezeichenfolge beim Generieren des Cache-Schlüssels, sodass eine Anforderung `style.css?something` normalisiert wird zu `style.css`, wenn sie den Cache passiert.) 
 * Abhängig von Abfragezeichenfolge: Übergibt jedes Mal eine andere Ressource, wenn sich die Abfragezeichenfolge ändert. 
  
## Cache löschen
 
Sie können Ihren Cache jederzeit in Vorbereitung auf Aktualisierungen löschen, indem Sie einfach die URL in das Feld zum Löschen des Cache einfügen. Sie können eine einzelne Datei oder mehrere Dateien (bis zu 30 gleichzeitig) löschen. 
 
 ## Verfallsdatum des Browsers
 
Im Dropdown-Menü können Sie das erforderliche Verfallsdatum des Browsers auswählen, z. B. 8 Stunden oder 1 Tag. 
 
 ## Entwicklungsmodus verwenden
 
Der **Entwicklungsmodus** ist für die Verwendung bei wichtigen Aktualisierungen oder neuen Dateiuploads vorgesehen, oder wenn Sie vermeiden möchten, dass die Endbenutzer den Cache nutzen, und sie Dateien stattdessen direkt von den Ursprungsservern abrufen sollen. Um den **Entwicklungsmodus** zu verwenden, schalten Sie ihn auf `Aktiviert` um. Wenn Sie den **Entwicklungsmodus** nicht nicht mehr verwenden möchten, schalten Sie ihn zurück auf `Inaktiviert`. Die Aktivierung des **Entwicklungsmodus** läuft automatisch nach drei Stunden ab.  

## Seitenregeln verwalten
 
Sie können bis zu 50 Seitenregeln aktivieren. Verwenden Sie dazu die Dropdown-Menüs. Die Regeleinstellungen sind in drei Kategorien unterteilt: **Sicherheit**, **Leistung** und **Zuverlässigkeit**. 

Beachten Sie: Wenn bestimmte Regeln aktiviert sind, werden andere Optionen abgeblendet, falls diese in Konflikt zu den eben ausgewählten Regeln stehen. Nachdem Sie die gewünschten Seitenregeln ausgewählt haben, klicken Sie auf **Bereitstellung**, um sie zu aktivieren. Die neuen Regeln werden sofort wirksam und sind auch sofort in der Ansicht 'Seitenregeln' sichtbar. 
 
 ![SEITENREGELMENÜS](images/page-rule-dropdown-settings.png)
 
Sie können Ihre Seitenregeln auch in der Tabelle aktivieren oder inaktivieren, die in der Ansicht 'Seitenregeln' enthalten ist. Weitere Informationen finden Sie unter [Seitenregeln verwenden](using-page-rules.html). 
 
 ## Sicherheitseinstellungen
 
Standardmäßig ist der DDoS-Schutz für alle DNS-Datensätze mit aktivem Proxy aktiviert, was in der Tabelle **Datensätze** auf der DNS-Seite vorgenommen werden kann. Schalten Sie die WAF ein. Wenn Sie die Regeln ein- oder ausschalten, werden die Änderungen sofort wirksam. 

![ABBILDUNG](images/ddos-waf-ssl-screen.png)

## Zertifikate

Wenn Sie in einer Zone bereitstellen, implementiert IBM CIS automatisch ein universelles Zertifikat für diese Zone. Sie müssen für einen zertifikatsbasierten Schutz in dieser Zone folglich nichts unternehmen. Wenn Sie möchten, können Sie Ihr eigenes Zertifikat hochladen. Sie benötigen ein separates Zertifikat für jede Zone und es wird eine Fehlernachricht angezeigt, falls das von Ihnen hochgeladene Zertifikat nicht zu Ihrer Zone passt. 

![ABBILDUNG](images/certificates-table.png)
 
 ## Lastausgleichsfunktionen einrichten und konfigurieren
 
 IBM CIS stellt einen globalen Lastausgleich als Service bereit. 

![ABBILDUNG](images/glb-screen.png)

### GLB-Dashboard
Auf Ihrem Dashboard werden drei Listen angezeigt - für Lastausgleichsfunktionen, für Ursprungspools und für Statusprüfungen. In den Listen werden die neue oder aktualisierte globale Lastausgleichsfunktion oder eine ihrer Komponenten angezeigt. Anfänglich sind die Listen leer und bevor Sie eine Lastausgleichsfunktion erstellen, müssen Sie einige Aktionen ausführen. 

#### Erstellen
**Hinweis**: <sup>`*`</sup> weist darauf hin, dass dieser Schritt optional ist. 

1) <sup>`*`</sup>Erstellen Sie eine Statusprüfung, klicken Sie auf 'Statusprüfung erstellen'.
  ![ABBILDUNG](images/glb-health-check-list.png)
    <ul>
      <li>* **Pfad**: Der Pfad zu dem Endpunkt, an dem die Statusprüfung ausgeführt werden soll. </li> 
      <li>* **Typ**: Das Protokoll für die Statusprüfung. </li>
      <li>* **Beschreibung**: Vom Benutzer bereitgestellte Beschreibung. </li>
    </ul>

2) Erstellen Sie einen Pool, klicken Sie auf 'Pool erstellen'.
  ![ABBILDUNG](images/glb-pool-list.png)
    <ul>
      <li>* **Status**: Status des Pools. </li>
      <li>* **Name**: Vom Benutzer angegebener Name. </li>
      <li>* **Ursprünge**: Anzahl von Ursprüngen in einwandfreiem Zustand im Pool. </li>
      <li>* **Statusprüfung**: Pfad der angehängten Statusprüfung, falls vorhanden. </li>
    </ul>

3) Erstellen Sie eine Lastausgleichsfunktion, klicken Sie auf 'Lastausgleichsfunktion erstellen'.
  ![ABBILDUNG](images/glb-load-balancer-list.png)
    <ul>
      <li>* **Status**: Status der Lastausgleichsfunktion. </li>
      <li>* **Hostname**: Dem Domänennamen vorangestellter Name. </li>
      <li>* **Verfügbare Pools**: Anzahl von Pools in einwandfreiem Zustand. </li>
      <li>* **TTL**: Lebensdauer. </li>
      <li>* **Proxy**: Proxy-Datenverkehr aktivieren oder inaktivieren. </li>
      <li>* **Status**: Lastausgleichsfunktion aktivieren oder inaktivieren. </li>
    </ul>

#### Bearbeiten/Löschen
Um eine Lastausgleichsfunktion oder eine ihrer Komponenten zu bearbeiten oder zu löschen, klicken Sie auf die Überlaufmenüschaltfläche am rechten Ende jeder Zeile. 

Überlaufmenüschaltfläche: 

![ABBILDUNG](images/overflow.png)

Folgende Optionen stehen für jede Liste zur Verfügung. 

* Statusprüfung
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

### Statusprüfung hinzufügen

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

### Pool hinzufügen

Für jede bereitgestellte Lastausgleichsfunktion ist mindestens ein Pool erforderlich. Pools gruppieren Ihre Ursprünge für die zu verwendende Lastausgleichsfunktion. 

Wenn Sie einen Pool erstellen, sind zwei Felder erforderlich: 
 * **Name**: Ein Kurzname (Tag) für den Pool. Es sind nur alphanumerische Zeichen, Bindestriche und Unterstreichungszeichen zulässig. 
 * **Ursprünge**: Die Liste von Ursprüngen in diesem Pool. Der an diesen Pool umgeleitete Datenverkehr wird über alle Ursprünge ausgeglichen, die sich aktuell in einwandfreiem Zustand befinden, vorausgesetzt, der Pool selbst ist fehlerfrei. 

Zusätzliche optionale Felder:
 * **Beschreibung**: Eine lesbare Beschreibung des Pools. 
 * **Aktiviert**: Eine Angabe, ob dieser Pool aktiviert werden soll (Standardeinstellung). Inaktivierte Pools empfangen keinen Datenverkehr und sind von Statusprüfungen ausgeschlossen. Das Inaktivieren eines Pools führt dazu, dass für alle Lastausgleichsfunktionen ein Failover zum nächsten Pool durchgeführt wird, falls vorhanden (Standardeinstellung ist 'wahr'). 
 * **Schwellenwert für Ursprünge in einwandfreiem Zustand**: Die Mindestanzahl von Ursprüngen, die sich in einwandfreiem Zustand befinden müssen, damit dieser Pool Datenverkehr verarbeiten kann. Wenn die Anzahl der Ursprünge in einwandfreiem Zustand unter diese Zahl fällt, wird der Pool als fehlerhaft markiert und es wird ein Failover zum nächsten verfügbaren Pool durchgeführt (Standardwert ist '1'). 
 * **Regionen der Statusprüfung**: Region, die von der Statusprüfung überwacht wird. 
 * **Statusprüfung**: Statusprüfung für die Prüfung von Ursprüngen in diesem Pool (standardmäßig ist keine Statusprüfung festgelegt). 
 * **Benachrichtigungs-E-Mail**: Die E-Mail-Adresse, an die Statusbenachrichtigungen gesendet werden sollen. Bei dieser Adresse kann es sich um eine einzelne Mailbox oder um eine Mailing-Liste handeln. 

 ### Lastausgleichsfunktion hinzufügen

Lastausgleichsfunktionen helfen Ihnen, Ihren Proxy-Datenverkehr mithilfe einer Umlaufverteilung über mehrere Ursprungspools zu verteilen. 

Beim Erstellen einer Lastausgleichsfunktion sind die erforderlichen Felder folgende: 
 * **Name**: Der DNS-Hostname, der Ihrer Lastausgleichsfunktion zugeordnet werden soll. Wenn dieser Hostname bereits als DNS-Eintrag im IBM DNS vorhanden ist, hat die Lastausgleichsfunktion Vorrang und der DNS-Datensatz wird nicht verwendet. 
 * **Standardpools**: Eine Liste von Pool-IDs. Die Liste ist nach Failoverpriorität geordnet. Hier definierte Pools werden standardmäßig verwendet, oder wenn für eine bestimmte Region keine Regionspools konfiguriert sind. 

Optional können die folgenden Felder konfiguriert werden: 
 * **Proxy**: Leitet Datenverkehr über den IBM Performance and Metrics Service weiter. 
 * **Sitzungsaffinität**: Leitet Datenverkehr immer über dieselbe Instanz des Performance and Metrics Service weiter. Diese Option ist nur verfügbar, wenn ein Proxy aktiviert ist. 
 * **TTL**: Lebensdauer (Time to Live, TTL) des DNS-Eintrags für die von dieser Lastausgleichsfunktion zurückgegebene IP-Adresse. Diese Option gilt nur für Nicht-Proxy-Lastausgleichsfunktionen. Andernfalls nimmt sie standardmäßig den Wert `Automatisch` an. 
 * **Regionspools**: Zuordnung von Regions- oder Landescodes zu einer Liste von (nach Failoverpriorität sortierten) Pools für die gegebene Region. Alle nicht explizit definierten Regionen verwenden die Standardpools. 
