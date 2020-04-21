---

copyright:
  years: 2018, 2020
lastupdated: "2020-04-10"

keywords: IBM Cloud Internet Services, CIS Activity Tracker events

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}


# Auditing events for {{site.data.keyword.cis_short_notm}}
{: #at_events}

As a security officer, auditor, or manager, you can use the Activity Tracker service to track how users and applications interact with the {{site.data.keyword.cis_short_notm}} service in {{site.data.keyword.cloud}}.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see the [getting started tutorial for {{site.data.keyword.at_full_notm}}](/docs/Activity-Tracker-with-LogDNA?topic=logdnaat-getting-started#getting-started).

## List of events: DNS domains
{: #events_dns_domain}

The following table lists the actions that are related to DNS domains and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.zones.create|Create a DNS domain.|
|internet-svcs.zones.update|Update a DNS domain.|
|internet-svcs.zones.delete|Delete a DNS domain.|
|internet-svcs.zones_activation_check.update|Perform activation check for a DNS domain.|
|internet-svcs.dnssec.update|Enable or Disable DNSSEC for a DNS domain.|

## List of events: DNS records
{: #events_dns_record}

The following table lists the actions that are related to DNS records and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.dns_records.create|Create a DNS record.|
|internet-svcs.dns_records.update|Update a DNS record.|
|internet-svcs.dns_records.delete|Delete a DNS record.|
|internet-svcs.dns_records_bulk.create|Import DNS records from zone file.|


## List of events: Load balancers
{: #events_load_balancers}

The following table lists the actions that are related to load balancers and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.load_balancers.create|Create a global load balancer.|
|internet-svcs.load_balancers.update|Update a global load balancer.|
|internet-svcs.load_balancers.delete|Delete a global load balancer.|
|internet-svcs.load_balancer_monitors.create|Create a global load balancer healthcheck.|
|internet-svcs.load_balancer_monitors.update|Update a global load balancer healthcheck.|
|internet-svcs.load_balancer_monitors.delete|Delete a global load balancer healthcheck.|
|internet-svcs.load_balancer_pools.create|Create a global load balancer pool.|
|internet-svcs.load_balancer_pools.update|Update a global load balancer pool.|
|internet-svcs.load_balancer_pools.delete|Delete a global load balancer pool.|


## List of events: Purging the cache
{: #events_cache}

The following table lists the actions that are related to purging the cache and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.purge_cache_all.update|Purge all cached assets of a domain from edge server.|
|internet-svcs.purge_cache_by_urls.update|Purge cached assets by URLs from edge server.|
|internet-svcs.purge_cache_by_cache_tags.update|Purge cached assets by cache tags from edge server.|
|internet-svcs.purge_cache_by_hosts.update|Purge cached assets by hostnames from edge server.|


## List of events: Page rules
{: #events_page_rules}

The following table lists the actions that are related to page rules and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.pagerules.create|Create a page rule.|
|internet-svcs.pagerules.update|Update a page rule.|
|internet-svcs.pagerules.delete|Delete a page rule.|


## List of events: Firewalls
{: #events_firewalls}

The following table lists the actions that are related to firewalls and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.waf_groups.update|Enable or Disable a group of WAF rule sets.|
|internet-svcs.waf_rules.update|Enable or Disable a WAF rule.|
|internet-svcs.ip_firewall_rules.create|Create IP firewall rule at domain level or instance level.|
|internet-svcs.ip_firewall_rules.update|Update IP firewall rule at domain level or instance level.|
|internet-svcs.ip_firewall_rules.delete|Delete IP firewall rule at domain level or instance level.|
|internet-svcs.filters.create|Create filters.|
|internet-svcs.filters.update|Update filters.|
|internet-svcs.filters.delete|Delete filters.|
|internet-svcs.filters_validate_expr.create|Validate a filter expression.|
|internet-svcs.firewall_rules.create|Create filter based firewall rule.|
|internet-svcs.firewall_rules.update|Update filter based firewall rule.|
|internet-svcs.firewall_rules.delete|Delete filter based firewall rule.|
|internet-svcs.ua_rules.create|Create user agent blocking rule.|
|internet-svcs.ua_rules.update|Update user agent blocking rule.|
|internet-svcs.ua_rules.delete|Delete user agent blocking rule.|
|internet-svcs.domain_lockdown_rules.create|Create domain lockdown rule.|
|internet-svcs.domain_lockdown_rules.update|Update domain lockdown rule.|
|internet-svcs.domain_lockdown_rules.delete|Delete domain lockdown rule.|

## List of events: Rate limiting
{: #events_rate_limiting}

The following table lists the actions that are related to rate limiting and generate an event:

|Action|Description|
|---|---|
|internet-svcs.rate_limits.create|Create rate limiting rule.|
|internet-svcs.rate_limits.update|Update rate limiting rule.|
|internet-svcs.rate_limits.delete|Delete rate limiting rule.|

## List of events: Routing
{: #events_routing}

The following table lists the actions that are related to routing and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.smart_routing.update|Enable or disable smart routing.|
|internet-svcs.tiered_caching.update|Enable or disable tiered caching.|

## List of events: Certificate packs
{: #events_certificate_packs}

The following table lists the actions that are related to certificate packs and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.certificate_packs.create|Order a dedicated wildcard or custom certificate.|
|internet-svcs.certificate_packs.delete|Delete a dedicated wildcard or custom certificate.|


## List of events: Custom certificates
{: #events_custom_certificate}

The following table lists the actions that are related to custom certificates and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.custom_certificates.create|Upload a custom certificate.|
|internet-svcs.custom_certificates.update|Update a custom certificate.|
|internet-svcs.custom_certificates.delete|Delete a custom certificate.|

## List of events: Origin certificates
{: #events_origin_certificate}

The following table lists the actions that are related to origin certificates and generate an event:

|Action|Description|
|---|---|
|internet-svcs.origin_certificates.create|Create an origin certificate.|
|internet-svcs.origin_certificates.delete|Revoke an origin certificate.|

## List of events: Edge Functions
{: #events_edge_functions}

The following table lists the actions that are related to edge functions and generate an event:

|Action|Description|
|---|---|
|internet-svcs.edge_functions_scripts.create|Create an edge functions script.|
|internet-svcs.edge_functions_scripts.update|Update a new version of edge functions script.|
|internet-svcs.edge_functions_scripts.delete|Delete an edge functions script.|
|internet-svcs.edge_functions_routes.create|Create an edge functions route.|
|internet-svcs.edge_functions_routes.update|Update an edge functions route.|
|internet-svcs.edge_functions_routes.delete|Delete an edge functions route.|

## List of events: Range Applications
{: #events_range_apps}

The following table lists the actions that are related to range applications and generate an event:

|Action|Description|
|---|---|
|internet-svcs.range_apps.create|Create a range application.|
|internet-svcs.range_apps.update|Update a range application.|
|internet-svcs.range_apps.delete|Delete a range application.|

## List of events: Logpush
{: #events_logpush}

The following table lists the actions that are related to Logpush and generate an event:

|Action|Description|
|---|---|
|internet-svcs.logpush_ownership.create|Initiate logpush ownership challenge.|
|internet-svcs.logpush_ownership_validate.create|Validate logpush ownership challenge.|
|internet-svcs.logpush_jobs.create|Create a logpush job.|
|internet-svcs.logpush_jobs.update|Update a logpush job.|
|internet-svcs.logpush_jobs.delete|Delete a logpush job.|

## List of events: Custom error pages
{: #events_custom_error_pages}

The following table lists the actions that are related to custom error pages and generate an event:

|Action|Description|
|---|---|
|internet-svcs.custom_pages.create|Create a custom error page.|
|internet-svcs.custom_pages.update|Update a custom error page.|

## List of events: Settings
{: #events_settings}

The following table lists the actions that are related to configuring settings and generate an event:

|Action|Description|
|---|---|  
|internet-svcs.cache_level_setting.update|Change caching level.|
|internet-svcs.browser_cache_ttl_setting.update|Change browser cache TTL.|
|internet-svcs.development_mode_setting.update|Enable or Disable development mode.|
|internet-svcs.security_level_setting.update|Change security level.|
|internet-svcs.ssl_setting.update|Change SSL setting.|
|internet-svcs.tls_1_2_only_setting.update|Enable or Disable TLS 1.2 support.|
|internet-svcs.waf_setting.update|Enable or Disable web application firewall.|
|internet-svcs.cname_flattening_setting.update|Change CNAME flattening setting.|
|internet-svcs.always_online_setting.update|Enable or disable serve stale content for the domain.|
|internet-svcs.sort_query_string_for_cache_setting.update|Enable or disable sorting query arguments when querying content in cache.|
|internet-svcs.tls_1_3_setting.update|Change TLS 1.3 setting.|
|internet-svcs.automatic_https_rewrites_setting.update|Enable or disable automatic HTTPS rewrites.
|internet-svcs.opportunistic_encryption_setting.update|Enable or disable opportunistic encryption.|
|internet-svcs.browser_check_setting.update|Enable or disable browser integrity check.|
|internet-svcs.challenge_ttl_setting.update|Update challenge TTL.|
|internet-svcs.always_use_https_setting.update|Enable or disable always use HTTPS.|
|internet-svcs.true_client_ip_header_setting.update|Enable or disable True client IP header.|
|internet-svcs.image_size_optimization_setting.update|Enable or disable image size optimization.|
|internet-svcs.script_load_optimization_setting.update|Enable or disable script load optimization.|
|internet-svcs.image_load_optimization_setting.update|Enable or disable image load optimization.|
|internet-svcs.minify_setting.update|Enable or disable minification for HTML, CSS or JavaScript files.|
|internet-svcs.min_tls_version_setting.update|Change minimum TLS version.|
|internet-svcs.ip_geolocation_setting.update|Enable or disable IP geolocation header.|
|internet-svcs.http2_setting.update|Enable or disable HTTP2 for the domain.|
|internet-svcs.max_upload_setting.update|Change the amount of data visitors can upload to the website in a single request.|
|internet-svcs.origin_error_page_pass_thru_setting.update|Enable or disable the proxy of 502 and 504 error pages returned from origin server.|


## Viewing events
{: #ui}

Currently, events are available in the **Frankfurt** region. 

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_full_notm}} service in the same location where your service instance is available. For more information, see [Launching the web UI through the IBM Cloud UI](/docs/Activity-Tracker-with-LogDNA?topic=logdnaat-launch#launch_step2).

## Additional information
{: #info}

When you monitor {{site.data.keyword.at_full_notm}} events that are generated by the {{site.data.keyword.cis_full_notm}}, and you identify an API request for which you need additional information, check the `requestData` field in the event. Open a support case and include the value of the field **X-CORRELATION-ID** that is available in requestData.
