---
copyright:
  years: 2018
lastupdated: "2018-03-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Bekannte Einschränkungen

 * Wir empfehlen, Chrome zu verwenden. 

 * In Firefox und Safari können die Zeitpunkte, an denen Zertifikate *hochgeladen* und *geändert* wurden bzw. *verfallen* sind, nicht angezeigt werden. 

 * Wenn die URL-Übereinstimmung für eine Seitenregel bearbeitet wird, führt das dazu, dass die Regel die niedrigste Priorität erhält. 
 
 * Ohne eine konfigurierte Domäne können Sie zu **Zuverlässigkeit > Globale Lastausgleichsfunktionen** navigieren, um Ihre Lastausgleichsfunktionspools und Statusprüfungen zu erstellen. Wenn Sie jedoch **Lastausgleichsfunktion erstellen** auswählen, die Lastausgleichsfunktion konfigurieren und auf **1 Ressource bereitstellen** klicken, wird die Anforderung zurückgewiesen, weil eine Domäne erforderlich ist. Diese funktionale Einschränkung erleichtert dem Benutzer das Verständnis des Zwecks von Pools und Überwachungen bei der Erstellung von Lastausgleichsfunktionen. 
 
 * Das Early Access-Programm ist auf eine Instanz pro Konto begrenzt. Nachdem Sie eine Ressourceninstanz erstellt und ihr eine Domäne hinzugefügt haben, sind Sie nicht berechtigt, eine neue Ressourceninstanz für CIS hinzuzufügen. Diese Einschränkung wird auch dann durchgesetzt, wenn Sie eine Testdomäne löschen und dann versuchen, derselben Ressourceninstanz erneut eine Domäne hinzuzufügen. Wenn Sie dies versuchen, tritt ein Fehler auf. 

 * Wenn Sie eine neue Domäne hinzufügen, erfasst oder importiert unser System derzeit nicht Ihre vorhandenen Domänendatensätze. 

 * Im Rahmen dieses Early Access-Programms unterstützen wir die Delegierung von Unterdomänen nur mithilfe von NS-Datensätzen eines anderen Anbieters. Die CNAME-Delegierung wird nicht unterstützt. 
