---

copyright:
  years: 2018
lastupdated: "2018-03-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Einrichten Ihres Domain Name System (DNS) für IBM CIS

In diesem Dokument finden Sie spezifische Anweisungen zum Konfigurieren Ihrer IBM CIS-DNS-Datensätze, darunter auch zum Konfigurieren von Secure DNS. 

## Secure DNS

**DNSSec** ist eine Technologie zum digitalen Signieren von DNS-Daten, sodass Sie sicher sein können, dass diese gültig sind. Um mögliche Internetsicherheitslücken zu eliminieren, muss DNSSec in jedem Schritt des Suchvorgangs implementiert sein, von der Rootzone bis hin zum finalen Domänennamen (z. B. www.icann.org). 

## Secure DNS konfigurieren und verwalten 

DNSSec fügt der DNS-Infrastruktur des Internets, die andernfalls nicht sicher wäre, eine Authentifizierungsebene hinzu. Secure DNS garantiert, dass Besucher direkt zu **Ihrem** Web-Server geführt werden, wenn sie Ihren Domänennamen in einen Web-Browser eingeben. Sie müssen nur dafür sorgen, dass 'DNSSec' auf der DNS-Seite in Ihrem IBM CIS-Konto aktiviert ist, und Sie müssen den DS-Datensatz zu Ihrem Registrator hinzufügen. 

![Secure DNS](images/dns/secure-dns.png)

Sie können auf die Schaltfläche **DS-Datensätze anzeigen** klicken, um ein Dialogfenster zu öffnen, in dem erläutert wird, wie Sie den DS-Datensatz zu Ihrem Registrator hinzufügen. Sie müssen Teile des DS-Datensatzes kopieren und in das Dashboard Ihres Registrators einfügen. Jeder Registrator unterscheidet sich, und möglicherweise müssen Sie bei Ihrem Registrator nur einen Teil der verfügbaren Felder ausfüllen. 

## DNS-Datensätze hinzufügen

Im Dropdown-**Typ** können Sie den Typ von Datensatz auswählen, den Sie erstellen möchten. Jedem DNS-Datensatztyp ist ein Name und eine Lebensdauer (Time-To-Live, TTL) zugeordnet.  

Dem Eintrag im Namensfeld wird der Domänenname angehängt, es sei denn, der Domänenname wurde bereits manuell im Feld angegeben (Beispiel: Wenn `www` oder `www.beispiel.com` im Feld eingegeben wird, verarbeitet die API beides als `www.beispiel.com`). Wenn der exakte Domänenname in das Namensfeld eingegeben wird, wird er nicht an sich selbst angehängt (Beispiel: `beispiel.com` wird als `beispiel.com` verarbeitet). In der Liste von DNS-Datensätzen werden jedoch nur die Namen ohne die angehängten Domänennamen angezeigt. `www.beispiel.com` wird also als `www` und `beispiel.com` wird als `beispiel.com` angezeigt. Die Lebensdauer hat den Standardwert `Automatisch`, kann aber vom Benutzer geändert werden. Ein Proxy-DNS-Datensatz hat immer die TTL-Einstellung `Automatisch`, deshalb wird ein neuer Proxy-Datensatz diese Konfiguration übernehmen. 

### Datensatz vom Typ A

Um diesen Datensatztyp hinzuzufügen, müssen in den Feldern **Name** und **IPv4-Adresse** gültige Werte vorhanden sein. Im Dropdown-Menü kann auch eine **TTL** ausgewählt werden, der Standardwert ist 'Automatisch'. 

![Datensatz vom Typ A erstellen](images/dns/create-a-type-record.png)

    Erforderliche Felder: Name, IPv4-Adresse
    Optionales Feld: TTL (Standardwert ist 'Automatisch')

### Datensatz vom Typ AAAA

Um diesen Datensatztyp hinzuzufügen, müssen in den Feldern **Name** und **IPv-Adresse** gültige Werte vorhanden sein. Im Dropdown-Menü kann auch eine **TTL** ausgewählt werden, der Standardwert ist 'Automatisch'. 

![Datensatz vom Typ AAAA erstellen](images/dns/create-aaaa-type-record.png)

    Erforderliche Felder: Name, IPv6-Adresse
    Optionales Feld: TTL (Standardwert ist 'Automatisch')

### Datensatz vom Typ CNAME

Um diesen Datensatztyp hinzuzufügen, müssen im Feld **Name** ein gültiger Wert und im Feld **Domänenname** (FQDN) ein vollständig qualifizierter Domänenname vorhanden sein. Im Dropdown-Menü kann auch eine **TTL** ausgewählt werden, der Standardwert ist 'Automatisch'. 


![Datensatz vom Typ CNAME erstellen](images/dns/create-cname-type-record.png)

    Erforderliche Felder: Name, Domänenname (für CNAME)
    Optionales Feld: TTL (Standardwert ist 'Automatisch')


### Datensatz vom Typ MX

Um diesen Datensatztyp hinzuzufügen, müssen im Feld **Name** ein gültiger Wert und im Feld **E-Mail-Server** eine gültige Adresse vorhanden sein. Im Dropdown-Menü kann auch eine **TTL** ausgewählt werden, der Standardwert ist 'Automatisch'. 

![Datensatz vom Typ MX erstellen](images/dns/create-mx-type-record.png)

    Erforderliche Felder: Name, E-Mail-Server
    Optionale Felder: TTL (Standardwert ist 'Automatisch'), Priorität (Standardwert ist '1')

### Datensatz vom Typ LOC

Um diesen Datensatz hinzuzufügen, muss im Feld **Name** ein gültiger Wert vorhanden sein. Wenn Sie genauere Informationen benötigen, klicken Sie auf die Schaltfläche **LOC-Optionen konfigurieren**. Im Dropdown-Menü kann auch eine **TTL** ausgewählt werden, der Standardwert ist 'Automatisch'. 

![Datensatz vom Typ LOC erstellen](images/dns/create-loc-type-record-1.png)

    Erforderliche Felder: Name
    Optionale Felder: LOC-Optionen (zur Konfiguration auf die Schaltfläche klicken)

![Datensatz vom Typ LOC erstellen](images/dns/create-loc-type-record-2.png)

### Datensatz vom Typ CAA

Um diesen Datensatztyp hinzuzufügen, müssen in den Feldern **Name** und **Wert** gültige Werte vorhanden sein. Das Feld 'Wert' wird mit dem Wert im Dropdown-Feld **Tag** korreliert, der standardmäßig 'Berichte zu Verstößen an URL senden' lautet. Im Dropdown-Menü kann auch eine **TTL** ausgewählt werden, der Standardwert ist 'Automatisch'. 

![Datensatz vom Typ CAA erstellen](images/dns/create-caa-type-record.png)

    Erforderliche Felder: Name, Wert (mit Tag korreliert)
    Optionale Felder: TTL (Standardwert ist 'Automatisch'), Tag (Standardwert ist 'Berichte zu Verstößen an URL senden')

### Datensatz vom Typ SRV

Um diesen Datensatztyp hinzuzufügen, müssen in den Feldern **Name**, **Servicename** und **Ziel** gültige Werte vorhanden sein. Wählen Sie im Dropdown-Menü ein **Protokoll** aus; standardmäßig ist das UDP-Protokoll ausgewählt. Darüber hinaus können Sie die **Priorität**, die **Wertigkeit** und den **Port** angeben. Diese drei Felder haben den Standardwert '1'. Im Dropdown-Menü kann auch eine **TTL** ausgewählt werden; der Standardwert ist 'Automatisch'. 

![Datensatz vom Typ SRV erstellen](images/dns/create-srv-type-record.png)

    Erforderliche Felder: Name, Servicename, Ziel
    Optionale Felder: TTL (Standardwert ist 'Automatisch'), Protokoll (Standardwert ist 'UDP'), Priorität (Standardwert ist '1'), Wertigkeit (Standardwert ist '1'), Port (Standardwert ist '1')

### Datensatz vom Typ SPF

Um diesen Datensatztyp hinzuzufügen, müssen in den Feldern **Name** und **Inhalt** gültige Werte vorhanden sein. Im Dropdown-Menü kann auch eine **TTL** ausgewählt werden, der Standardwert ist 'Automatisch'. 

![Datensatz vom Typ SPF erstellen](images/dns/create-spf-type-record.png)

    Erforderliche Felder: Name, Inhalt
    Optionales Feld: TTL (Standardwert ist 'Automatisch')

### Datensatz vom Typ TXT

Um diesen Datensatztyp hinzuzufügen, müssen in den Feldern **Name** und **Inhalt** gültige Werte vorhanden sein. Im Dropdown-Menü kann auch eine **TTL** ausgewählt werden, der Standardwert ist 'Automatisch'. 

![Datensatz vom Typ TXT erstellen](images/dns/create-txt-type-record.png)

    Erforderliche Felder: Name, Inhalt
    Optionales Feld: TTL (Standardwert ist 'Automatisch')

### Datensatz vom Typ NS

Um diesen Datensatztyp hinzuzufügen, müssen in den Feldern **Name** und **Namensserver** gültige Werte vorhanden sein. Im Dropdown-Menü kann auch eine **TTL** ausgewählt werden, der Standardwert ist 'Automatisch'. 

![Datensatz vom Typ NS erstellen](images/dns/create-ns-type-record.png)

    Erforderliche Felder: Name, Namensserver
    Optionales Feld: TTL (Standardwert ist 'Automatisch')

## DNS-Datensätze aktualisieren

Sie können in jeder Datensatzzeile im Menü auf die Option **Datensatz bearbeiten** klicken, wodurch ein Dialogfenster geöffnet wird, in dem Sie den Datensatz aktualisieren können. 

![DNS-Datensatz bearbeiten](images/dns/edit-dns-record.png)

Dies ist z. B. der Aktualisierungsdialog für den Datensatztyp **A**. Nachdem Sie die Änderungen vorgenommen haben, wählen Sie **Datensatz aktualisieren** aus, um sie zu speichern. 

![Dialogfenster 'DNS-Datensatz bearbeiten'](images/dns/update-dns-dialog.png)

## Datensätze löschen

Sie können in jeder Datensatzzeile im Menü die Option **Datensatz löschen** auswählen, wodurch ein Dialogfenster geöffnet wird, in dem Sie den Löschvorgang bestätigen können. 

![DNS-Datensatz löschen](images/dns/delete-record.png)

Klicken Sie auf die Schaltfläche **Löschen**, um Ihre Löschaktion zu bestätigen. Wählen Sie **Abbrechen** aus, wenn Sie doch nicht löschen möchten. 

![Dialogfenster 'DNS-Datensatz löschen'](images/dns/delete-record-dialog.png)
