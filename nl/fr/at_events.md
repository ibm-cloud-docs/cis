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


# Evénements CIS {{site.data.keyword.cloudaccesstrailshort}}
{: #at_events}

Utilisez le service {{site.data.keyword.cloudaccesstrailfull}} pour suivre la manière dont les utilisateurs et les applications interagissent avec IBM Cloud Internet Services (CIS) dans {{site.data.keyword.cloud}}. {:shortdesc}

Le service {{site.data.keyword.cloudaccesstrailfull_notm}} enregistre les activités initiées par l'utilisateur qui modifient l'état d'un service dans {{site.data.keyword.cloud_notm}}. Pour plus d'informations, voir [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker?topic=cloud-activity-tracker-getting-started-with-cla).




## Liste des événements : domaines DNS 
{: #events_dns_domain}

Le tableau suivant répertorie les actions liées aux domaines DNS et qui génèrent un événement : 

|Action|Description|
|---|---|  
|internet-svcs.zones.create|Créer un domaine DNS.|
|internet-svcs.zones.update|Mettre à jour un domaine DNS.|
|internet-svcs.zones.delete|Supprimer un domaine DNS.|
|internet-svcs.zones.activation_check.update|Effectuer une vérification d'activation pour un domaine DNS.|
|internet-svcs.zones.dnssec.update|Activer ou désactiver DNSSEC pour un domaine DNS.|

## Liste des événements : enregistrements DNS 
{: #events_dns_record}

Le tableau suivant répertorie les actions liées aux enregistrements DNS et qui génèrent un événement : 

|Action|Description|
|---|---|  
|internet-svcs.zones.dns_records.create|Créer un enregistrement DNS.|
|internet-svcs.zones.dns_records.update|Mettre à jour un enregistrement DNS.|
|internet-svcs.zones.dns_records.delete|Supprimer un enregistrement DNS.|
|internet-svcs.zones.dns_records_bulk.create|Importer des enregistrements DNS à partir du fichier de zone.|


## Liste des événements : équilibreurs de charge
{: #events_load_balancers}

Le tableau suivant répertorie les actions liées aux équilibreurs de charge et qui génèrent un événement : 

|Action|Description|
|---|---|  
|internet-svcs.zones.load_balancers.create|Créer un équilibreur de charge global.|
|internet-svcs.zones.load_balancers.update|Mettre à jour un équilibreur de charge global.|
|internet-svcs.zones.load_balancers.delete|Supprimer un équilibreur de charge global.|
|internet-svcs.load_balancers.monitors.create|Créer un moniteur de santé.|
|internet-svcs.load_balancers.monitors.update|Mettre à jour un moniteur de santé.|
|internet-svcs.load_balancers.monitors.delete|Supprimer un moniteur de santé.|
|internet-svcs.load_balancers.pools.create|Créer un pool d'équilibreurs de charge global.|
|internet-svcs.load_balancers.pools.update|Mettre à jour un pool d'équilibreurs de charge global.|
|internet-svcs.load_balancers.pools.delete|Supprimer un pool d'équilibreurs de charge global.|


## Liste des événements : purge de la mémoire cache
{: #events_cache}

Le tableau suivant répertorie les actions liées à la purge de la mémoire cache et qui génèrent un événement : 

|Action|Description|
|---|---|  
|internet-svcs.zones.purge_cache.purge_all.update|Purger tous les actifs mis en cache d'un domaine à partir du serveur de périphérie.|
|internet-svcs.zones.purge_cache.purge_by_urls.update|Purger les actifs mis en cache par URL à partir du serveur de périphérie. |
|internet-svcs.zones.purge_cache.purge_by_cache_tags.update|Purger les actifs mis en cache par balises de cache à partir du serveur de périphérie.|
|internet-svcs.zones.purge_cache.purge_by_hosts.update|Purger les actifs mis en cache par noms d'hôte à partir du serveur de périphérie. |


## Liste des événements : règles de page
{: #events_page_rules}

Le tableau suivant répertorie les actions liées aux règles de page et qui génèrent un événement : 

|Action|Description|
|---|---|  
|internet-svcs.zones.pagerules.create|Créer une page de règle.|
|internet-svcs.zones.pagerules.update|Mettre à jour une page de règle.|
|internet-svcs.zones.pagerules.delete|Supprimer une page de règle.|


## Liste des événements : pare-feux
{: #events_firewalls}

Le tableau suivant répertorie les actions liées aux pare-feux et qui génèrent un événement : 

|Action|Description|
|---|---|  
|internet-svcs.zones.firewall.waf.packages.groups.update|Activer ou désactiver un groupe de jeux de règles WAF. |
|internet-svcs.zones.firewall.waf.packages.rules.update|Activer ou désactiver une règle WAF. |
|internet-svcs.zones.firewall.access_rules.rules.create|Créer une règle de pare-feu IP au niveau du domaine. |
|internet-svcs.zones.firewall.access_rules.rules.update|Mettre à jour une règle de pare-feu IP au niveau du domaine. |
|internet-svcs.zones.firewall.access_rules.rules.delete|Supprimer une règle de pare-feu IP au niveau du domaine. |
|internet-svcs.firewall.access_rules.rules.create|Créer une règle de pare-feu IP au niveau de l'instance. |
|internet-svcs.firewall.access_rules.rules.update|Mettre à jour une règle de pare-feu IP au niveau de l'instance. |
|internet-svcs.firewall.access_rules.rules.delete|Supprimer une règle de pare-feu IP au niveau de l'instance. |
|internet-svcs.zones.rate_limits.create|Créer une règle de limitation de débit.|
|internet-svcs.zones.rate_limits.update|Mettre à jour une règle de limitation de débit.|
|internet-svcs.zones.rate_limits.delete|Supprimer une règle de limitation de débit.|
|internet-svcs.zones.ua_rules.create|Créer une règle de blocage de l'agent utilisateur.|
|internet-svcs.zones.ua_rules.update|Mettre à jour une règle de blocage de l'agent utilisateur.|
|internet-svcs.zones.ua_rules.delete|Supprimer une règle de blocage de l'agent utilisateur.|
|internet-svcs.zones.firewall.lockdowns.create|Créer une règle de verrouillage de domaine.|
|internet-svcs.zones.firewall.lockdowns.update|Mettre à jour une règle de verrouillage de domaine.|
|internet-svcs.zones.firewall.lockdowns.delete|Supprimer une règle de verrouillage de domaine.|

## Liste des événements : routage
{: #events_routing}

Le tableau suivant répertorie les actions liées au routage et qui génèrent un événement : 

|Action|Description|
|---|---|  
|internet-svcs.zones.routing.smart_routing.update	|Activer ou désactiver le routage intelligent.|
|internet-svcs.zones.routing.tiered_caching.update	|Activer ou désactiver la mise en cache multiniveau.|

## Liste des événements : packs de certificats
{: #events_certificate_packs}

Le tableau suivant répertorie les actions liées aux packs de certificats et qui génèrent un événement : 

|Action|Description|
|---|---|  
|internet-svcs.zones.ssl.certificate_packs.create|Commander un certificat dédié.|
|internet-svcs.zones.ssl.certificate_packs.delete|Supprimer un certificat dédié.|


## Liste des événements : certificats personnalisés
{: #events_custom_certificate}

Le tableau suivant répertorie les actions liées aux certificats personnalisés et qui génèrent un événement : 

|Action|Description|
|---|---|  
|internet-svcs.zones.custom_certificates.create|Télécharger un certificat personnalisé. |
|internet-svcs.zones.custom_certificates.update|Mettre à jour un certificat personnalisé. |
|internet-svcs.zones.custom_certificates.delete|Supprimer un certificat personnalisé. |


## Liste des événements : paramètres
{: #events_settings}

Le tableau suivant répertorie les actions liées à la configuration des paramètres et qui génèrent un événement : 

|Action|Description|
|---|---|  
|internet-svcs.zones.settings.cache_level.update|Modifier le niveau de mise en cache. |
|internet-svcs.zones.settings.browser_cache_ttl.update|Modifier la durée de vie du cache du navigateur. |
|internet-svcs.zones.settings.development_mode.update|Activer ou désactiver le mode de développement. |
|internet-svcs.zones.settings.security_level.update|Modifier le niveau de sécurité. |
|internet-svcs.zones.settings.ssl.update|Modifier le paramètre SSL. |
|internet-svcs.zones.settings.tls_1_2_only.update|Activer ou désactiver le support TLS 1.2. |
|internet-svcs.zones.settings.waf.update|Activer ou désactiver le pare-feu de l'application Web. |
|internet-svcs.zones.settings.cname_flattening.update|Modifier le paramètre de mise à plat de CNAME. |
|internet-svcs.zones.settings.always_online.update|Activer ou désactiver le contenu obsolète du domaine. |
|internet-svcs.zones.settings.sort_query_string_for_cache.update|Activer ou désactiver le tri des arguments de requête lors d'une requête de contenu dans le cache. |
|internet-svcs.zones.settings.tls_1_3.update|Modifier le paramètre TLS 1.3. |
|internet-svcs.zones.settings.automatic_https_rewrites.update|Activer ou désactiver les réécritures HTTPS automatiques.
|internet-svcs.zones.settings.opportunistic_encryption.update|Activer ou désactiver le chiffrement opportuniste. |


## Où rechercher les événements ?
{: #ui}

Les événements {{site.data.keyword.cloudaccesstrailshort}} sont disponibles dans le **domaine de compte** {{site.data.keyword.cloudaccesstrailshort}}, lui-même disponible dans la région {{site.data.keyword.cloud_notm}} où les événements sont générés.



## Informations supplémentaires 
{: #info}

Lorsque vous surveillez les événements {{site.data.keyword.cloudaccesstrailshort}} générés par IBM Cloud Internet Services (CIS) et que vous identifiez une demande d'API pour laquelle vous avez besoin d'informations supplémentaires, vérifiez la zone requestData de l'événement. Ouvrez un ticket de demande de service et incluez la valeur de la zone **X-CORRELATION-ID** disponible dans requestData. 
