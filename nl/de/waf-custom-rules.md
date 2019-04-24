---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: WAF Custom Rules, Custom WAF Rules

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Angepasste WAF-Regeln
{:#waf-custom-rules}

Navigieren Sie zu Angepassten WAF-Regeln über **Sicherheit > Web Application Firewall > Angepasste Regeln**. WAF-Regeln sind in Enterprise-Plänen verfügbar und werden auf Basis der eindeutigen Anforderungen des Kunden und/oder der Muster seines Websitedatenverkehrs erstellt. Dies bedeutet, dass Sie uns bitten können, praktisch jede Kombination von Merkmalen einer Anfrage zu blockieren. 

Angepasste WAF-Regeln greifen in Situationen, in denen IBM WAF noch keine Regel zur Hand hat und der Angreifer ein bestimmtes Muster oder einen Benutzeragenten verwendet, das bzw. der speziell für die Struktur Ihrer Website bestimmt ist. In diesen Situationen können Sie eine angepasste Regel für Ihre Webeigenschaft erstellen. 

## Angepasste Regel anfordern
{:#request-a-custom-rule}

Um eine Regel anzufordern, schreiben Sie eine E-Mail mit den Regelanforderungen und den Datenverkehrsmustern an wafsup@us.ibm.com.  

Stellen Sie so viele Informationen wie möglich zur Verfügung. Dazu gehören: 
* Zugriffsprotokolle, mit einem Beispiel von ca. 100 mutmaßlich schädlichen Anforderungen. 
* Eine POST-Beispielanforderung inklusive der POST-Daten (wenn die Anforderung über einen POST-Hauptteil verfügt), um zu bestimmen, ob die Anforderung Elemente enthält, die blockiert oder als Auslöser verwendet werden können. 
* Angaben dazu, ob Sie möchten, dass die Anforderung bei möglichen Fehlalarmen sofort blockiert oder ob eine Sicherheitsabfrage gestellt werden soll. 
* Die spezifischen Domänen, für die Sie diese Regeln anwenden möchten. 
* Angaben dazu, ob die Regeln standardmäßig ein- oder ausgeschaltet sein sollen. 

Nachdem Ihre angepassten WAF-Regeln erstellt wurden, müssen Sie alle angepassten Regeln für sie aktivieren, damit sie wirksam werden.
{:note}
