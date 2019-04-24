---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: configuration domain, Free Trial plan, CIS instance

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:faq: data-hd-content-type='faq'}



# FAQ
{:#faq}

## Was ist mit dem Early Access Plan passiert, der früher im Katalog war?
{:#cis-faq-early-access-plan}
{: faq}

Der Early Access Plan wurde am 31. Mai 2018 aus dem Katalog entfernt. Es wurde durch den kostenpflichtigen Standard-Plan und den neuen 30-Tage-Testplan ersetzt. Wenn Sie über eine Instanz des Early Access Plans verfügen, führen Sie bitte ein Upgrade auf den Standardplan aus, um Datenverlust zu vermeiden. Sie können keine Instanz der kostenlosen Testversion (Free Trial) erstellen, wenn Sie an Early Access-Beta teilgenommen haben. 

## Was umfasst der kostenlose Testplan (Free Trial)? 
{:#cis-faq-free-trial-plan}
{: faq}

Der kostenlose Testplan 'Free Trial' ermöglicht Ihnen von der Konstruktion her nur eine Zone pro Konto. Es wird empfohlen, pro Konto nur eine Instanz zu erstellen und den Zonennamen zu überprüfen. Der Zonenname MUSS überprüft werden, bevor er hinzufügt wird. Wenn eine Zone gelöscht wird, kann weder eine anderen Zone noch dieselbe Zone während des kostenlosen Testplans hinzugefügt werden. 

## Wie viele kostenlose Testinstanzen kann ich haben? 
{:#cis-faq-free-trial-instances}
{: faq}

Sie können während der Lebensdauer des Kontos höchstens eine Instanz der kostenlosen Testversion pro Konto haben. Wenn Sie bereits über eine kostenlose Testinstanz verfügen oder wenn Sie eine kostenlose Testinstanz löschen oder wenn die kostenlose Testversion abläuft, können Sie keine andere kostenlose Testversion erstellen. Sie können jedoch Instanzen anderer kostenpflichtiger Plantypen (z.B. Standardplan) unabhängig von möglicherweise schon erstellten kostenlosen Testversionen erstellen. 

## Ich habe eine Serviceinstanz, die beim Early Access Plan abonniert ist. Kann ich das in Free Trial ändern?
{:#cis-faq-early-access-to-free-trial-plan}
{: faq}

Nein. Für einen vorhandenen Access Plan kann nur ein Upgrade auf einen kostenpflichtigen Plan durchgeführt werden. Das ist momentan der Standardplan. 

## Ich hatte eine Early Access-Instanz, die ich (möglicherweise oder auch nicht) gelöscht habe. Kann ich jetzt eine Free Trial-Instanz erstellen? 
{:#cis-faq-early-access-and-free-trial-plan}
{: faq}

Nein. Jedes Konto ist nur für eine kostenfreie Instanz berechtigt. Sowohl der Early Access Plan als auch der Free Trial-Plan, der diesen ersetzt hat, sind kostenfrei. Das bedeutet auch, dass Sie höchstens eine Free Trial-Instanz haben können.

## Kann ich ein Downgrade von Standard auf Free Trial durchführen?
{:#cis-faq-downgrade-standard-to-free-plan}
{: faq}

Nein. Das ist nicht zulässig. 

## Mein Free Trial ist abgelaufen. Welche Möglichkeiten habe ich? 
{:#cis-faq-free-trial-plan-expired}
{: faq}

Um Datenverlust zu vermeiden, müssen Sie vor dem Ablaufdatum ein Upgrade von Free Trial den Standardplan auf durchführen. Danach unterstützen wir nur eine Aktualisierung des Plans oder das Löschen der CIS-Instanz. Wenn die Instanz nicht innerhalb von 45 Tagen (von der Initialisierung der Instanz an gerechnet) gelöscht oder aktualisiert wird, werden die Konfigurationsdomäne, GLB, Pools und Statusprüfungen automatisch gelöscht. 

## Wie lösche ich meine CIS-Instanz? 
{:#{:#cis-faq-delete-instance}
{: faq}

Wenn Sie eine CIS-Instanz löschen möchten, müssen Sie zuerst alle GLBs, Pools und Statusprüfungen löschen. Anschließend löschen Sie die zugehörige Domäne (Zone). Rufen Sie die Seite **Übersicht** auf und klicken Sie auf das Papierkorbsymbol neben dem Domänennamen, der sich im Abschnitt **Servicedetails** befindet, um den Löschvorgang zu starten. 

## Ich habe eine Benutzer zu meinem Konto hinzugefügt und ihm Benutzerberechtigungen zum Verwalten der Internet-Service-Instanz(en) erteilt. Warum hat dieser Benutzer Authentifizierungsprobleme? 
{:#cis-faq-user-authentication-issue}
{: faq}

Es ist möglich, dass Sie dem Benutzer nicht die Rollen für den Zugriff auf den Service erteilt haben. Beachten Sie, dass es zwei separate Gruppen von Rollen gibt: "Plattformzugriff" und "Servicezugriff". Plattformzugriffsrollen sind erforderlich, um Serviceinstanzen zu erstellen und zu verwalten. Aber Servicezugriffsrollen sind erforderlich um servicespezifische Operationen an Serviceinstanzen auszuführen. Diese Einstellungen können in der Konsole durch die Auswahl von **Verwalten > Sicherheit > Identität und Zugriff** aktualisiert werden.

## Warum hat meine Domäne den Status 'Anstehend'? Wie aktiviere ich sie?
{:#cis-faq-pending-domain}
{: faq}

Wenn Sie eine Domäne zu CIS hinzufügen, nennen wir Ihnen ein Paar Namensserver, die Sie bei Ihrem Registrator konfigurieren sollen (oder bei Ihrem DNS-Anbieter, falls Sie eine Unterdomäne hinzufügen). Die Domäne oder Unterdomäne verbleibt bis zur korrekten Konfiguration der Namensserver im Status 'Anstehend'. Stellen Sie sicher, dass Sie beide Namensserver zu Ihrem Registrator oder Ihrem DNS-Anbieter hinzufügen. Wir prüfen das öffentliche DNS-System regelmäßig, um zu sehen, ob die Namensserver wie angewiesen konfiguriert wurden. Sobald wir die Änderung der Namensserver verifizieren können (dies kann bis zu 24 Stunden dauern), aktivieren wir Ihre Domäne. Sie können eine Anforderung zum erneuten Prüfen der Namensserver übergeben, indem Sie auf der Übersichtsseite auf **Namensserver erneut prüfen** klicken.

## Wer ist der Registrator für meine Domäne?
{:#cis-faq-who-is-registrar}
{: faq}

Diese Information finden Sie unter 'https://whois.icann.org/'. **Hinweis**: Sie müssen über Administratorberechtigungen verfügen, um Ihre Domänenkonfiguration beim Registrator zu registrieren oder um die Namensserver zu aktualisieren oder hinzuzufügen, die für Ihre Domäne bereitgestellt werden, wenn Sie diese zu CIS hinzufügen. Wenn Sie den Registrator für die Domäne, die Sie zu CIS hinzuzufügen versuchen, nicht kennen, ist es unwahrscheinlich, dass Sie berechtigt sind, die Konfiguration Ihrer Domäne beim Registrator zu aktualisieren. Arbeiten Sie mit dem Eigentümer der Domäne in Ihrem Unternehmen zusammen, um die erforderlichen Änderungen vorzunehmen.

## Ich möchte meinen aktuellen DNS-Anbieter für meine Domäne (beispiel.com) behalten. Kann ich eine Unterdomäne (unterdomäne.beispiel.com) von meinem aktuellen DNS-Anbieter an CIS delegieren?
{:#cis-faq-keep-current-dns-provider}
{: faq}

Ja. Der Prozess ähnelt dem Hinzufügen einer Domäne, aber statt des Registrators arbeiten Sie mit dem DNS-Anbieter für die Domäne der höheren Ebene zusammen. Wenn Sie eine Unterdomäne zu CIS hinzufügen, werden Ihnen wie üblich zwei Namensserver genannt, die Sie konfigurieren müssen. Sie konfigurieren einen Namensserver-Datensatz (NS-Datensatz) für jeden der beiden Namensserver in Form eines DNS-Eintrags in Ihrer Domäne, die von dem anderen DNS-Anbieter verwaltet wird. Sobald wir verifizieren konnten, dass die erforderlichen NS-Datensätze hinzugefügt wurden, aktivieren wir Ihre Unterdomäne. Wenn Sie die Domäne der höheren Ebene nicht in Ihrem Unternehmen verwalten, müssen Sie mit dem Eigner der Domäne der höheren Ebene arbeiten, um die NS-Datensätze hinzuzufügen.

## Was ist TLS?
{:#cis-faq-what-is-tls}
{: faq}

TLS ist ein Standardsicherheitsprotokoll zur Einrichtung verschlüsselter Links zwischen einem Web-Server und einem Browser in einer Onlinekommunikation. Ein TLS-Zertifikat ist erforderlich, um eine TLS-Verbindung mit einer Website herzustellen, und besteht aus dem Domänennamen, dem Namen des Unternehmens und weiteren Daten wie Adresse, Stadt, Bundesland und Land des Unternehmens. Das Zertifikat zeigt außerdem das Verfallsdatum sowie Details der ausstellenden Zertifizierungsstelle an.

## Wie funktioniert TLS?
{:#cis-faq-how-does-tls-work}
{: faq}

Wenn ein Browser eine Verbindung mit einer durch TLS gesicherten Website startet, ruft er zunächst das TLS-Zertifikat der Site ab, um zu prüfen, ob dieses noch gültig ist. Der Browser verifiziert, dass die Zertifizierungsstelle vertrauenswürdig ist und dass das Zertifikat von der Website verwendet wird, für die es ausgegeben wurde. Schlägt eine dieser Prüfungen fehl, wird eine Warnung angezeigt, dass die Website nicht durch ein gültiges Zertifikat gesichert ist.

Wenn ein TLS-Zertifikat auf einem Web-Server installiert ist, ermöglicht es eine sichere Verbindung zwischen dem Web-Server und dem damit verbundenen Browser. Der Website der URL wird 'https' anstelle von 'http' vorangestellt und in der Adressleiste wird ein Vorhängeschloss angezeigt. Wenn die Website ein EV-Zertifikat (Extended Validation, erweiterte Validierung) verwendet, kann im Browser auch eine grüne Adressleiste angezeigt werden.

## Warum wird eine Datenschutzwarnung angezeigt?
{:#cis-faq-privacy-warning}
{: faq}

Die TLS-Zertifikate, die von IBM Cloud CIS ausgestellt werden, decken die Rootdomäne (`beispiel.com`) und eine Unterdomäne (`*.beispiel.com`) ab. Wenn Sie versuchen, eine Unterdomäne der zweiten Ebene (`*.*.beispiel.com`) zu erreichen, wird in Ihrem Browser eine Warnung zum Datenschutz angezeigt, da diese Hostnamen nicht zum SAN hinzugefügt werden.

Es kann bis zu 15 Minuten dauern, bis eine unserer Partnerzertifizierungsstellen ein neues Zertifikat ausstellt. Solange Ihr neues Zertifikat noch nicht ausgestellt wurde, wird in Ihrem Browser eine Warnung zum Datenschutz angezeigt.

## Warum werden Fehler wegen ungültiger SSL-Zertifikate angezeigt? 
{:#cis-faq-invalid-ssl-cert-error}
{: faq}

Wenn Sie den "Fehler 526, Ungültiges SSL-Zertifikat" sehen, wenn Sie Ihre Site besuchen, kann das bedeuten, dass Ihr Ursprungszertifikat ungültig ist. Wenn der CIS-Proxy aktiviert ist, ist ein gültiges CA-signiertes Zertifikat, das 'End-to-End-CA-signiert' ist, am Ursprung im SSL-Standardmodus erforderlich. Beachten Sie, dass die Einstellung für den SSL-Modus zuvor "End-to-End-flexibel" lautete und dass die vorherige Einstellung die Gültigkeit eines Zertifikats, das vom Ursprung präsentiert wurde, ignoriert hat. Der neue Standardwert wird nur auf Domänen angewendet, die neu hinzugefügt wurden. Wenn Ihre Domäne hinzugefügt wurde, als der SSL-Modus standardmäßig 'End-to-End-flexibel' lautete, wird diese Einstellung nicht überschrieben. Sie können den Modus in einen weniger strengen Modus ändern. Dies wird jedoch für Produktionsumgebungen nicht empfohlen. 

## Was ist DDoS?
{:#cis-faq-what-is-ddos}
{: faq}

Ein dezentraler Denial-of-Service-Angriff (Distributed Denial of Service, DDoS) ist ein Versuch, einen Onlineservice auszuhebeln, indem er mit Datenverkehr aus mehreren Quellen überschwemmt wird. Bei einem DDoS-Angriff greifen mehrere Computersysteme gemeinsam ein Ziel wie einen Server, eine Website oder andere Netzressourcen an, wodurch die Benutzer der Zielressourcen in ihrer Arbeit beeinträchtigt werden.

Die Flut von eingehenden Nachrichten, Verbindungsanforderungen oder fehlerhaften Paketen an das Zielsystem führt zu einer Verlangsamung oder sogar zum Absturz und zum Herunterfahren des Systems. Berechtigte Benutzer können den Service nicht länger nutzen. DDoS-Angriffe waren und sind Mittel zum Zweck diverser Bedrohungsakteure, von einzelnen kriminellen Hackern bis hin zu organisiertem Verbrechen und Regierungsbehörden.

## Was kann ich tun, wenn ich Ziel eines DDoS-Angriffs bin?
{:#cis-faq-what-to-do-in-ddos}
{: faq}

**Schritt 1:** Aktivieren Sie in der Anzeige **Übersicht** den 'Verteidigungsmodus'. 

![Verteidigungsmodus](images/defense-mode.png)

**Schritt 2:** Legen Sie für Ihre DNS-Datensätze maximale Sicherheit fest.

**Schritt 3:** Drosseln Sie die Anforderungen von IBM CIS nicht, wir benötigen eine möglichst große Bandbreite, um Sie in Ihrer Situation zu unterstützen.

**Schritt 4:** Blockieren Sie ggf. bestimmte Länder und Besucher.

## Ich bekomme einen 522-Fehler. Was mache ich jetzt?
{:#cis-faq-522-error}
{: faq}

Ein 522-Fehler gibt an, dass wir keine Verbindung mit Ihrem Ursprungsserver (d. h. Ihrem Host) herstellen konnten. Wenn wir nach ca. 15 Sekunden keine Verbindung herstellen können, schließen wir die Verbindung und zeigen eine 522-Fehlerseite an.

Dieses Problem wird üblicherweise von einer Firewall oder Sicherheitssoftware hervorgehoben, die unsere IP-Adressen unbeabsichtigt blockiert. Da CIS als Reverse Proxy agiert, kann es den Anschein haben, dass Verbindungen mit Ihrer Site von einer Reihe von CIS-IPs stammen. Dieses Verhalten kann dazu führen, dass bestimmte Firewalls diese Verbindungen blockieren und wir folglich den Besuchern Ihrer Website Inhalte nicht mehr ordnungsgemäß bereitstellen können.

Sie können dieses Problem beheben, indem Sie Ihren Host auffordern, alle CIS-IP-Bereiche, die [hier](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses) aufgelistet sind, in die Whitelist aufzunehmen.

Alle diese IPs müssen in der Whitelist enthalten sein, um 522-Fehler zu vermeiden. Es lohnt sich auch, zu prüfen, ob IPs in diesen Bereichen blockiert werden.

522-Fehler können auch durch Netzkonnektivitätsprobleme verursacht werden. Stellen Sie also grundsätzlich sicher, dass Ihr Server und Ihr Netz in einwandfreiem Zustand und nicht überlastet sind.

Wenn Sie nach der Ausführung der oben genannten Schritte immer noch Fehler erhalten, wenden Sie sich an den IBM CIS Support und bestätigen Sie Folgendes: 

* Unsere IP-Bereiche sind in Ihrer Whitelist aufgeführt.
* Ihr Server/Netz ist online und in einwandfreiem Zustand.

Wenn Sie unser Support-Team kontaktieren, geben Sie die Ray ID eines kürzlich angezeigten 522-Fehlers an. Wir können anhand dieser ID bestimmen, welches CIS-Rechenzentrum Sie nutzen und weitere Tests ausführen.

## Was ist ein Proxy-Datensatz und wozu brauche ich ihn?
{:#cis-faq-proxied-record}
{: faq}

Proxy-Datensätze sind Datensätze, die ihren Datenverkehr über IBM CIS weiterleiten. Nur Proxy-Datensätze können die Vorteile von CIS wie beispielsweise IP-Masking nutzen. Dabei wird Ihre Ursprungs-IP durch eine CIS-IP ersetzt, um sie zu schützen:

```
$ whois 104.28.22.57 | grep OrgName
OrgName:        IBM
```

Wenn Sie CIS in einer Domäne lieber umgehen möchten (DNS werden weiter aufgelöst), dann ist das Nicht-Weiterleiten des Datensatzes eine mögliche Lösung. 

## Ich bekomme einen DNS-Validierungsfehler 1004; was kann ich jetzt tun?
{:#cis-faq-dns-validation-error}
{: faq}

Damit Seitenregeln funktionieren, muss DNS für Ihre Zone aufgelöst werden. Sie müssen folglich über einen Proxy-DNS-Datensatz für Ihre Zone verfügen. 

## Kann ich einen CNAME für einen Stammdatensatz hinzufügen? 
{:#cis-faq-add-cname-root-record}
{: faq}

Ja. IBM CIS unterstützt eine Funktion mit dem Namen "CNAME-Vereinfachung", mit der unsere Benutzer einen CNAME als Stammdatensatz hinzufügen können. Unsere autoritativen DNS-Server zählen die Datensätze des CNAME-Ziels auf und antworten mit den Datensätzen anstelle des CNAMEs selbst. Dadurch wird die Tatsache wirksam verdeckt, dass der Benutzer einen CNAME im Stammverzeichnis der Domäne konfiguriert hat. 

## Wie lang ist das Standardzeitlimit bei der Statusprüfung? 
{:#cis-faq-default-health-check-timeout}
{: faq}

Das Standardzeitlimit für die Statusprüfung beträgt für die Pläne "Free Trial" und "Standard" 60 Sekunden.

## Können Statusprüfungen für Nicht-HTTP/HTTPS-Verkehr konfiguriert werden?
{:#cis-faq-health-check-non-http-traffic}
{: faq}

Nein, sie können nur für HTTP/HTTPS konfiguriert werden.

## Kann eine GLB für Nicht-HTTP/HTTPS-Datenverkehr konfiguriert werden?
{:#cis-faq-glb-non-http-traffic}
{: faq}

Nein, sie kann nur für HTTP/HTTPS konfiguriert werden.

## Führt die Inaktivierung aller meiner Ursprünge in einem Ursprungspool dazu, dass der gesamte Ursprungspool selbst inaktiviert wird? 
{:#cis-faq-disabling-origins-disable-origin-pool}
{: faq}

Ja, wenn der Ursprungspool in einer Lastausgleichsfunktion verwendet wird, wird der Datenverkehr an den nächsthöchsten Prioritätspool oder den Ausweichpool weitergeleitet.

## Ich habe einen Fehler in meinem Kubernetes Ingress, was soll ich tun?
{:#cis-faq-kubernetes-ingress-error}
{: faq}

Der Hostname in einer Kubernetes Ingress muss aus alphanumerischen Zeichen in Kleinbuchstaben, '-' oder '.' bestehen und mit einem alphanumerischen Zeichen beginnen und enden. Die Verwendung des Unterstrichs `_` im Namen der Lastausgleichsfunktion kann - obwohl sie zulässig ist - zu einem Ingress-Fehler bei den Kubernetes-Clustern führen. Wir empfehlen, den Unterstrich `_` in Namen für die Lastausgleichsfunktion nicht zu verwenden, um Probleme mit Kubernetes-Clustern zu vermeiden.

## Ich habe einen Fehler 502 erhalten, als ich versucht habe, eine Edge-Funktionsaktion zu speichern. Was soll ich tun? 
{:#cis-faq-502-error}
{: faq}

Wenden Sie sich an den [IBM Support](/docs/infrastructure/cis?topic=cis-getting-help-and-support) und stellen Sie das Script zur Verfügung, das Sie  speichern wollten. 
