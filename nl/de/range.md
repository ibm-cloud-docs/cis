---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: range application, tls encryption, ddos protection, global tcp proxy

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Range
{:#cis-range}

Die Funktion Range ergänzt ein beliebiges TCP-basiertes Protokoll um DDoS-Schutz, Lastausgleich und Inhaltsbeschleunigung.
Range ist ein globaler TCP-Proxy, der auf den Edge-Knoten von CIS/Cloudflare ausgeführt wird.  

Range kann wie folgt verwendet werden:  
* Schutz Ihrer TCP-Ports und -Protokolle vor Attacken der **Ebene 3 und 4 DDoS**. 
* Reduzierung der Möglichkeit von Angreifern, sensible Daten durch Aktivieren der **TLS-Verschlüsselung** auszuspionieren und zu stehlen.
* Integration der CIS IP-Firewall, wodurch IP-Adressen oder ganze IP-Bereiche blockiert oder abgefragt werden können, bevor Sie Ihre TCP-Services erreichen.  
* Konfiguration von Lastausgleichsfunktionen mit TCP-Statusprüfungen, Funktionsübernahme und Lenkungsrichtlinien, die festlegen, wo der Datenverkehr fließt. 

## Einführung in Range
{:#getting-started-with-range}

Range ist nur für Enterprise-Kunden verfügbar und ist gebührenpflichtig. Die Abrechnung erfolgt nach Nutzung der Bandbreite.
{:note}

### Anwendung hinzufügen
{:#range-add-an-application}
Führen Sie die folgenden Schritte aus, um eine Anwendung  hinzuzufügen. 

1. Navigieren Sie zu **Sicherheit > Range**.
1. Klicken Sie auf die Schaltfläche **Anwendung hinzufügen** 
1. Geben Sie den Anwendungsnamen im ersten Eingabefeld ein. Ihre Anwendung wird einem DNS-Namen in Ihrer CIS-Domäne zugeordnet. 
1. Geben Sie den Edge-Port im nächsten Eingabefeld ein. Dieser Port ist nun für eingehende Verbindungen zu diesen Adressen empfangsbereit. Verbindungen zu diesen Adressen werden an Ihren Ursprung weitergeleitet. (Die Weiterleitung wird auf allen Ports unterstützt. Eine Ausnahme bildet nur Port 21.)
1. Geben Sie im Abschnitt für den Ursprung die Ursprungs-IP und den Port Ihrer TCP-Anwendung ein. Sie können auch eine vorhandene Lastausgleichsfunktion auswählen. 
1. Aktivieren Sie eine IP-Firewall. Wenn diese Option aktiviert ist, werden Firewallregeln mit der Aktion "block" (Blockieren) oder "whitelist" (Whitelist) für diese Anwendung erzwungen. Länder- oder ASN-basierte Regeln werden noch nicht unterstützt. 
1. Aktivieren Sie das Proxy-Protokoll, wenn Sie über einen integrierten Proxy verfügen, der das PROXY-Protokoll Version 1 unterstützt. Diese Funktion ist nützlich, wenn Sie einen Service ausführen, der Kenntnisse der tatsächlichen Client-IP erfordert. In den meisten Fällen sollte diese Einstellung inaktiviert bleiben. 
1. Klicken Sie auf **Bereitstellung**.

Das Proxy-Protokoll stellt jeder Verbindung einen Header voran, der die IP-Adresse und den Port des Client berichtet. Ein Proxy-Protokollheader hat das folgende Format: 
  * PROXY_STRING + single space + INET_PROTOCOL + single space + CLIENT_IP + single space + PROXY_IP + single space + CLIENT_PORT + single space + PROXY_PORT + "\r\n"
  * Es folgt ein Beispiel für eine Proxy-Protokollzeile für eine IPv4-Adresse:
    `PROXY TCP4 192.0.2.0 192.0.2.255 42300 443\r\n`
  * Es folgt ein Beispiel für eine Proxy-Protokollzeile für eine IPv6-Adresse:
    `PROXY TCP6 2001:db8:: 2001:db8:ffff:ffff:ffff:ffff:ffff:ffff 42300 443\r\n`
   
Die Bereitstellung einer Range-Anwendung beinhaltet zusätzliche Kosten, die auf der von der App genutzten Bandbreite beruhen.
{:note}

Ihre Anwendung ist nun in einer Kachel mit den folgenden Eigenschaften sichtbar:
  * Anwendungsname
  * Edge-Port
  * Ursprung & Port
  * Verbindungen der letzten Stunde (pro Minute abgefragt)
  * Durchsatz der letzten Stunde (pro Minute abgefragt)
  * Überlaufmenü (obere rechte Ecke), das Folgendes ermöglicht:  
    * Bearbeiten der Anwendung
    * Anzeigen von Metriken für die angegebene Anwendung
    * Löschen der Anwendung 
    
Wenn eine Range-Anwendung erstellt wird, wird ihr eine eindeutige IPv4- und IPv6-Adresse zugeordnet. Diese IP-Adressen sind nicht statisch und können möglicherweise geändert werden. Sie können die zugeordneten IP-Adressen mithilfe von DNS bestimmen. Der DNS-Name gibt immer die IP-Adresse zurück, die der Anwendung zugeordnet wurde.      
    
### Metriken anzeigen
{:#range-view-metrics}
Ihre Anwendung ist nun bereit, TCP-Datenverkehr über Cloudflare/CIS weiterzuleiten.

Navigieren Sie zu **Metriken > Range**, um Ihre Anzahl an Verbindungen zu Anwendungen und den Durchsatzdatenverkehr anzuzeigen.
Die Grafiken zeigen Metriken für bis zu 10 Anwendungen an.
{:note}

Anwendungsmetriken können über die Diagrammtaste oder durch Klicken auf die Schaltfläche **Anwendungen auswählen** umgeschaltet werden. Der Zeitrahmen der Metrikdaten kann mithilfe des Dropdown-Menüs geändert werden. 

## Range AppTiles
{:#range-apptiles}
Nach dem Erstellen einiger Apps, wird die Seite **Sicherheit > Range** mit Anwendungskacheln gefüllt. Die Anwendungskacheln enthalten die folgenden Informationen: 
* Anwendungsname
* Edge-Port
* Ursprung & Port
* Verbindungen der letzten Stunde (pro Minute abgefragt)
* Durchsatz der letzten Stunde (pro Minute abgefragt)


Die Anwendungskachel enthält auch ein Überlaufmenü in der oberen Ecke (3 Punkte). Das Überlaufmenü stellt den Benutzern die folgenden Optionen zur Verfügung:
* Bearbeiten der Anwendung
* Anzeigen von Metriken für die angegebene Anwendung
  * Der Benutzer wird auf die Seite **Metriken > Range** geleitet, die nur die Metriken für diese Anwendung anzeigt. 
* Löschen der Anwendung


## API-Verwendungsbeispiele
{:#range-api-usage-examples}
Dies sind Beispiele zum Erstellen und Auflisten von Anwendungen mithilfe von Range.

### Eine Range-App erstellen
{:#create-range-app}
Es gibt zwei Möglichkeiten, einen Ursprung in einer Range-App zu bezeichnen:
1. Ursprungs-IP - mit dem Parameter `origin_direct`
2. Lastausgleichsfunktion - mit den Parametern `origin_dns` und `origin_port`

**Anforderung:**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_direct":["tcp://172.0.2.1:22"],"proxy_protocol":true,"ip_firewall":true}'

```
**Antwort:**
```
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_direct": [
            "tcp://172.0.2.1:22"
        ],
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:33:09.190606Z",
        "modified_on": "2019-01-09T17:33:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```

**Anforderung:**
```
curl -X POST \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps \
  -H 'X-Auth-User-Token: <token>' \
  -d '{"protocol":"tcp/22","dns":{"type":"CNAME","name":"ssh.example.com"},"origin_dns": {"name": "test"},"proxy_protocol":true,"ip_firewall":true, "origin_port": 43}'

```
**Antwort:**
```
{
    "result": {
        "id": "4f70c3d4f20576b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_dns": {
          "name": "test"
        },
        "origin_port": 43,
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:39:09.190606Z",
        "modified_on": "2019-01-09T17:39:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}
```

**DNS-Name:** Ihre Anwendung ist einem DNS-Namen in Ihrer Domäne zugeordnet. 

**Protokoll/Edge-Port:** Dies ist der Port, auf dem Ihre Anwendung ausgeführt wird. Verbindungen zu diesen Adressen werden zu Ihrem Ursprung weitergeleitet. 

**Ursprung direkt:** Dies ist die IP, an der Ihre Anwendung ausgeführt wird, und der Port, den Sie für den Fluss des Datenverkehrs vom Edge zu Ihrem Ursprung vorgesehen haben. 

**IP-Firewall:** Wenn diese Option aktiviert ist, werden Firewallregeln mit einer Blockierungsaktion für diese Range-Anwendung erzwungen. 

**Proxy-Protokoll:** Aktivieren Sie diese Option, wenn Sie über einen integrierten Proxy verfügen, der PROXY-Protokoll Version 1 unterstützt. In den meisten Fällen sollte diese Einstellung inaktiviert bleiben. 

**Ursprungs-DNS:** Dies ist der Namen der Lastausgleichsfunktion, die Sie als Ursprung festlegen möchten. 

**Ursprungsport:** Dies ist der Port Ihres Service.  

### Alle Apps auflisten
{:#range-list-all-apps}

**Anforderung:**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps
```

**Antwort:**
```
{
    "result": [
        {
            "id": "4f70c3d4f20546b79135b898295e8093",
            "protocol": "tcp/22",
            "dns": {
                "type": "CNAME",
                "name": "ssh.example.com"
            },
            "origin_direct": [
                "tcp://172.0.2.1:22"
            ],
            "ip_firewall": true,
            "proxy_protocol": true,
            "created_on": "2019-01-09T17:33:09.190606Z",
            "modified_on": "2019-01-09T17:33:09.190606Z"
        }
    ],
    "success": true,
    "errors": [],
    "messages": []
}
```

### Liste einer bestimmten Range-App
{:#range-list-a-specific-range-app}
**Anforderung:**
```
curl -X GET \
  https://api.cis.cloud.ibm.com/v1/<url-encoded-crn>/zones/<zone-d>/range/apps/4f70c3d4f20546b79135b898295e8093
```

**Antwort:**
App unter Verwendung der Ursprungs-IP
```
{
    "result": {
        "id": "4f70c3d4f20546b79135b898295e8093",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_direct": [
            "tcp://172.0.2.1:22"
        ],
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-09T17:33:09.190606Z",
        "modified_on": "2019-01-09T17:33:09.190606Z"
    },
    "success": true,
    "errors": [],
    "messages": []
} 
```

App unter Verwendung der Lastausgleichsfunktion
```
{
    "result": {
        "id": "555359036e7f4acc82d69b916f62caba",
        "protocol": "tcp/22",
        "dns": {
            "type": "CNAME",
            "name": "ssh.example.com"
        },
        "origin_dns": {
            "name": "test_update"
        },
        "origin_port": 76,
        "ip_firewall": true,
        "proxy_protocol": true,
        "created_on": "2019-01-10T22:26:47.167008Z",
        "modified_on": "2019-01-10T22:26:47.167008Z"
    },
    "success": true,
    "errors": [],
    "messages": []
}

```
