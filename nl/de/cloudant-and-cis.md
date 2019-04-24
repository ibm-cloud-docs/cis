---

copyright:
  years: 2019
lastupdated: "2019-03-28"

keywords: Cloudant database, CORS, cross-origin resource sharing, host header

subcollection: cis

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"} 
{:note: .note}


# Greifen Sie über IBM Cloud Internet Services auf Ihre Cloudant-Datenbank zu.
{: #access-cloudant-through-cis}

Führen Sie die folgenden Schritte aus, um über IBM Cloud Internet Services (CIS) auf Ihre Cloudant-Datenbank zuzugreifen.

## Vorbemerkungen
{: #access-cloudant-through-cis-begin}

Bei diesen Anweisungen wird vorausgesetzt, dass Sie bereits wie auf der Seite [Erste Schritte](/docs/infrastructure/cis?topic=cis-getting-started-with-ibm-cloud-internet-services-cis-) beschrieben eine Domäne zu CIS hinzugefügt haben.

### Schritt 1: Fügen Sie Ihre CIS-Domäne zum Cross-Origin Resource Sharing (CORS) hinzu
{: #access-cloudant-through-cis-step1}

* Navigieren Sie zu Ihrer Cloudant-Datenbank und öffnen Sie die Seite `Acccount` -> `CORS`.
* Fügen Sie Ihre CIS-Domäne im Eingabefeld der Ursprungsdomänen hinzu. Beispiel: `https://cloudant.test.foo.com`.

### Schritt 2. Konfigurieren Sie CIS so, dass es auf Ihre Cloudant-Datenbank verweist.
{: #access-cloudant-through-cis-step2}

* Navigieren Sie zum CIS-Dashboard und erstellen Sie eine Lastausgleichsfunktion oder einen DNS-Datensatz, der auf den Hostnamen Ihrer Cloudant-Datenbank verweist. Beispiel: `https://cloudant.test.foo.com` -> `111-222-333-444-555-test.cloudant.com`.
* Aktivieren Sie `proxy` für den DNS-Datensatz oder die Lastausgleichsfunktion. 


### Schritt 3. Erstellen Sie eine Seitenregel, um die Überschreibung des Host-Headers festzulegen.
{: #access-cloudant-through-cis-step3}

* Navigieren Sie im CIS-Dashboard zu `Leistung` -> `Seitenregeln`.
* Erstellen Sie eine Seitenregel für die gewünschte URL, z. B. `https://cloudant.test.foo.com/*`.
* Wählen Sie für das Regelverhalten die Einstellung `Überschreibung des Host-Headers` aus.
* Legen Sie den Hostname für die Cloudant-Datenbank fest. Beispiel: `111-222-333-444-555-test.cloudant.com`.

Weitere Informationen zu Cloudant finden Sie in der [Dokumentation zu Cloudant](/docs/services/Cloudant?topic=cloudant-getting-started-with-cloudant).
