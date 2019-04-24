---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: edge functions beta, edge functions

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Edge-Funktionen (Beta)
{: #edge-functions}

Mit den Edge-Funktionen von CIS können Sie neue Anwendungen erstellen oder vorhandene Anwendungen verändern, ohne die Infrastruktur mithilfe einer serverlosen Ausführungsumgebung konfigurieren oder warten zu müssen. Edge-Funktionen können definiert und auf die Cloud-Edge hochgeladen werden, um Anforderungen zu verarbeiten, bevor sie den Ursprung erreichen. Die Edge-Funktionen von CIS können verwendet werden, um HTTP-Anforderungen und -Antworten zu ändern, parallele Anforderungen zu stellen oder Antworten vom Cloud-Edge zu generieren. 

## Funktionsweise von Edge-Funktionen
{: #how-edge-functions-work}

Edge-Funktionen ordnen **Aktionen** auf Grundlage einer definierten Domäne zu URIs zu. Diese Zuordnung wird als **Auslöser** bezeichnet. Auf Ihrer Site eingehende Anforderungen werden am Edge der Cloud abgefangen und mit den Triggern in Ihrem Konto oder in Ihrer Domäne abgeglichen. Wenn die Anforderungs-URL mit dem URI des Auslösers übereinstimmt, wird die Aktion, die dem Auslöser zugeordnet ist, ausgeführt. 

Edge-Funktionen werden auf den [Service-Workern](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API), die in modernen Web-Browsern zur Verfügung stehen, modelliert und verwenden nach Möglichkeit dieselbe API. 

Die Service-Worker-API ermöglicht Ihnen, eine beliebige Anforderung abzufangen, die an Ihre Site gestellt wird. Sobald Ihr JavaScript die Anforderung bearbeitet, können Sie auswählen, eine beliebige Anzahl an Unteranforderungen an Ihre oder andere Sites zu stellen und schließlich eine gewünschte Antwort an den Besucher Ihrer Site zurückzugeben. 

Im Gegensatz zu standardmäßigen Service-Workern werden Edge-Funktionen auf CIS-Edge-Servern ausgeführt und nicht im Browser der Benutzer. Dies bedeutet, dass Sie darauf vertrauen können, dass Ihr Code in einer vertrauenswürdigen Umgebung ausgeführt wird, in der er nicht von schädlichen Clients umgangen werden kann. Das heißt auch, dass Benutzer keinen modernen Browser verwenden müssen, der Service-Workers unterstützt. Sie können sogar Anforderungen von API-Clients abfangen, die gar keine Browser sind. 

Intern verwenden Edge-Funktionen dieselbe JavaScript-Engine Version 8, die im Google Chrome-Browser verwendet wird, um Worker in Ihrer Infrastruktur auszuführen. Version 8 kompiliert Ihren JavaScript-Code dynamisch in ultraschnellen Maschinencode und erhöht so die Leistung enorm. Dies ermöglicht Ihrem Code die Ausführung in Mikrosekunden und der Edge-Funktion die Ausführung von vielen Tausend Scripts pro Sekunde. 

Edge-Funktionen verwenden zwar Version 8 jedoch nicht Node.js. Die innerhalb der JavaScript-APIs verfügbaren Worker werden von uns direkt implementiert. Die direkte Arbeit mit Version 8 ermöglicht eine effizientere Ausführung des Codes unter Einhaltung der erforderlichen Maßnahmen für die Sicherheit der Kunden und der Infrastruktur. 


## Aktionen
{: #edge-functions-actions}

Aktionen werden in JavaScript geschrieben und benötigen einen Ereignislistener, um auf ein Auslöserereignis zu reagieren. Aktionen haben keine Auswirkungen auf Ihren Datenverkehr, es sei denn ein Auslöser verwendet sie. 

### Enterprise-Plan versus Standardplan
{: #edge-functions-enterprise-v-standard-plans}

Standardpläne weisen maximal eine Aktion auf. Der Aktion ist ein Name zugeordnet, der mit Ihrem Domänennamen identisch ist. Sie können Ihre Aktionen durch Hochladen einer anderen Datei ersetzen oder Ihre Aktion mithilfe des Codeeditors aktualisieren. Das Hochladen einer anderen Datei entfernt die vorhandene Aktion. 

Enterprise-Pläne können eine unbegrenzte Anzahl an Scripts hochladen. Diesen können eindeutige Namen zugewiesen werden. 

### Aktionen erstellen
{: #edge-functions-create-actions}

Wählen Sie **Erstellen** aus, um eine Aktion mit dem Codeeditor hinzuzufügen. Geben Sie bei Enterprise-Plänen einen Namen für Ihre Aktion ein. Bei Standardplänen kann der Name nicht bearbeitet werden und entspricht dem Namen Ihrer Domäne. Nach dem Hinzufügen Ihres JavaScript-Code wählen Sie **Speichern** aus, um Ihre Aktion zu erstellen. 

### Aktionen hochladen
{: #edge-functions-upload-actions}

Verwenden Sie die Schaltfläche **Hochladen**, um eine JavaScript-Datei hochzuladen. Bei Enterprise-Plänen entspricht der Name der Aktion dem Dateinamen. Bei Standardplänen ist der Aktionsname auf den Namen Ihrer Domäne festgelegt. 

Das Hochladen oder Erstellen einer Aktion mit demselben Namen wie eine vorhandene Aktion führt dazu, dass die vorhandene Aktion überschrieben wird. Benennen Sie die Aktionsdatei vor dem Hochladen um oder geben Sie einen eindeutigen Namen beim Erstellen in der Texteingabe ein, um dieses Verhalten zu vermeiden.
{:note}

### Aktionen bearbeiten
{: #edge-functions-edit-actions}

Das Auswählen einer Aktion öffnet die Aktion im Editor zur Bearbeitung. Immer wenn Sie Ihre Änderungen speichern, wird die Aktion auf den Edge der Cloud hochgeladen. Nach dem Hochladen, wählen Sie **Speichern** aus. Wenn die Aktion verwendet wird, werden die Änderungen sofort wirksam.  

### Löschaktionen
{: #edge-functions-delete-actions}

Löschen Sie eine Aktion, indem Sie auf das Symbol für **Löschen** in der Tabelle **Aktionen** klicken. Eine Aktion kann nicht gelöscht werden, wenn Sie noch verwendet wird. Um eine Aktion zu löschen, entfernen Sie sie zuerst aus den Auslösern. Die Spalte für die **Verwendung** zeigt die Anzahl der Auslöser an, die zu dieser Aktion gehören. Das Löschen kann nicht rückgängig gemacht werden. 


### Zugehörige Auslöser
{: #edge-functions-associated-triggers}

Fügen Sie einen Auslöser hinzu und ordnen Sie ihn einer Aktion zu.

### Bekannte Einschränkungen bei Edge-Funktionen
{: #edge-functions-known-limitations}

Das Hochladen einer Aktion mit demselben Namen wie eine vorhandene Aktion. Die vorhandene Aktion wird überschrieben. Benennen Sie die Aktionsdatei um, bevor Sie sie hochladen, um dieses Verhalten zu vermeiden. 


## Auslöser
{: #triggers}

### Informationen zu Auslösern
{: #about-triggers}

Auslöser (Routes) bestimmen die Weiterleitung des Domänendatenverkehrs an Aktionen. Auslöser ordnen bestimmte URL-Muster auf Grundlage einer Domäne im Konto zu einer vordefinierten Aktion zu. Die URL muss die Domäne enthalten, kann aber entweder als Präfix der Domäne oder am Ende des Pfades Platzhalterzeichen enthalten. Wenn im Muster kein Pfad angegeben ist, wird ein Schrägstrich `/` implizit hinzugefügt. Das URL-Muster kann keine Infixplatzhalterzeichen oder Abfrageparameter enthalten. 

Sie müssen eine Domäne hinzufügen, um Auslöser hinzuzufügen. Sie können Auslöser hinzufügen, ohne über Aktionen zu verfügen. 

### Auslöser hinzufügen
{: #add-triggers}

Wechseln Sie auf die Registerkarte **Auslöser** und klicken Sie auf **Auslöser hinzufügen**. Geben Sie ein URL-Muster ein und wählen Sie eine Aktion aus der Liste der vorhandenen Aktionen aus.  

Für eine Aktion können Sie auch **Edge-Funktionen vermeiden** auswählen. Dadurch kann der Pfad des Auslösers aktiv bleiben und es wird gleichzeitig vermieden, dass Edge-Funktionen verwendet werden. Beispiel: Es gibt eine Aktion mit dem Namen `my-function` und einen Auslöser mit dem Pfad `beta.cistest-load.com/*`. Wenn der Pfad `beta.cistest-load.com/data` die Aktion `my-function` nicht verwenden soll, erstellen Sie einen anderen Auslöser mit dem Pfad `beta.cistest-load.com/data` und der Option **Edge-Funktionen vermeiden**. Dadurch kann der Pfad `beta.cistest-load.com/data` aktiv bleiben, ohne dass die Aktion `my-function` verwendet wird.

### Auslöser bearbeiten
{: #edit-triggers}

Aktualisieren Sie einen Auslöser mit den Menüoptionen in der Tabellenzeile für einen ausgewählten Auslöser. Nach dem Hochladen wählen Sie **Speichern** aus.

### Auslöser löschen
{: #delete-triggers}

Löschen Sie einen Auslöser mithilfe der Menüoption in der Tabellenzeile für einen ausgewählten Auslöser. Diese Aktion kann nicht rückgängig gemacht werden.


## Anwendungsfälle
{: #edge-functions-use-cases-examples}

Diese Beispiele dienen nur zu Demonstrationszwecken und sind nicht für die Produktion vorgesehen:
{:important}
* [A/B-Test](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#ab-testing)
* [Antwortheader hinzufügen](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#add-response-header)
* [Mehrere Anforderungen zusammenfassen](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#aggregate-multiple-requests)
* [Bedingtes Routing](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#conditional-routing)
* [Hot Link-Schutz](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#hot-link-protection)
* [Ursprungslose Antworten](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#originless-responses)
* [Beitragsanforderungen](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#post-requests)
* [Cookie setzen](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#setting-cookies)
* [Signierte Anforderungen](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#signed-requests)
* [Antworten streamen](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#streaming-responses)
