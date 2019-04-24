---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Access Group Writer role, CIS instance, IAM

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# IAM und CIS
{:#iam-and-cis}

IBM Cloud Internet Services (CIS) nutzt IAM für die Autorisierung und Authentifizierung. 

Wenn Sie niemanden zu Ihrer CIS-Instanz hinzufügen möchten, können Sie diese Seite ignorieren.
{:note}

Schränken Sie den Zugriff durch die folgenden drei CIS-Funktionsbereiche auf Grundlage der Navigationsstruktur ein:  
* Zuverlässigkeit - beispielsweise DNS, GLB
* Sicherheit - beispielsweise Zertifikate, IP-Firewallregeln und Drosselung
* Leistung - beispielsweise Caching und Routing

In diesem Abschnitt wird schrittweise erläutert, wie Sie eine differenzierte Zugriffssteuerung für Ihre Instanz zur Verfügung stellen können. 

## Rollen
{:#iam-and-cis-roles}

Verwenden Sie die folgenden drei Rollen, um IAM zu nutzen:
* Leser - Kann Informationen zu Instanz und Domäne abrufen
* Schreibberechtigter - Kann Änderungen an der vorhandenen Konfiguration vornehmen
* Manager - Kann Instanzen, Domänen und Konfigurationen erstellen oder löschen

## Zugriffsgruppen und Benutzer
{:#iam-and-cis-access-groups-users}

Eine Richtlinie kann einem Benutzer direkt zugeordnet werden oder einer Zugriffsgruppe.
Wir empfehlen die Zuordnung zu einer Zugriffsgruppe, um die Anzahl der erstellten Richtlinien zu minimieren und den Aufwand bei der Verwaltung dieser Richtlinien zu reduzieren. 

## Cache
{:#iam-and-cis-cache}

Wir speichern die Autorisierungsergebnisse im Cache zwischen und verwenden den Cache, um eine Entscheidung zu treffen, wenn dieselbe Anforderung erneut eingeht. Nachdem der Cache seine Lebensdauer (10 Minuten) erreicht hat, verfällt er. 

## Bewährte Verfahren
{:#iam-and-cis-best-practices}

1. Anstatt eine Richtlinie zu ändern, löschen Sie die vorhandene Richtlinie und erstellen Sie dann eine neue Richtlinie.

## Szenarien
{:#iam-and-cis-scenarios}

Dieser Abschnitt erläutert schrittweise die unterschiedlichen Beispiele für Zugriffsrichtlinien, die über CIS erstellt werden.  

### Domänenebene mit dem Typ `config`
{:#iam-and-cis-scenarios-domain-level}

#### Zugriff auf eine einzelne Domäne mit `Sicherheitskonfiguration` in einer Zugriffsgruppe 
##### Rolle als Schreibberechtigter

Bob hat eine CIS-Instanz, `cis-test-instance`, und zwei Domänen; `bob.com` und `bob-ibm.com`.
Bob möchte allen Sicherheitsentwicklern (sec-group) im Unternehmen nur in der **Sicherheitskonfiguration** von **`bob.com`** Zugriff auf die Rolle als Schreibberechtigter erteilen.

Die folgenden Schritte zeigen, wie eine IAM-Richtlinie erstellt wird, die dieses Szenario ermöglicht. 

Nachdem Bob sich bei der Instanz 'cis-test-instance' angemeldet hat, führt er folgende Schritte aus: 
1. Er klickt auf die Registerkarte **Konto > Zugriff** in der Navigationsleiste.
1. Er wählt die **Zugriffsgruppe** - **sec-group** aus, für die Zugriff erteilt werden soll. 
1. Er wählt **`bob.com`** aus.
1. Er wählt die Rolle **Schreibberechtigter** aus. 
1. Er wählt die Option **Sicherheitskonfiguration** aus. 
1. Er klickt auf **Richtlinie erstellen**

Auf der Registerkarte 'Verwalten':
Die folgenden Richtlinien werden für **sec-group** erstellt:

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e

Service Instance 
    name: cis-test-instance  
    id: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9 
Domain 
    name: bob.com
    id: 4b23ec772965f672f96f05670e36827e 
Config Type
    cfgType: security
```

Jetzt hat 'sec-group' Zugriff, um nur `bob.com` anzuzeigen und Werte bezüglich der Sicherheit zu ändern.  

##### Aktualisierung von der Rolle als Schreibberechtigter auf die Rolle für Managementaufgaben für eine Zugriffsgruppe

Wenn Bob die Rolle von 'sec-group' von 'Schreibberechtigter' auf 'Manager' aktualisieren möchte, muss er die vorhandene Richtlinie löschen.  
1. Wechseln Sie zur Registerkarte **IAM verwalten > Zugriffsgruppen > sec-group > Zugriffsrichtlinien**
1. Löschen Sie die folgende Richtlinie 
  ```
  Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
  ```

Jetzt muss Bob eine neue Richtlinie erstellen.  
1. Klicken Sie auf die Registerkarte **Konto > Zugriff** in der Navigationsleiste. 
1. Wählen Sie die **Zugriffsgruppe** - **sec-group** aus, für die Zugriff erteilt werden soll. 
1. Wählen Sie **`bob.com`** aus.
1. Wählen Sie die Rolle **Manager** aus. 
1. Wählen Sie die Option **Sicherheitskonfiguration** aus.
1. Klicken Sie auf **Richtlinie erstellen**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

Wenn die vorhandene Richtlinie (Schreibberechtigter) nicht gelöscht wird, dann schlägt das Erstellen einer Richtlinie für Manager fehl. 

##### Konfiguration aktualisieren, um Leistung zusammen mit Sicherheit einzubeziehen

Wenn Bob der sec-group mit der Managerrolle zusammen mit der Sicherheit auch Zugriff auf die Leistungskonfiguration auf `bob.com` erteilen möchte, muss er folgende Schritte ausführen: 
1. Er klickt auf die Registerkarte **Konto > Zugriff** in der Navigationsleiste.
1. Er wählt die **Zugriffsgruppe** - **sec-group** aus, für die Zugriff erteilt werden soll. 
1. Er wählt **`bob.com`** aus.
1. Er wählt die Rolle **Manager** aus. 
1. Er wählt die Option **Leistungskonfiguration** aus. 
1. Er klickt auf **Richtlinie erstellen**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: performance, domainId: 4b23ec772965f672f96f05670e36827e

```

#### Zugriff auf alle Domänen mit der `Sicherheitskonfiguration`

Wenn Sie Sicherheitsaktionen für `bob.com` und `bob-ibm.com` aus dem vorherigen Beispiel bereitstellen möchten, müssen Sie eine neue Richtlinie erstellen, indem Sie die Schritte für jede Domäne wiederholen. Der einzige Unterschied besteht in der Auswahl der entsprechenden Domäne für jede Richtlinie. 

1. Klicken Sie in der Navigationsleiste auf die Registerkarte **Konto > Zugriff**. 
1. Wählen Sie die **Zugriffsgruppe** - **sec-group** aus, für die Zugriff erteilt werden soll. 
1. Wählen Sie **`bob.com`** aus.
1. Wählen Sie die Rolle **Manager** aus. 
1. Wählen Sie die Option **Sicherheitskonfiguration** aus.
1. Klicken Sie auf **Richtlinie erstellen**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

1. Klicken Sie auf die Registerkarte **Konto > Zugriff** in der Navigationsleiste. 
1. Wählen Sie die **Zugriffsgruppe** - **sec-group** aus, für die Zugriff erteilt werden soll. 
1. Wählen Sie **`bob-ibm.com`** aus.
1. Wählen Sie die Rolle **Manager** aus. 
1. Wählen Sie die Option **Sicherheitskonfiguration** aus.
1. Klicken Sie auf **Richtlinie erstellen**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 7ad7341865246f5df482ad9f76aafb5a
```



#### Zugriff auf eine einzelne Domäne mit der `Sicherheitskonfiguration` und der `Zuverlässigkeitskonfiguration`

Bob hat eine CIS-Instanz, 'cis-test-instance', und zwei Domänen: `bob.com` und `bob-ibm.com`.
Bob möchte Tony Zugriff mit der Rolle als Schreibberechtigter nur für die **Sicherheits- und Zuverlässigkeitsaktionen** auf**`bob-ibm.com`** erteilen.

Nachdem Bob sich bei der Instanz 'cis-test-instance' angemeldet hat, führt er folgende Schritte aus: 
1. Er klickt auf die Registerkarte **Konto > Zugriff** in der Navigationsleiste.
1. Er wählt **Tony** aus, dem er den Zugriff erteilen möchte. 
1. Er wählt **`bob-ibm.com`** aus.
1. Er wählt die Rolle **Schreibberechtigter** aus. 
1. Er wählt das Markierungsfeld für die Option **Sicherheit und Zuverlässigkeit** aus 
1. Er klickt auf **Richtlinie erstellen**

Dadurch werden im Back-End zwei Richtlinien für jeden Konfigurationstyp erstellt. 

### Domänenebene mit allen Konfigurationstypen
{:#iam-and-cis-scenarios-domain-level-all-config-types}

Bob möchte Tony auf Domänenebene Lese-/Schreib-/Verwaltungszugriff erteilen.

#### Schreibzugriff (Write)
Nachdem Bob sich bei der Instanz 'cis-test-instance' angemeldet hat, führt er folgende Schritte aus: 
1. Er klickt auf die Registerkarte **Konto > Zugriff** in der Navigationsleiste.
1. Er wählt **Tony** aus, dem er den Zugriff erteilen möchte. 
1. Er wählt **`bob.com`** aus.
1. Er wählt die Rolle **Schreibberechtigter** aus. 
1. Er überprüft alle Felder für den CIS-Funktionsbereich. 
1. Er klickt auf **Richtlinie erstellen**

```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### Verwaltungszugriff (Manager)
Nachdem Bob sich bei der Instanz 'cis-test-instance' angemeldet hat, führt er folgende Schritte aus: 
1. Er klickt auf die Registerkarte **Konto > Zugriff** in der Navigationsleiste.
1. Er wählt **Tony** aus, dem er den Zugriff erteilen möchte. 
1. Er wählt **`bob.com`** aus.
1. Er wählt die Rolle **Manager** aus. 
1. Er überprüft alle Felder für den CIS-Funktionsbereich. 
1. Er klickt auf **Richtlinie erstellen**

```
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### Lesezugriff (Reader)
Nachdem Bob sich bei der Instanz 'cis-test-instance' angemeldet hat, führt er folgende Schritte aus: 
1. Er klickt in der Navigationsleiste auf die Registerkarte **Konto > Zugriff**.
1. Er wählt **Tony** aus, dem er den Zugriff erteilen möchte. 
1. Er wählt **`bob.com`** aus.
1. Er wählt die Rolle **Leser** aus. 
  1. Alle Kontrollkästchen sind bereits vorab ausgewählt, um anzuzeigen, dass der Benutzer *mindestens* Lesezugriff auf die gesamte Domäne benötigt und ihm kein Teilzugriff auf eine Domäne erteilt werden kann. 
1. Klicken Sie auf **Richtlinie erstellen**


```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

### Instanzebene - alle Ihre Domänen
{:#iam-and-cis-scenarios-instance-level}

Diese Richtlinie muss über die IAM-Verwaltungsseite erstellt und verwaltet werden.

Der Zugriff auf Instanzebene bedeutet, dass Bob Tony die Berechtigung für Instanz 1 der 10 vorhandenen Instanzen erteilen kann.
Tony kann alle Domänen in dieser Instanz anzeigen.  

Wenn Bob einem Schreibberechtigten oder einem Manager Zugriff auf eines der folgenden Elemente erteilen möchte, muss er den Zugriff auf Instanzebene erteilen: 
* Lastausgleichsfunktion - Pools und Statusprüfungen
* Firewallzugriffsregeln
* Worker 

Erstellen Sie auf der Seite zum Verwalten von IAM eine Richtlinie für Schreibberechtigte/Manager in der Serviceinstanz cis-test-instance.

```
Manager	Resource	Only service instance cis-test-instance of CIS 	
oder
Writer	Resource	Only service instance cis-test-instance of CIS 	
```

## IAM-Richtlinien verwalten 
{:#manage-iam-policies}

CIS ermöglicht es Benutzern, IAM-Richtlinien zu erstellen. Aber die Verwaltung muss über die [IAM-Seite] erfolgen: https://{DomainName}/iam#/overview.

## Anmerkung
{:#iam-note}
Für jede Richtlinie, die auf der Zugriffsseite in der CIS-Instanz erstellt wurde, werden im Gegenzug 2-3 Richtlinien erstellt. 

1. Die Anzeigeberechtigten-Rolle des Plattformzugriffs für die Serviceinstanz ermöglicht es dem hinzugefügten Benutzer, die Instanz im Dashboard anzuzeigen. 

**Beispiel**
```
Viewer	Resource	Only service instance cis-instance-instance of CIS 	
```

2. Der Lesezugriff auf Domänenebene ist die Mindestanforderung für den differenzierten Zugriff auf die Arbeit. 

**Beispiel**
```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
```
3. Die Richtlinie, die Sie mit dem vorhandenem Konfigurationstyp erstellt haben.

**Beispiel**
```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

**FAQ**
1. Wie erhalte ich meine Serviceinstanz-ID?

   Kopieren Sie die CRN auf der Übersichtsseite.
   ```
   crn:v1:test:public:internet-svcs:global:a/2c38d9a9913332006a27665dab3d26e8:836f33a5-d3e1-4bc6-876a-982a8668b1bb::
   ```
   Der letzte Teil der CRN ist Ihre Serviceinstanz: `836f33a5-d3e1-4bc6-876a-982a8668b1bb`.
   
   oder
   
   Klicken Sie in der Ressourcenliste auf der Hauptseite auf die Zeile mit der CIS-Instanz und kopieren Sie die GUID für die Serviceinstanz-ID. 

2. Ich habe eine Richtlinie gelöscht, aber der Benutzer, dem ich die Richtlinie übergeben habe, kann die Aktion immer noch ausführen! 

   CIS speichert Berechtigungsergebnisse im Cache zwischen und die Lebensdauer (TTL) für den Cache beträgt 10 Minuten.   
   
   Wenn IAM berechtigt, werden die Zugriffsrichtlinien aus der Zugriffsgruppe und die eigenen Richtlinien des Benutzers verwendet, bevor eine Entscheidung getroffen wird. 

3. Welche Berechtigungen sind für die Bereitstellung von Internet-Service erforderlich? 

   Wenn Sie nicht in der Lage sind, eine Ressource zu erstellen und einer Ressourcengruppe hinzuzufügen, dann haben Sie es in aller Regel mit einem Zugriffsproblem zu tun. Sie müssen in der Ressourcengruppe selbst mindestens über die Rolle des Anzeigeberechtigten verfügen und für den Service im Konto mindestens über die Bearbeiterrolle. Sie können den Kontoadministrator bitten, den Ihnen zugeordneten Zugriff im Konto zu überprüfen. Weitere Informationen finden Sie unter [Zugriff auf Ressourcen verwalten](/docs/iam?topic=iam-iammanidaccser). 
   
 
