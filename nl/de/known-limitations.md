---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: health checks, Free Trial plan, dedicated certificate, known issues

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 
{:note: .note} 
{:important: .important} 
{:deprecated: .deprecated} 
{:generic: data-hd-programlang="generic"}

# Bekannte Einschränkungen
{:#known-limitations}

 * Wir empfehlen, Chrome zu verwenden.
 
 * Die kostenlose Testversion (Free Trial) ist auf eine Instanz pro Konto begrenzt. Nachdem Sie eine Ressourceninstanz erstellt und ihr eine Domäne hinzugefügt haben, sind Sie nicht berechtigt, eine neue Ressourceninstanz für CIS hinzuzufügen. Diese Einschränkung wird auch dann durchgesetzt, wenn Sie eine Testdomäne löschen und dann versuchen, derselben Ressourceninstanz erneut eine Domäne hinzuzufügen. Wenn Sie dies versuchen, tritt ein Fehler auf.

 * Im Rahmen dieses Service unterstützten wir die Delegierung von Unterdomänen nur bei Verwendung von NS-Datensätzen von einem anderen Provider. Die CNAME-Delegierung wird nicht unterstützt.
  
 * A-, AAAA- und CNAME-Platzhalterzeichen (*) können nicht weitergeleitet werden. 

 * Wenn Sie ein dediziertes Zertifikat löschen, kann es für kurze Zeit erneut in der Liste angezeigt werden, bevor der Löschvorgang abgeschlossen ist. 
 
 * Wenn Sie die Hostnamen des angepassten, dedizierten Zertifikats nach der Bestellung ändern, müssen Sie ein neues Zertifikat anfordern und anschließend das alte löschen.  
 
 * IP-Regeln, die mit aus zwei Buchstaben bestehenden Ländercode erstellt wurden, können nur mit der Aktion `Sicherheitsabfrage ausgeben` erstellt werden. Wenn Sie Besucher von einem Land blockieren möchten, führen Sie eine Aktualisierung auf den Enterprise-Plan durch oder platzieren Sie Regeln auf Ihrem Server, um eine vollständige Blockade zu erreichen. 

## Globale Lastausgleichsfunktion
{:#known-limitations-glb}

 * Cloud Internet Services ermöglichen Ihnen, den Unterstrich `_` in Hostnamen der Lastausgleichsfunktion zu verwenden. Kubernetes-Cluster können den Unterstrich `_` jedoch nicht verwenden. 

 * Der Standardplan ermöglicht maximal 5 Lastausgleichsfunktionen, Pools und Statusprüfungen. Jeder Pool kann über insgesamt 6 Ursprünge verfügen, aber nur 6 eindeutige Ursprünge sind in jeder CIS-Instanz zulässig. 

* Statusprüfereignisse für gelöschte Pools und Ursprünge können gefiltert werden, sie werden aber weiterhin in der Tabelle angezeigt. 

* Wenn Sie Statusprüfereignisse mit `Poolstatus` filtern, werden `beschränkt einwandfreie` Pools eingeschlossen, weil sie technisch in einwandfreiem Zustand sind, aber einen oder mehrere kritische Ursprünge aufweisen. 

* Beim Hinzufügen des Anforderungsheadernamens für eine Statusprüfung verwenden Sie `Host`. Die Verwendung von `host` in Kleinschreibung als Name für eine Statusprüfung schlägt fehl. 

## DNS
{:#known-limitations-dns}

 * Das Exportieren von DNS-Datensätzen umfasst Cloudflare CNAME-Datensätze, die ausgeblendet sein sollten. Diese Datensätze beginnen mit einem Unterstrich `_` und weisen meistens einen zweiten Datensatz auf, der denselben Namen ohne den Unterstrich `_` trägt. 
   ```
   Ex.
   _cf.generate.yourdomain.com 0	IN	CNAME address.alias.com
   cf.generate.yourdomain.com 0	IN	CNAME address2.alias.com
   ```
 
   Diese Datensätze müssen aus der Zonendatei entfernt werden, damit diese ordnungsgemäß importiert werden kann. 
 
 * Das Exportieren von CAA DNS-Datensätzen funktioniert nicht ordnungsgemäß. Das Tag `<tag>` und der Wert `<value>` liegen in Hexadezimalcodierung vor.  
 
    CAA `<flags>` `<tag>` `<value>`
  {:note}
   ```
   Ex.
   Original CAA record
   caa.yourdomain.com.	1	IN	CAA	0 issue "letsencrypt.org"
 
   Exported CAA record
   caa.yourdomain.com.	1	IN	CAA	0 6973737565 "6c657473656e63727970742e6f7267"
   ```
   Diese Datensätze müssen von HEX in Zeichenfolgen konvertiert oder entfernt und vor dem Importieren manuell hinzugefügt werden. 

## Seitenregeln
{:#known-limitations-pagerules}

   * Das Aktualisieren von Einstellungen für Seitenregeln mithilfe des CIS-Plug-ins für IBM Cloud CLI kann zu einem Fehler führen, wenn die Seitenregel-ID nicht in die JSON-Zeichenfolge oder die JSON-Datei für die Aktualisierung eingeschlossen ist. Um dieses Problem zu umgehen, übergeben Sie die Aktualisierung mithilfe einer vollständigen JSON-Konfigurationsdatei für die Seitenregel einschließlich der ID.
   * Das Entfernen der Einstellungen für die Seitenregeln mithilfe der CIS-Benutzerschnittstelle führt möglicherweise auch dann nicht zum Entfernen der Einstellung, wenn die Benutzerschnittstelle eine erfolgreiche Aktualisierung meldet. Um dieses Problem zu umgehen, verwenden Sie das CIS-Plug-in für die IBM Cloud CLI, um die Einstellung zu entfernen und die Seitenregel-ID in das JSON-Aktualisierungsdokument einzubeziehen.
```
      $> ibmcloud cis page-rule-update <domain-id> <rule-id> -j <file>
      ```
      Die JSON-Datei sollte die vollständige Konfiguration der Seitenregel einschließlich der ID sowie die erforderlichen Aktualisierungen enthalten. 
