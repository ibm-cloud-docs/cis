---

copyright:
  years: 2016, 2018

lastupdated: "2018-06-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# CIS {{site.data.keyword.cloudaccesstrailshort}} events
{: #at_events}

Use the {{site.data.keyword.cloudaccesstrailfull}} service to track how users and applications interact with the IBM Cloud Internet Services (CIS) in the {{site.data.keyword.Bluemix}}.
{:shortdesc}

The {{site.data.keyword.cloudaccesstrailfull_notm}} service records user-initiated activities that change the state of a service in the {{site.data.keyword.Bluemix_notm}}. For more information, see [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla).




## List of events: DNS domains
{: #events_dns_domain}

The following table lists the actions that are related to DNS domains and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.zones.create|Create a DNS domain.|
|internet-svcs.zones.update|Update a DNS domain.|
|internet-svcs.zones.delete|Delete a DNS domain.|
|internet-svcs.zones.activation_check.update|Perform activation check for a DNS domain.|
|internet-svcs.zones.dnssec.update|Enable or Disable DNSSEC for a DNS domain.|

## List of events: DNS records
{: #events_dns_record}

The following table lists the actions that are related to DNS records and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.zones.dns_records.create<|Create a DNS record.|
|internet-svcs.zones.dns_records.update|Update a DNS record.|
|internet-svcs.zones.dns_records.delete<|Delete a DNS record.|


## List of events: Load balancers
{: #events_load_balancers}

The following table lists the actions that are related to load balancers and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.zones.load_balancers.create|Create a global load balancer.|
|internet-svcs.zones.load_balancers.update|Update a global load balancer.|
|internet-svcs.zones.load_balancers.delete|Delete a global load balancer.|
|internet-svcs.load_balancers.monitors.create|Create a health monitor.|
|internet-svcs.load_balancers.monitors.update|Update a health monitor.|
|internet-svcs.load_balancers.monitors.delete|Delete a health monitor.|
|internet-svcs.load_balancers.pools.create|Create a global load balancer pool.|
|internet-svcs.load_balancers.pools.update|Update a global load balancer pool.|
|internet-svcs.load_balancers.pools.delete|Delete a global load balancer pool.|


## List of events: Purging the cache
{: #events_cache}

The following table lists the actions that are related to purging the cache and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.zones.purge_cache.purge_all.update|Purge all cached assets of a domain from edge server.|
|internet-svcs.zones.purge_cache.purge_by_urls.update|Purge cached assets by URLs from edge server.|


## List of events: Page rules
{: #events_page_rules}

The following table lists the actions that are related to page rules and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.zones.pagerules.create|Create a page rule.|
|internet-svcs.zones.pagerules.update|Update a page rule.|
|internet-svcs.zones.pagerules.delete|Delete a page rule.|


## List of events: Firewalls
{: #events_firewalls}

The following table lists the actions that are related to firewalls and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.zones.firewall.waf.packages.groups.update|Enable or Disable a group of WAF rule sets.|
|internet-svcs.zones.firewall.waf.packages.rules.update|Enable or Disable a WAF rule.|


## List of events: Certificate packs
{: #events_certificate_packs}

The following table lists the actions that are related to certificate packs and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.zones.ssl.certificate_packs.create|Order a dedicated certificate.|
|internet-svcs.zones.ssl.certificate_packs.delete|Delete a dedicated certificate.|


## List of events: Custom certificates
{: #events_custom_certificate}

The following table lists the actions that are related to custom certificates and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.zones.custom_certificates.create|Upload a custom certificate.|
|internet-svcs.zones.custom_certificates.update|Update a custom certificate.|
|internet-svcs.zones.custom_certificates.delete|Delete a custom certificate.|


## List of events: Settings
{: #events_settings}

The following table lists the actions that are related to configuring settings and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.zones.settings.cache_level.update|Change caching level.|
|internet-svcs.zones.settings.browser_cache_ttl.update|Change browser cache TTL.|
|internet-svcs.zones.settings.development_mode.update|Enable or Disable development mode.|
|internet-svcs.zones.settings.security_level.update|Change security level.|
|internet-svcs.zones.settings.ssl.update|Change SSL setting.|
|internet-svcs.zones.settings.tls_1_2_only.update|Enable or Disable TLS 1.2 support.|
|internet-svcs.zones.settings.waf.update|Enable or Disable web application firewall.|


## Where to look for the events
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} events are available in the {{site.data.keyword.cloudaccesstrailshort}} **account domain** that is available in the {{site.data.keyword.Bluemix_notm}} region where the events are generated.



## Additional information
{: #info}

When you monitor {{site.data.keyword.cloudaccesstrailshort}} events that are generated by the IBM Cloud Internet Services (CIS), and you identify an API request for which you need additional information, check the requestData field in the event. Open a support ticket and include the value of the field **X-CORRELATION-ID** that is available in requestData.
