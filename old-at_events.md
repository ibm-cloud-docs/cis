---

copyright:
  years: 2018, 2022
lastupdated: "2022-01-25"

keywords: CIS Activity Tracker events

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Auditing events for {{site.data.keyword.cis_short_notm}}
{: #old-at_events}

As a security officer, auditor, or manager, you can use the Activity Tracker service to track how users and applications interact with the {{site.data.keyword.cis_short_notm}} service in {{site.data.keyword.cloud}}.
{: shortdesc}

{{site.data.keyword.at_full_notm}} records user-initiated activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use this service to investigate abnormal activity and critical actions and to comply with regulatory audit requirements. In addition, you can be alerted about actions as they happen. The events that are collected comply with the Cloud Auditing Data Federation (CADF) standard. For more information, see the [getting started tutorial for {{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started).

Names for auditing events changed on 1 July 2020. The change replaced all underscore (`_`) characters in the names with dash (`-`) characters.
{: important}

## List of events: DNS domains
{: #events_dns_domain}

The following table lists the actions that are related to DNS domains and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.zones.create`|Create a DNS domain.|
|`internet-svcs.zones.update`|Update a DNS domain.|
|`internet-svcs.zones.delete`|Delete a DNS domain.|
|`internet-svcs.zones-activation-check.update`|Run activation check for a DNS domain.|
|`internet-svcs.dnssec.update`|Enable or disable DNSSEC for a DNS domain.|
{: caption="Table 1. Actions that generate DNS domain events" caption-side="bottom"}

## List of events: DNS records
{: #events_dns_record}

The following table lists the actions that are related to DNS records and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.dns-records.create`|Create a DNS record.|
|`internet-svcs.dns-records.update`|Update a DNS record.|
|`internet-svcs.dns-records.delete`|Delete a DNS record.|
|`internet-svcs.dns-records-bulk.create`|Import DNS records from zone file.|
{: caption="Table 2. Actions that generate DNS record events" caption-side="bottom"}

## List of events: Load balancers
{: #events_load_balancers}

The following table lists the actions that are related to load balancers and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.load-balancers.create`|Create a global load balancer.|
|`internet-svcs.load-balancers.update`|Update a global load balancer.|
|`internet-svcs.load-balancers.delete`|Delete a global load balancer.|
|`internet-svcs.load-balancer-monitors.create`|Create a global load balancer health check.|
|`internet-svcs.load-balancer-monitors.update`|Update a global load balancer health check.|
|`internet-svcs.load-balancer-monitors.delete`|Delete a global load balancer health check.|
|`internet-svcs.load-balancer-pools.create`|Create a global load balancer pool.|
|`internet-svcs.load-balancer-pools.update`|Update a global load balancer pool.|
|`internet-svcs.load-balancer-pools.delete`|Delete a global load balancer pool.|
{: caption="Table 3. Actions that generate load balancer events" caption-side="bottom"}

## List of events: Purging the cache
{: #events_cache}

The following table lists the actions that are related to purging the cache and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.purge-cache-all.update`|Purge all cached assets of a domain from edge server.|
|`internet-svcs.purge-cache-by-urls.update`|Purge cached assets by URLs from edge server.|
|`internet-svcs.purge-cache-by-cache-tags.update`|Purge cached assets by cache tags from edge server.|
|`internet-svcs.purge-cache-by-hosts.update`|Purge cached assets by hostnames from edge server.|
{: caption="Table 4. Actions that generate cache purge events" caption-side="bottom"}

## List of events: Page rules
{: #events_page_rules}

The following table lists the actions that are related to page rules and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.pagerules.create`|Create a page rule.|
|`internet-svcs.pagerules.update`|Update a page rule.|
|`internet-svcs.pagerules.delete`|Delete a page rule.|
{: caption="Table 5. Actions that generate page rule events" caption-side="bottom"}


## List of events: Firewalls
{: #events_firewalls}

The following table lists the actions that are related to firewalls and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.waf-groups.update`|Enable or disable a group of WAF rule sets.|
|`internet-svcs.waf-rules.update`|Enable or disable a WAF rule.|
|`internet-svcs.ip-firewall-rules.create`|Create an IP firewall rule at the domain level or instance level.|
|`internet-svcs.ip-firewall-rules.update`|Update an IP firewall rule at the domain level or instance level.|
|`internet-svcs.ip-firewall-rules.delete`|Delete an IP firewall rule at the domain level or instance level.|
|`internet-svcs.filters.create`|Create filters.|
|`internet-svcs.filters.update`|Update filters.|
|`internet-svcs.filters.delete`|Delete filters.|
|`internet-svcs.filters-validate-expr.create`|Validate a filter expression.|
|`internet-svcs.firewall-rules.create`|Create a filter-based firewall rule.|
|`internet-svcs.firewall-rules.update`|Update a filter-based firewall rule.|
|`internet-svcs.firewall-rules.delete`|Delete a filter-based firewall rule.|
|`internet-svcs.ua-rules.create`|Create a user agent blocking rule.|
|`internet-svcs.ua-rules.update`|Update a user agent blocking rule.|
|`internet-svcs.ua-rules.delete`|Delete a user agent blocking rule.|
|`internet-svcs.domain-lockdown-rules.create`|Create a domain lockdown rule.|
|`internet-svcs.domain-lockdown-rules.update`|Update a domain lockdown rule.|
|`internet-svcs.domain-lockdown-rules.delete`|Delete a domain lockdown rule.|
{: caption="Table 6. Actions that generate firewall events" caption-side="bottom"}

## List of events: Rate limiting
{: #events_rate_limiting}

The following table lists the actions that are related to rate limiting and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.rate-limits.create`|Create a rate limiting rule.|
|`internet-svcs.rate-limits.update`|Update a rate limiting rule.|
|`internet-svcs.rate-limits.delete`|Delete a rate limiting rule.|
{: caption="Table 7. Actions that generate a rate limiting events" caption-side="bottom"}

## List of events: Routing
{: #events_routing}

The following table lists the actions that are related to routing and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.smart-routing.update`|Enable or disable smart routing.|
|`internet-svcs.tiered-caching.update`|Enable or disable tiered caching.|
{: caption="Table 8. Actions that generate routing events" caption-side="bottom"}

## List of events: Certificate packs
{: #events_certificate_packs}

The following table lists the actions that are related to certificate packs and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.certificate-packs.create`|Order a dedicated wildcard or custom certificate.|
|`internet-svcs.certificate-packs.delete`|Delete a dedicated wildcard or custom certificate.|
{: caption="Table 9. Actions that generate certificate pack events" caption-side="bottom"}

## List of events: Custom certificates
{: #events_custom_certificate}

The following table lists the actions that are related to custom certificates and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.custom-certificates.create`|Upload a custom certificate.|
|`internet-svcs.custom-certificates.update`|Update a custom certificate.|
|`internet-svcs.custom-certificates.delete`|Delete a custom certificate.|
{: caption="Table 10. Actions that generate custom certificate events" caption-side="bottom"}

## List of events: Origin certificates
{: #events_origin_certificate}

The following table lists the actions that are related to origin certificates and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.origin-certificates.create`|Create an origin certificate.|
|`internet-svcs.origin-certificates.delete`|Revoke an origin certificate.|
{: caption="Table 11. Actions that generate origin certificate events" caption-side="bottom"}

## List of events: Edge functions
{: #events_edge_functions}

The following table lists the actions that are related to edge functions and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.edge-functions-scripts.create`|Create an edge functions script.|
|`internet-svcs.edge-functions-scripts.update`|Update a new version of edge functions script.|
|`internet-svcs.edge-functions-scripts.delete`|Delete an edge functions script.|
|`internet-svcs.edge-functions-routes.create`|Create an edge functions route.|
|`internet-svcs.edge-functions-routes.update`|Update an edge functions route.|
|`internet-svcs.edge-functions-routes.delete`|Delete an edge functions route.|
{: caption="Table 12. Actions that generate edge functions events" caption-side="bottom"}


## List of events: Range applications
{: #events_range_apps}

The following table lists the actions that are related to range applications and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.range-apps.create`|Create a range application.|
|`internet-svcs.range-apps.update`|Update a range application.|
|`internet-svcs.range-apps.delete`|Delete a range application.|
{: caption="Table 13. Actions that generate range events" caption-side="bottom"}


## List of events: Logpush
{: #events_logpush}

The following table lists the actions that are related to Logpush and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.logpush-ownership.create`|Initiate logpush ownership challenge.|
|`internet-svcs.logpush-ownership-validate.create`|Validate logpush ownership challenge.|
|`internet-svcs.logpush-jobs.create`|Create a logpush job.|
|`internet-svcs.logpush-jobs.update`|Update a logpush job.|
|`internet-svcs.logpush-jobs.delete`|Delete a logpush job.|
{: caption="Table 14. Actions that generate logpush events" caption-side="bottom"}


## List of events: Custom error pages
{: #events_custom_error_pages}

The following table lists the actions that are related to custom error pages and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.custom-pages.create`|Create a custom error page.|
|`internet-svcs.custom-pages.update`|Update a custom error page.|
{: caption="Table 15. Actions that generate custom error page events" caption-side="bottom"}


## List of events: Settings
{: #events_settings}

The following table lists the actions that are related to configuring settings and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.cache-level-setting.update`|Change caching level.|
|`internet-svcs.browser-cache-ttl-setting.update`|Change browser cache TTL.|
|`internet-svcs.development-mode-setting.update`|Enable or disable development mode.|
|`internet-svcs.security-level-setting.update`|Change security level.|
|`internet-svcs.ssl-setting.update`|Change SSL setting.|
|`internet-svcs.tls-1-2-only-setting.update`|Enable or disable TLS 1.2 support.|
|`internet-svcs.waf-setting.update`|Enable or disable web application firewall.|
|`internet-svcs.cname-flattening-setting.update`|Change CNAME flattening setting.|
|`internet-svcs.always-online-setting.update`|Enable or disable serve stale content for the domain.|
|`internet-svcs.sort-query-string-for-cache-setting.update`|Enable or disable sorting query arguments when querying content in cache.|
|`internet-svcs.tls-1-3-setting.update`|Change TLS 1.3 setting.|
|`internet-svcs.automatic-https-rewrites-setting.update`|Enable or disable automatic HTTPS rewrites.
|`internet-svcs.opportunistic-encryption-setting.update`|Enable or disable opportunistic encryption.|
|`internet-svcs.browser-check-setting.update`|Enable or disable browser integrity check.|
|`internet-svcs.challenge-ttl-setting.update`|Update challenge TTL.|
|`internet-svcs.always-use-https-setting.update`|Enable or disable `Always Use HTTPS`.|
|`internet-svcs.true-client-ip-header-setting.update`|Enable or disable True client IP header.|
|`internet-svcs.image-size-optimization-setting.update`|Enable or disable image size optimization.|
|`internet-svcs.script-load-optimization-setting.update`|Enable or disable script load optimization.|
|`internet-svcs.image-load-optimization-setting.update`|Enable or disable image load optimization.|
|`internet-svcs.minify-setting.update`|Enable or disable minification for HTML, CSS, or JavaScript files.|
|`internet-svcs.min-tls-version-setting.update`|Change minimum TLS version.|
|`internet-svcs.ip-geolocation-setting.update`|Enable or disable IP geolocation header.|
|`internet-svcs.http2-setting.update`|Enable or disable HTTP2 for the domain.|
|`internet-svcs.max-upload-setting.update`|Change the amount of data that visitors can upload to the website in a single request.|
|`internet-svcs.origin-error-page-pass-thru-setting.update`|Enable or disable the proxy of 502 and 504 error pages that are returned from origin server.|
|`internet-svcs.bot-management.update`|Change Bot Management settings.|
{: caption="Table 16. Actions that generate settings events" caption-side="bottom"}


## Viewing events
{: #ui}

Currently, events are available in the **Frankfurt** region. 

{{site.data.keyword.at_full_notm}} can have only one instance per location. To view events, you must access the web UI of the {{site.data.keyword.at_full_notm}} service in the same location where your service instance is available. For more information, see [Launching the web UI through the IBM Cloud UI](/docs/activity-tracker?topic=activity-tracker-launch#launch_cloud_ui).

## Additional information
{: #info}

When you monitor {{site.data.keyword.at_full_notm}} events that are generated by the {{site.data.keyword.cis_full_notm}}, and you identify an API request for which you need additional information, check the `requestData` field in the event. 

Open a Support case and include the value of the field **requestId** that is available in requestData.
