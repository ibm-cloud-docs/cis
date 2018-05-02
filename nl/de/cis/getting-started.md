---
copyright:
  years: 2018
lastupdated: "2018-03-19"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Einführung in IBM Cloud Internet Services (CIS)

IBM Cloud Internet Services (CIS) bietet drei zentrale Leistungsmerkmale zur Verbesserung Ihres Workflows: [Sicherheit](/docs/infrastructure/cis/managing-for-security.html), [Zuverlässigkeit](/docs/infrastructure/cis/managing-for-reliability.html) und [Leistung](/docs/infrastructure/cis/managing-for-performance.html). Alle drei Funktionalitäten werden in der linken Navigationsleiste Ihres Bildschirms dargestellt, sobald Sie die IBM CIS-Anwendung öffnen. 

Mit IBM CIS können Sie die einzelnen Merkmale dieser Funktionalitäten an Ihre speziellen Bedürfnisse anpassen: 

 * Autoritative DNS-Server
 * Globaler und lokaler Lastausgleich
 * Web Application Firewall (WAF)
 * DDoS-Schutz
 * Caching und Seitenregeln



## Vorbemerkungen
Bevor Sie IBM CIS verwenden können, benötigen Sie eine [IBMid](https://www.ibm.com/account/us-en/signup/register.html). Im Anschluss können Sie Ihre Services über Ihr IBM Cloud-Konto oder über das neue [IBM Cloud Internet Services-Portal](https://console.bluemix.net/catalog/services/internet-services) anfordern, ganz wie Sie wünschen. 

Wenn Sie Unterstützung benötigen, um ein Konto für die Verwendung von IBM Cloud Internet Services zu erhalten, [wenden Sie sich an Ihren IBM Vertriebsbeauftragten](https://www.ibm.com/cloud-computing/bluemix/contact-us), um weitere Informationen zu den ersten Schritten zu erhalten. 

Wenn Sie bereits über ein Softlayer-Konto verfügen, können Sie [Ihr Konto mit Ihrer IBMid verknüpfen](https://console.bluemix.net/docs/account/softlayerlink.html#unifyingaccounts).  

## Übersicht über die Vorgehensweise

Sie können IBM CIS nach nur wenigen Schritten für Ihren Internetdatenverkehr verwenden. 

 * Öffnen Sie die IBM CIS-Anwendung in Ihrem IBM Cloud-Dashboard. 
 * Fügen Sie die Domäne hinzu, die Sie verwalten möchten. 
 * Konfigurieren Sie Ihre DNS-Informationen mit den Namensservern, die wir bereitgestellt haben. 
 * Fahren Sie mit der Einführung in IBM CIS fort, indem Sie ein Lernprogramm ausführen oder weitere Features einrichten. 

### Schritt 1: IBM CIS-Anwendung öffnen

Öffnen Sie Ihr [IBM Cloud-Dashboard](https://console.bluemix.net/catalog/). Navigieren Sie dann zum IBM CIS-Anwendungssymbol, indem Sie die Kategorie **Plattform -> Netz** in der linken Navigationsleiste des Dashboards auswählen. Öffnen Sie die IBM Cloud Internet Services-Anwendung, indem Sie auf das Symbol klicken, das in der Mitte des Bildschirms angezeigt wird.  

![Katalog](images/catalog-cis-tile.png)

**Übersichtsanzeige**

Sobald die IBM CIS-Anwendung gestartet wurde, wird die Anzeige **Übersicht** für IBM CIS geöffnet und auf der linken Seite der Benutzeroberfläche finden Sie die Registerkarten für **Sicherheit**, **Zuverlässigkeit** und **Leistung**. 

**Welchen Plan wähle ich?**

Für das Release _Early Access_ steht nur ein Plan zur Auswahl und er ist kostenlos. Klicken Sie unten links in der Anzeige **Übersicht** auf die Schaltfläche **Erstellen**, um mit der Bereitstellung Ihres Kontos zu beginnen. 

**Bereitstellung beginnen**

Die erste Anzeige der IBM CIS-Anwendung wird geöffnet, in der Sie auf die Schaltfläche **Domäne hinzufügen** klicken. 

|**Beachten Sie, dass das Early Access-Programm auf eine Instanz pro Konto begrenzt ist.** |
|-------------------------------------------------------------------|
| Nachdem Sie eine Ressourceninstanz erstellt und ihr eine Domäne hinzugefügt haben, sind Sie nicht berechtigt, neue Ressourceninstanzen für IBM CIS hinzuzufügen. Diese Einschränkung wird auch dann durchgesetzt, wenn Sie eine Testdomäne löschen und dann versuchen, derselben Ressourceninstanz erneut eine Domäne hinzuzufügen. Wenn Sie dies versuchen, tritt ein Fehler auf. |

### Schritt 2. Domäne hinzufügen und konfigurieren

Beginnen Sie mit dem Schutz und der Verbesserung der Leistung Ihres Web-Service, indem Sie Ihre Domäne oder eine Unterdomäne eingeben. 

**Hinweis:** Geben Sie bitte DNS-Zonen an. Sie können die Namensserver für diese Domänen oder Unterdomänen beim Registrator der Domäne oder beim DNS-Anbieter konfigurieren. Verwenden Sie keine CNAMEs. 

![Einführung](images/overview-add-domain.png)
In der Übersichtsanzeige wird Ihre Domäne im Status `Anstehend` dargestellt. Sie verbleibt in diesem Status, bis Sie Schritt 3 ausgeführt haben. 

**Hinweis:** Die IBM CIS-Instanz kann nicht gelöscht werden, nachdem eine Domäne hinzugefügt wurde. Um die Instanz zu löschen, müssen Sie zunächst die Domäne aus der Instanz löschen. 

### Schritt 3. Namensserver beim Registrator oder dem vorhandenen DNS-Anbieter konfigurieren

Damit Sie von den Vorteilen von IBM CIS profitieren können, konfigurieren Sie Ihren Registrator oder Domänennamenanbieter für die Verwendung der aufgelisteten Namensserver. Wenn Sie eine Domäne delegieren (z. B. `beispiel.com`), konfigurieren Sie die aufgelisteten Namensserver in den Einstellungen Ihrer Domäne, wo sie von Ihrem Registrator verwaltet werden (z. B. im Webportal des Registrators). Wenn Sie sich nicht sicher sind, wer der Registrator für Ihre Domäne ist, finden Sie diese Angabe unter 'https://whois.icann.org/'. Wenn Sie eine Unterdomäne (z. B. `unterdomäne.beispiel.com`) von einem anderen DNS-Anbieter delegieren, müssen Sie einen Namensserver-Datensatz (NS-Datensatz) für jeden aufgelisteten Namensserver hinzufügen. 

Nachdem Sie Ihren Registrator oder DNS-Anbieter konfiguriert haben, kann es bis zu 24 Stunden dauern, bis die Änderungen wirksam werden. Sobald wir überprüfen konnten, dass die angegebenen Namensserver korrekt für Ihre Domäne oder Unterdomäne konfiguriert wurden, ändert sich der Status der Domäne von `Anstehend` in `Aktiv`. Nach der Konfiguration der Namensserver können Sie auf den Link zum erneuten Prüfen der Namensserver auf der Seite `Übersicht` klicken, um die Aktivierung Ihrer Domäne möglicherweise zu beschleunigen (diese Prüfung kann nur einmal pro Stunde ausgeführt werden). 

### Schritt 4. Stellen Sie sicher, dass IBM Cloud Internet Services die Domäneninformationen für Ihre Anwendung, Ihren Hostnamen oder Ihre Website auflöst. 

Fahren Sie fort, indem Sie die Registerkarte **Zuverlässigkeit** in der linksseitigen Navigationsleiste und dann die Option **DNS** auswählen. Stellen Sie sicher, dass Sie die passenden _DNS-Datensätze_ hinzufügen. Fügen Sie den **Datensatz A** und alle **AAAA**- oder **MX**-Einträge hinzu, die einen Wert enthalten. Wenn Sie vergessen, diese Datensätze hinzuzufügen, bevor die Delegierung des Registrators abgeschlossen ist, kann IBM Cloud Internet Services die Domäneninformationen für Ihre mit dem Internet verbundenen Anwendungen nicht auflösen.   

![Einführung](images/dns-records.png)

### Schritt 5. Mit der Verwaltung anderer IBM CIS-Funktionen und -Features beginnen

Weitere Details zum Verwalten anderer Funktionen oder Features finden Sie in den [schrittweisen Anleitungen](/docs/infrastructure/cis/how-to.html). 
