---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Bypass, header responses, brute-force login attempts

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Drosselungen
{:#cis-rate-limiting}

Drosselungen (nur Enterprise-Plan) schützen vor Denial-of-Service-Attacken, Brute-Force-Anmeldeversuchen und anderen Arten von missbräuchlichem Verhalten, das auf die Anwendungsebene zielt. 

Wählen Sie einen Regeltyp für die Drosselung aus: **Angepasste Regel** oder **Anmeldung schützen**

## Erstellen Sie eine angepasste Regel für die Drosselung
{:#create-a-custom-rate-limiting-rule}

Geben Sie einen Regelnamen ein, der Sie daran erinnert, was diese Regel tut. Dies ist ein optionales Feld. 

**Übereinstimmungskriterien für Datenverkehr** verwendet die Operation AND. Geben Sie eine URL ein, für die Sie eine Drosselung festlegen möchten. Nun führen Anforderungen von **derselben IP**, die die von Ihnen angegebene Anzahl an **Anforderungen pro Sekunde überschreiten** zum Auslösen der angegebenen Regel. 

Mit der Option **Erweiterte Kriterien** können Sie angeben, welche HTTP-Methoden, Headerantworten und Ursprungsantwortcodes die Übereinstimmungskriterien weiter einschränken sollen.  

Wählen Sie einen Wert aus dem Dropdownmenü **Methode** aus (ANY ist der Standardwert).  

Aktualisieren Sie **HTTP-Antwortheader**. Sie können auch **Antwortheader hinzufügen** auswählen, um Header einzuschließen, die von Ihrem Ursprungsserver zurückgegeben wurden.  

Wenn Sie über mehr als einen Header unter **HTTP-Antwortheader** verfügen, wird die boolesche Logik _AND_ angewendet. Wenn Sie einen Header von der Übereinstimmung ausschließen möchten, verwenden Sie die Option _Ungleich_. Außerdem muss jeder Header eine exakte Übereinstimmung aufweisen. Groß-/Kleinschreibung spielt hier keine Rolle.
{:note}

Geben Sie unter **Ursprungsantwortcode** den gültigen numerischen Wert für jeden HTTP-Antwortcode ein, der übereinstimmen soll. Wenn Sie zwei oder mehr Antwortcodes einschließen möchten, trennen Sie die einzelnen Werte durch ein Komma. Sie können z. B. `401, 403` eingeben, wenn nur die beiden Fehlercodes gezählt werden sollen. 

### Antwort konfigurieren
{:#rate-limiting-configure-response}

Wählen Sie aus den aufgelisteten Aktionen aus und geben Sie das Zeitlimitintervall an. In diesem Fall bezieht sich das Zeitlimit ausschließen auf den Zeitraum, in dem die Aktion ausgeführt wird. Ein Zeitlimit von 60 Sekunden bedeutet, dass die Aktion für 60 Sekunden angewendet wird. 

|Aktion|Beschreibung|
|------|------------|
|Blockieren | Gibt den Fehler 429 aus, wenn der Schwellenwert überschritten wird.|
|Sicherheitsabfrage ausgeben | Der Benutzer muss eine Google-reCaptcha-Abfrage durchlaufen, bevor er fortfahren kann. Wenn dies erfolgreich war, wird die Anforderung akzeptiert. Andernfalls wird die Anforderung blockiert.| 	
|JS-Abfrage |	Der Benutzer muss eine Javascript-Abfrage durchlaufen, bevor er fortfahren kann. Wenn dies erfolgreich war, wird die Anforderung akzeptiert. Andernfalls wird die Anforderung blockiert.|Simulieren |Sie könne diese Option zum Testen Ihrer Regel verwenden, bevor Sie sie auf andere Optionen in Ihrer Liveumgebung anwenden. 

**Erweiterte Antwort**

Geben Sie den Antworttyp an, wenn ein Regelschwellenwert überschritten wurde.  

### Umgehung
{:#rate-limiting-bypass}

Mit einer Umgehung können Sie das Äquivalent einer Whitelist oder eine Ausnahme für eine Reihe von URLs erstellen. Für diese URLs werden keine Aktionen ausgelöst, auch wenn die Regel für die Drosselung übereinstimmt. 

## Anmeldung schützen
{:#rate-limiting-protect-login}

Das Schützen der Anmeldung erstellt eine Standardregel, die die Anmeldeseite gegen Brute-Force-Angriffe schützt. Clients, die versuchen sich mehr als 5 Mal innerhalb von 5 Minuten anzumelden, werden für 15 Minuten gesperrt.  

Geben Sie einen Namen für die Regel und die Anmelde-URL ein. 
