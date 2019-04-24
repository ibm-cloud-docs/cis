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


# Eventi CIS {{site.data.keyword.cloudaccesstrailshort}}
{: #at_events}

Utilizza il servizio {{site.data.keyword.cloudaccesstrailfull}} per tracciare il modo in cui utenti e applicazioni interagiscono con IBM Cloud Internet Services (CIS) in {{site.data.keyword.cloud}}.
{:shortdesc}

Il servizio {{site.data.keyword.cloudaccesstrailfull_notm}} registra le attività avviate dall'utente che modificano lo stato di un servizio in {{site.data.keyword.cloud_notm}}. Per ulteriori informazioni, vedi [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla).




## Elenco di eventi: domini DNS
{: #events_dns_domain}

La seguente tabella elenca le azioni che sono correlate ai domini DNS e che generano un evento:

|Azione|Descrizione|
|---|---|  
|internet-svcs.zones.create|Crea un dominio DNS.|
|internet-svcs.zones.update|Aggiorna un dominio DNS.|
|internet-svcs.zones.delete|Elimina un dominio DNS.|
|internet-svcs.zones.activation_check.update|Esegue il controllo di attivazione per un dominio DNS.|
|internet-svcs.zones.dnssec.update|Abilita o disabilita DNSSEC per un dominio DNS.|

## Elenco di eventi: record DNS
{: #events_dns_record}

La seguente tabella elenca le azioni che sono correlate ai record DNS e che generano un evento:

|Azione|Descrizione|
|---|---|  
|internet-svcs.zones.dns_records.create|Crea un record DNS.|
|internet-svcs.zones.dns_records.update|Aggiorna un record DNS.|
|internet-svcs.zones.dns_records.delete|Elimina un record DNS.|
|internet-svcs.zones.dns_records_bulk.create|Importa record DNS dal file di zona.|


## Elenco di eventi: programmi di bilanciamento del carico
{: #events_load_balancers}

La seguente tabella elenca le azioni che sono correlate ai programmi di bilanciamento del carico e che generano un evento:

|Azione|Descrizione|
|---|---|  
|internet-svcs.zones.load_balancers.create|Crea un programma di bilanciamento del carico globale.|
|internet-svcs.zones.load_balancers.update|Aggiorna un programma di bilanciamento del carico globale.|
|internet-svcs.zones.load_balancers.delete|Elimina un programma di bilanciamento del carico globale.|
|internet-svcs.load_balancers.monitors.create|Crea un monitoraggio di integrità.|
|internet-svcs.load_balancers.monitors.update|Aggiorna un monitoraggio di integrità.|
|internet-svcs.load_balancers.monitors.delete|Elimina un monitoraggio di integrità.|
|internet-svcs.load_balancers.pools.create|Crea un pool del programma di bilanciamento del carico globale.|
|internet-svcs.load_balancers.pools.update|Aggiorna un pool del programma di bilanciamento del carico globale.|
|internet-svcs.load_balancers.pools.delete|Elimina un pool del programma di bilanciamento del carico globale.|


## Elenco di eventi: pulizia della cache
{: #events_cache}

La seguente tabella elenca le azioni che sono correlate alla pulizia della cache e che generano un evento:

|Azione|Descrizione|
|---|---|  
|internet-svcs.zones.purge_cache.purge_all.update|Elimina tutte le risorse memorizzate nella cache di un dominio dal server edge.|
|internet-svcs.zones.purge_cache.purge_by_urls.update|Elimina le risorse memorizzate nella cache in base agli URL dal server edge.|
|internet-svcs.zones.purge_cache.purge_by_cache_tags.update|Elimina le risorse memorizzate nella cache in base alle tag della cache dal server edge.|
|internet-svcs.zones.purge_cache.purge_by_hosts.update|Elimina le risorse memorizzate nella cache in base ai nomi host dal server edge.|


## Elenco di eventi: regole della pagina
{: #events_page_rules}

La seguente tabella elenca le azioni che sono correlate alle regole della pagina e che generano un evento:

|Azione|Descrizione|
|---|---|  
|internet-svcs.zones.pagerules.create|Crea una pagina delle regole.|
|internet-svcs.zones.pagerules.update|Aggiorna una pagina delle regole.|
|internet-svcs.zones.pagerules.delete|Elimina una pagina delle regole.|


## Elenco di eventi: firewall
{: #events_firewalls}

La seguente tabella elenca le azioni che sono correlate ai firewall e che generano un evento:

|Azione|Descrizione|
|---|---|  
|internet-svcs.zones.firewall.waf.packages.groups.update|Abilita o disabilita un gruppo di serie di regole WAF.|
|internet-svcs.zones.firewall.waf.packages.rules.update|Abilita o disabilita una regola WAF.|
|internet-svcs.zones.firewall.access_rules.rules.create|Crea una regola del firewall IP a livello di dominio.|
|internet-svcs.zones.firewall.access_rules.rules.update|Aggiorna una regola del firewall IP a livello di dominio.|
|internet-svcs.zones.firewall.access_rules.rules.delete|Elimina una regola del firewall IP a livello di dominio.|
|internet-svcs.firewall.access_rules.rules.create|Crea una regola del firewall IP a livello di istanza.|
|internet-svcs.firewall.access_rules.rules.update|Aggiorna una regola del firewall IP a livello di istanza.|
|internet-svcs.firewall.access_rules.rules.delete|Elimina una regola del firewall IP a livello di istanza.|
|internet-svcs.zones.rate_limits.create|Crea una regola che limita la frequenza.|
|internet-svcs.zones.rate_limits.update|Aggiorna una regola che limita la frequenza.|
|internet-svcs.zones.rate_limits.delete|Elimina una regola che limita la frequenza.|
|internet-svcs.zones.ua_rules.create|Crea una regola di blocco dell'agent utente.|
|internet-svcs.zones.ua_rules.update|Aggiorna una regola di blocco dell'agent utente.|
|internet-svcs.zones.ua_rules.delete|Elimina una regola di blocco dell'agent utente.|
|internet-svcs.zones.firewall.lockdowns.create|Crea una regola di blocco del dominio.|
|internet-svcs.zones.firewall.lockdowns.update|Aggiorna una regola di blocco del dominio.|
|internet-svcs.zones.firewall.lockdowns.delete|Elimina una regola di blocco del dominio.|

## Elenco di eventi: instradamento
{: #events_routing}

La seguente tabella elenca le azioni che sono correlate all'instradamento e che generano un evento:

|Azione|Descrizione|
|---|---|  
|internet-svcs.zones.routing.smart_routing.update	|Abilita o disabilita l'instradamento mirato.|
|internet-svcs.zones.routing.tiered_caching.update	|Abilita o disabilita la memorizzazione nella cache a livelli.|

## Elenco di eventi: pacchetti di certificati
{: #events_certificate_packs}

La seguente tabella elenca le azioni che sono correlate ai pacchetti di certificati e che generano un evento:

|Azione|Descrizione|
|---|---|  
|internet-svcs.zones.ssl.certificate_packs.create|Ordina un certificato dedicato.|
|internet-svcs.zones.ssl.certificate_packs.delete|Elimina un certificato dedicato.|


## Elenco di eventi: certificati personalizzati
{: #events_custom_certificate}

La seguente tabella elenca le azioni che sono correlate ai certificati personalizzati e che generano un evento:

|Azione|Descrizione|
|---|---|  
|internet-svcs.zones.custom_certificates.create|Carica un certificato personalizzato.|
|internet-svcs.zones.custom_certificates.update|Aggiorna un certificato personalizzato.|
|internet-svcs.zones.custom_certificates.delete|Elimina un certificato personalizzato.|


## Elenco di eventi: impostazioni
{: #events_settings}

La seguente tabella elenca le azioni che sono correlate alla configurazione delle impostazioni e che generano un evento:

|Azione|Descrizione|
|---|---|  
|internet-svcs.zones.settings.cache_level.update|Modifica il livello di memorizzazione nella cache.|
|internet-svcs.zones.settings.browser_cache_ttl.update|Modifica il TTL della cache del browser.|
|internet-svcs.zones.settings.development_mode.update|Abilita o disabilita la modalità di sviluppo. |
|internet-svcs.zones.settings.security_level.update|Modifica il livello di sicurezza.|
|internet-svcs.zones.settings.ssl.update|Modifica l'impostazione SSL.|
|internet-svcs.zones.settings.tls_1_2_only.update|Abilita o disabilita il supporto TLS 1.2.|
|internet-svcs.zones.settings.waf.update|Abilita o disabilita il firewall dell'applicazione web.|
|internet-svcs.zones.settings.cname_flattening.update|Modifica l'impostazione del flattening di CNAME.|
|internet-svcs.zones.settings.always_online.update|Abilita o disabilita Serve Stale Content per il dominio. |
|internet-svcs.zones.settings.sort_query_string_for_cache.update|Abilita o disabilita l'ordinamento degli argomenti della query quando si esegue la query del contenuto nella cache. |
|internet-svcs.zones.settings.tls_1_3.update|Modifica l'impostazione TLS 1.3.|
|internet-svcs.zones.settings.automatic_https_rewrites.update|Abilita o disabilita le riscritture HTTPS automatiche.
|internet-svcs.zones.settings.opportunistic_encryption.update|Abilita o disabilita la codifica opportunistica.|


## Dove cercare gli eventi
{: #ui}

Gli eventi {{site.data.keyword.cloudaccesstrailshort}} sono disponibili nel {{site.data.keyword.cloudaccesstrailshort}} **dominio dell'account** disponibile nella regione {{site.data.keyword.cloud_notm}} in cui vengono generati gli eventi. 



## Informazioni aggiuntive
{: #info}

Quando monitori gli eventi {{site.data.keyword.cloudaccesstrailshort}} generati da IBM Cloud Internet Services (CIS) e identifichi una richiesta API per la quale necessiti di ulteriori informazioni, controlla il campo requestData nell'evento. Apri un ticket di supporto e includi il valore del campo **X-CORRELATION-ID** disponibile in requestData.
