---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM Cloud Internet Services, CIS Activity Tracker events

subcollection: cis

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# CIS {{site.data.keyword.cloudaccesstrailshort}}-Ereignisse
{: #at_events}

Verwenden Sie den {{site.data.keyword.cloudaccesstrailfull}}-Service, um zu überwachen, wie Benutzer und Anwendungen mit dem IBM Cloud Internet Services (CIS) in der {{site.data.keyword.cloud}} interagieren.
{:shortdesc}

Der {{site.data.keyword.cloudaccesstrailfull_notm}}-Service zeichnet vom Benutzer initiierte Aktivitäten auf, die den Status des Service in der {{site.data.keyword.cloud_notm}} ändern. Weitere Informationen finden Sie unter [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla).




## Liste der Ereignisse: DNS-Domänen
{: #events_dns_domain}

In der folgenden Tabelle sind die Aktionen aufgelistet, die sich auf DNS-Domänen beziehen und ein Ereignis generieren:

|Aktion|Beschreibung|
|---|---|  
|internet-svcs.zones.create|Erstellt eine DNS-Domäne.|
|internet-svcs.zones.update|Aktualisiert eine DNS-Domäne. |
|internet-svcs.zones.delete|Löscht eine DNS-Domäne. |
|internet-svcs.zones.activation_check.update|Führt eine Aktivierungsprüfung für eine DNS-Domäne aus. |
|internet-svcs.zones.dnssec.update|Aktiviert oder inaktiviert DNSSEC für eine DNS-Domäne. |

## Liste der Ereignisse: DNS-Datensätze
{: #events_dns_record}

In der folgenden Tabelle sind die Aktionen aufgelistet, die sich auf DNS-Datensätze beziehen und ein Ereignis generieren:

|Aktion|Beschreibung|
|---|---|  
|internet-svcs.zones.dns_records.create|Erstellt einen DNS-Datensatz. |
|internet-svcs.zones.dns_records.update|Aktualisiert einen DNS-Datensatz. |
|internet-svcs.zones.dns_records.delete|Löscht einen DNS-Datensatz. |
|internet-svcs.zones.dns_records_bulk.create|Importiert DNS-Datensätze aus einer Zonendatei. |


## Liste der Ereignisse: Lastausgleichsfunktionen 
{: #events_load_balancers}

In der folgenden Tabelle sind die Aktionen aufgelistet, die sich auf Lastausgleichsfunktionen beziehen und ein Ereignis generieren:

|Aktion|Beschreibung|
|---|---|  
|internet-svcs.zones.load_balancers.create|Erstellt eine globale Lastausgleichsfunktion. |
|internet-svcs.zones.load_balancers.update|Aktualisiert eine globale Lastausgleichsfunktion. |
|internet-svcs.zones.load_balancers.delete|Löscht eine globale Lastausgleichsfunktion. |
|internet-svcs.load_balancers.monitors.create|Erstellt eine Statusüberwachung. |
|internet-svcs.load_balancers.monitors.update|Aktualisiert eine Statusüberwachung. |
|internet-svcs.load_balancers.monitors.delete|Löscht eine Statusüberwachung. |
|internet-svcs.load_balancers.pools.create|Erstellt einen globalen Pool für Lastausgleichsfunktionen. |
|internet-svcs.load_balancers.pools.update|Aktualisiert einen globalen Pool für Lastausgleichsfunktionen. |
|internet-svcs.load_balancers.pools.delete|Löscht einen globalen Pool für Lastausgleichsfunktionen. |


## Liste der Ereignisse: Bereinigung des Cache
{: #events_cache}

In der folgenden Tabelle sind die Aktionen aufgelistet, die sich auf das Bereinigen des Cache beziehen und ein Ereignis generieren:

|Aktion|Beschreibung|
|---|---|  
|internet-svcs.zones.purge_cache.purge_all.update|Bereinigt alle zwischengespeicherten Assets einer Domäne vom Edge-Server. |
|internet-svcs.zones.purge_cache.purge_by_urls.update|Bereinigt alle zwischengespeicherten Assets nach URLs vom Edge-Server. |
|internet-svcs.zones.purge_cache.purge_by_cache_tags.update|Bereinigt zwischengespeicherte Assets nach Cache-Tags vom Edge-Server. |
|internet-svcs.zones.purge_cache.purge_by_hosts.update|Bereinigt zwischengespeicherte Assets nach Hostnamen vom Edge-Server. |


## Liste der Ereignisse: Seitenregeln 
{: #events_page_rules}

In der folgenden Tabelle sind die Aktionen aufgelistet, die sich auf Seitenregeln beziehen und ein Ereignis generieren:

|Aktion|Beschreibung|
|---|---|  
|internet-svcs.zones.pagerules.create|Erstellt eine Seitenregel. |
|internet-svcs.zones.pagerules.update|Aktualisiert eine Seitenregel. |
|internet-svcs.zones.pagerules.delete|Löscht eine Seitenregel. |


## Liste der Ereignisse: Firewalls
{: #events_firewalls}

In der folgenden Tabelle sind die Aktionen aufgelistet, die sich auf Firewalls beziehen und ein Ereignis generieren:

|Aktion|Beschreibung|
|---|---|  
|internet-svcs.zones.firewall.waf.packages.groups.update|Aktiviert oder inaktiviert eine Gruppe von WAF-Regelsätzen. |
|internet-svcs.zones.firewall.waf.packages.rules.update|Aktiviert oder inaktiviert eine WAF-Regel. |
|internet-svcs.zones.firewall.access_rules.rules.create|Erstellt eine IP-Firewallregel auf Domänenebene. |
|internet-svcs.zones.firewall.access_rules.rules.update|Aktualisiert eine IP-Firewallregel auf Domänenebene. |
|internet-svcs.zones.firewall.access_rules.rules.delete|Löscht eine IP-Firewallregel auf Domänenebene. |
|internet-svcs.firewall.access_rules.rules.create|Erstellt eine IP-Firewallregel auf Instanzebene. |
|internet-svcs.firewall.access_rules.rules.update|Aktualisiert eine IP-Firewallregel auf Instanzebene. |
|internet-svcs.firewall.access_rules.rules.delete|Löscht eine IP-Firewallregel auf Instanzebene. |
|internet-svcs.zones.rate_limits.create|Erstellt eine Drosselungsregel. |
|internet-svcs.zones.rate_limits.update|Aktualisiert eine Drosselungsregel. |
|internet-svcs.zones.rate_limits.delete|Löscht eine Drosselungsregel. |
|internet-svcs.zones.ua_rules.create|Erstellt eine Blockierungsregel für den Benutzeragenten. |
|internet-svcs.zones.ua_rules.update|Aktualisiert eine Blockierungsregel für den Benutzeragenten. |
|internet-svcs.zones.ua_rules.delete|Löscht eine Blockierungsregel für den Benutzeragenten. |
|internet-svcs.zones.firewall.lockdowns.create|Erstellt eine Sperrungsregel für die Domäne. |
|internet-svcs.zones.firewall.lockdowns.update|Aktualisiert eine Sperrungsregel für die Domäne. |
|internet-svcs.zones.firewall.lockdowns.delete|Löscht eine Sperrungsregel für die Domäne. |

## Liste der Ereignisse: Routing
{: #events_routing}

In der folgenden Tabelle sind die Aktionen aufgelistet, die sich auf Routing beziehen und ein Ereignis generieren:

|Aktion|Beschreibung|
|---|---|  
|internet-svcs.zones.routing.smart_routing.update	|Aktivieren oder inaktivieren von Smart Routing. |
|internet-svcs.zones.routing.tiered_caching.update	|Aktivieren oder inaktivieren von gestaffeltem Caching. |

## Liste der Ereignisse: Zertifikatpakete
{: #events_certificate_packs}

In der folgenden Tabelle sind die Aktionen aufgelistet, die sich auf Zertifikatpakete beziehen und ein Ereignis generieren:

|Aktion|Beschreibung|
|---|---|  
|internet-svcs.zones.ssl.certificate_packs.create|Bestellen eines dedizierten Zertifikats. |
|internet-svcs.zones.ssl.certificate_packs.delete|Löschen eines dedizierten Zertifikats. |


## Liste der Ereignisse: Angepasste Zertifikate
{: #events_custom_certificate}

In der folgenden Tabelle sind die Aktionen aufgelistet, die sich auf angepasste Zertifikate beziehen und ein Ereignis generieren:

|Aktion|Beschreibung|
|---|---|  
|internet-svcs.zones.custom_certificates.create|Hochladen eines angepassten Zertifikats. |
|internet-svcs.zones.custom_certificates.update|Hochladen eines angepassten Zertifikats. |
|internet-svcs.zones.custom_certificates.delete|Löschen eines angepassten Zertifikats. |


## Liste der Ereignisse: Einstellungen
{: #events_settings}

In der folgenden Tabelle sind die Aktionen aufgelistet, die sich auf angepasste Einstellungen beziehen und ein Ereignis generieren:

|Aktion|Beschreibung|
|---|---|  
|internet-svcs.zones.settings.cache_level.update|Ändern der Caching-Stufe. |
|internet-svcs.zones.settings.browser_cache_ttl.update|Ändern Lebensdauer (TTL) des Browser-Cache.|
|internet-svcs.zones.settings.development_mode.update|Aktivieren oder Inaktivieren des Entwicklungsmodus. |
|internet-svcs.zones.settings.security_level.update|Ändern der Sicherheitsstufe. |
|internet-svcs.zones.settings.ssl.update|Ändern der SSL-Einstellung. |
|internet-svcs.zones.settings.tls_1_2_only.update|Aktivieren oder Inaktivieren der Unterstützung für TLS 1.2. |
|internet-svcs.zones.settings.waf.update|Aktivieren oder Inaktivieren der Web Application Firewall (WAF). |
|internet-svcs.zones.settings.cname_flattening.update|Ändern der Einstellung für die CNAME-Vereinfachung. |
|internet-svcs.zones.settings.always_online.update|Aktivieren oder Inaktivieren des Speicherns nicht aktueller Inhalte für Domänen. |
|internet-svcs.zones.settings.sort_query_string_for_cache.update|Aktivieren oder Inaktivieren der Sortierung von Abfrageargumenten bei der Abfrage von Inhalten im Cache. |
|internet-svcs.zones.settings.tls_1_3.update|Ändern der Einstellung für TLS 1.3. |
|internet-svcs.zones.settings.automatic_https_rewrites.update|Aktivieren oder Inaktivieren von automatischen HTTPS-Neuerstellungen.
|internet-svcs.zones.settings.opportunistic_encryption.update|Aktivieren oder Inaktivieren von opportunistischen Verschlüsselungen. |


## Wo werden Ereignisse angezeigt?
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}}-Ereignisse sind in der {{site.data.keyword.cloudaccesstrailshort}}-**Kontodomäne** in der {{site.data.keyword.cloud_notm}}-Region verfügbar, in der die Ereignisse generiert werden. 



## Zusätzliche Informationen
{: #info}

Wenn Sie {{site.data.keyword.cloudaccesstrailshort}}-Ereignisse überwachen, die von IBM Cloud Internet Services (CIS) generiert wurden, und wenn Sie eine API-Anforderung erkennen, für die Sie weitere Informationen benötigen, überprüfen Sie das Feld 'requestData' im Ereignis. Öffnen Sie ein Ticket und geben Sie den Wert im Feld **X-CORRELATION-ID** an, das in requestData verfügbar ist.
