---
copyright:
  years: 2018
lastupdated: "2018-28-03"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# FAQ

## Was bekomme ich mit einem Early Access Plan?
Das Early Access-Programm lässt standardmäßig nur eine Zone pro Konto zu. Es wird empfohlen, pro Konto nur eine Instanz zu erstellen und den Zonennamen zu überprüfen. Der Zonenname MUSS überprüft werden, bevor er hinzufügt wird. Wird eine Zone gelöscht, kann weder eine andere noch diese Zone im Rahmen des Early Access-Programms hinzugefügt werden. 

## Warum hat meine Domäne den Status 'Anstehend'? Wie aktiviere ich sie? 
Wenn Sie eine Domäne zu CIS hinzufügen, nennen wir Ihnen ein Paar Namensserver, die Sie bei Ihrem Registrator konfigurieren sollen (oder bei Ihrem DNS-Anbieter, falls Sie eine Unterdomäne hinzufügen). Die Domäne oder Unterdomäne verbleibt bis zur korrekten Konfiguration der Namensserver im Status 'Anstehend'. Stellen Sie sicher, dass Sie beide Namensserver zu Ihrem Registrator oder Ihrem DNS-Anbieter hinzufügen. Wir prüfen das öffentliche DNS-System regelmäßig, um zu sehen, ob die Namensserver wie angewiesen konfiguriert wurden. Sobald wir die Änderung der Namensserver verifizieren können (dies kann bis zu 24 Stunden dauern), aktivieren wir Ihre Domäne. Sie können eine Anforderung zum erneuten Prüfen der Namensserver übergeben, indem Sie auf der Übersichtsseite auf **Namensserver erneut prüfen** klicken. 

## Wer ist der Registrator für meine Domäne? 
Diese Information finden Sie unter 'https://whois.icann.org/'. **Hinweis**: Sie müssen über Administratorberechtigungen verfügen, um Ihre Domänenkonfiguration beim Registrator zu registrieren oder um die Namensserver zu aktualisieren oder hinzuzufügen, die für Ihre Domäne bereitgestellt werden, wenn Sie diese zu CIS hinzufügen. Wenn Sie den Registrator für die Domäne, die Sie zu CIS hinzuzufügen versuchen, nicht kennen, ist es unwahrscheinlich, dass Sie berechtigt sind, die Konfiguration Ihrer Domäne beim Registrator zu aktualisieren. Arbeiten Sie mit dem Eigentümer der Domäne in Ihrem Unternehmen zusammen, um die erforderlichen Änderungen vorzunehmen. 

## Ich möchte meinen aktuellen DNS-Anbieter für meine Domäne (beispiel.com) behalten. Kann ich eine Unterdomäne (unterdomäne.beispiel.com) von meinem aktuellen DNS-Anbieter an CIS delegieren? 
Ja. Der Prozess ähnelt dem Hinzufügen einer Domäne, aber statt des Registrators arbeiten Sie mit dem DNS-Anbieter für die Domäne der höheren Ebene zusammen. Wenn Sie eine Unterdomäne zu CIS hinzufügen, werden Ihnen wie üblich zwei Namensserver genannt, die Sie konfigurieren müssen. Sie konfigurieren einen Namensserver-Datensatz (NS-Datensatz) für jeden der beiden Namensserver in Form eines DNS-Eintrags in Ihrer Domäne, die von dem anderen DNS-Anbieter verwaltet wird. Sobald wir verifizieren konnten, dass die erforderlichen NS-Datensätze hinzugefügt wurden, aktivieren wir Ihre Unterdomäne. Wenn Sie die Domäne der höheren Ebene nicht in Ihrem Unternehmen verwalten, müssen Sie mit dem Eigner der Domäne der höheren Ebene arbeiten, um die NS-Datensätze hinzuzufügen. 

## Was ist TLS?
TLS ist ein Standardsicherheitsprotokoll zur Einrichtung verschlüsselter Links zwischen einem Web-Server und einem Browser in einer Onlinekommunikation. Ein TLS-Zertifikat ist erforderlich, um eine TLS-Verbindung mit einer Website herzustellen, und besteht aus dem Domänennamen, dem Namen des Unternehmens und weiteren Daten wie Adresse, Stadt, Bundesland und Land des Unternehmens. Das Zertifikat zeigt außerdem das Verfallsdatum sowie Details der ausstellenden Zertifizierungsstelle an. 

## Wie funktioniert TLS? 
Wenn ein Browser eine Verbindung mit einer durch TLS gesicherten Website startet, ruft er zunächst das TLS-Zertifikat der Site ab, um zu prüfen, ob dieses noch gültig ist. Der Browser verifiziert, dass die Zertifizierungsstelle vertrauenswürdig ist und dass das Zertifikat von der Website verwendet wird, für die es ausgegeben wurde. Schlägt eine dieser Prüfungen fehl, wird eine Warnung angezeigt, dass die Website nicht durch ein gültiges Zertifikat gesichert ist. 

Wenn ein TLS-Zertifikat auf einem Web-Server installiert ist, ermöglicht es eine sichere Verbindung zwischen dem Web-Server und dem damit verbundenen Browser. Der Website der URL wird 'https' anstelle von 'http' vorangestellt und in der Adressleiste wird ein Vorhängeschloss angezeigt. Wenn die Website ein EV-Zertifikat (Extended Validation, erweiterte Validierung) verwendet, kann im Browser auch eine grüne Adressleiste angezeigt werden. 

## Warum wird eine Datenschutzwarnung angezeigt?
Die TLS-Zertifikate, die von IBM Cloud CIS ausgestellt werden, decken die Rootdomäne (`beispiel.com`) und eine Unterdomäne (`*.beispiel.com`) ab. Wenn Sie versuchen, eine Unterdomäne der zweiten Ebene (`*.*.beispiel.com`) zu erreichen, wird in Ihrem Browser eine Warnung zum Datenschutz angezeigt, da diese Hostnamen nicht zum SAN hinzugefügt werden. 

Es kann bis zu 15 Minuten dauern, bis eine unserer Partnerzertifizierungsstellen ein neues Zertifikat ausstellt. Solange Ihr neues Zertifikat noch nicht ausgestellt wurde, wird in Ihrem Browser eine Warnung zum Datenschutz angezeigt. 

## Was ist DDoS? 
Ein dezentraler Denial-of-Service-Angriff (Distributed Denial of Service, DDoS) ist ein Versuch, einen Onlineservice auszuhebeln, indem er mit Datenverkehr aus mehreren Quellen überschwemmt wird. Bei einem DDoS-Angriff greifen mehrere beeinträchtigte Computersysteme ein Ziel wie einen Server, eine Website oder andere Netzressourcen an, wodurch die Benutzer der Zielressourcen in ihrer Arbeit beeinträchtigt werden. 

Die Flut von eingehenden Nachrichten, Verbindungsanforderungen oder fehlerhaften Paketen an das Zielsystem führt zu einer Verlangsamung oder sogar zum Absturz und zum Herunterfahren des Systems. Berechtigte Benutzer können den Service nicht länger nutzen. DDoS-Angriffe waren und sind Mittel zum Zweck diverser Bedrohungsakteure, von einzelnen kriminellen Hackern bis hin zu organisiertem Verbrechen und Regierungsbehörden. 

## Was kann ich tun, wenn ich Ziel eines DDoS-Angriffs bin?

**Schritt 1:** Aktivieren Sie in der Anzeige **Übersicht** den 'Verteidigungsmodus'.  

![Verteidigungsmodus](images/defense-mode.png)

**Schritt 2:** Legen Sie für Ihre DNS-Datensätze maximale Sicherheit fest. 

**Schritt 3:** Drosseln Sie die Anforderungen von IBM CIS nicht, wir benötigen eine möglichst große Bandbreite, um Sie in Ihrer Situation zu unterstützen. 

**Schritt 4:** Blockieren Sie ggf. bestimmte Länder und Besucher. 

## Ich bekomme einen 522-Fehler. Was mache ich jetzt?

Ein 522-Fehler gibt an, dass wir keine Verbindung mit Ihrem Ursprungsserver (d. h. Ihrem Host) herstellen konnten. Wenn wir nach ca. 15 Sekunden keine Verbindung herstellen können, schließen wir die Verbindung und zeigen eine 522-Fehlerseite an. 

Dieses Problem wird üblicherweise von einer Firewall oder Sicherheitssoftware hervorgehoben, die unsere IP-Adressen unbeabsichtigt blockiert. Da CIS als Reverse Proxy agiert, kann es den Anschein machen, das Verbindungen mit Ihrer Site von einer Reihe von CIS-IPs kommen. Dieses Verhalten kann dazu führen, dass bestimmte Firewalls diese Verbindungen blockieren und wir folglich den Besuchern Ihrer Website Inhalte nicht mehr ordnungsgemäß bereitstellen können. 

Sie können dieses Problem beheben, indem Sie Ihren Host bitten, alle CIS-IP-Bereiche, die [hier](whitelisted-ips.html) aufgelistet sind, in die Whitelist aufzunehmen. 

Alle diese IPs müssen in der Whitelist enthalten sein, um 522-Fehler zu vermeiden. Es lohnt sich auch, zu prüfen, ob IPs in diesen Bereichen blockiert werden. 

522-Fehler können auch durch Netzkonnektivitätsprobleme verursacht werden. Stellen Sie also grundsätzlich sicher, dass Ihr Server und Ihr Netz in einwandfreiem Zustand und nicht überlastet sind. 

Wenn Sie immer noch Fehler bekommen, nachdem Sie die oben genannten Schritte ausgeführt haben, wenden Sie sich an den IBM CIS Support und bestätigen Sie Folgendes: 

* Unsere IP-Bereiche sind in Ihrer Whitelist aufgeführt. 
* Ihr Server/Netz ist online und in einwandfreiem Zustand. 

Wenn Sie unser Support-Team kontaktieren, geben Sie die Ray ID eines kürzlich angezeigten 522-Fehlers an. Wir können anhand dieser ID bestimmen, welches CIS-Rechenzentrum Sie nutzen und weitere Tests ausführen. 

## Was ist ein Proxy-Datensatz und wozu brauche ich ihn?

Proxy-Datensätze sind Datensätze, die ihren Datenverkehr über IBM CIS weiterleiten. Nur Proxy-Datensätze können die Vorteile von CIS nutzen, wie IP-Masking, bei dem Ihre Ursprungs-IP durch eine CIS-IP ersetzt wird, um sie zu schützen: 

```
$ whois 104.28.22.57 | grep OrgName
OrgName:        IBM
```

Wenn Sie CIS in einer Domäne lieber übergehen möchten (DNS wird trotzdem aufgelöst), ist ein Nicht-Proxy-Datensatz eine mögliche Lösung. 

## Ich bekomme einen DNS-Validierungsfehler 1004; was kann ich jetzt tun?

Damit Seitenregeln funktionieren, muss DNS für Ihre Zone aufgelöst werden. Sie müssen folglich über einen Proxy-DNS-Datensatz für Ihre Zone verfügen.  
