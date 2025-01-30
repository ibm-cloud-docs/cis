---

copyright:
  years: 2018, 2025
lastupdated: "2025-01-24"

keywords: CIS activity tracker events

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Activity tracking events for {{site.data.keyword.cis_short_notm}}
{: #at_events}

{{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.cis_full_notm}}, generate activity tracking events.
{: shortdesc}

Activity tracking events report on activities that change the state of a service in {{site.data.keyword.cloud_notm}}. You can use the events to investigate abnormal activity and critical actions and to comply with regulatory audit requirements.

You can use {{site.data.keyword.atracker_full_notm}}, a platform service, to route auditing events in your account to destinations of your choice by configuring targets and routes that define where activity tracking events are sent. For more information, see [About {{site.data.keyword.atracker_full_notm}}](/docs/atracker?topic=atracker-about).

You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.



As of 28 March 2024, the {{site.data.keyword.at_full_notm}} service is deprecated and will no longer be supported as of 30 March 2025. Customers will need to migrate to {{site.data.keyword.logs_full_notm}} before 30 March 2025. During the migration period, customers can use {{site.data.keyword.at_full_notm}} along with {{site.data.keyword.logs_full_notm}}. Activity tracking events are the same for both services. For information about migrating from {{site.data.keyword.at_full_notm}} to {{site.data.keyword.logs_full_notm}} and running the services in parallel, see [migration planning](/docs/cloud-logs?topic=cloud-logs-migration-intro).
{: important}

## Locations where activity tracking events are generated
{: #at-locations}

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are generated in Americas locations" caption-side="top"}
{: #at-gen-table-1}
{: tab-title="Americas"}
{: tab-group="at-gen"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are generated in Asia Pacific locations" caption-side="top"}
{: #at-gen-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="at-gen"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are generated in Europe locations" caption-side="top"}
{: #at-gen-table-3}
{: tab-title="Europe"}
{: tab-group="at-gen"}
{: class="simple-tab-table"}
{: row-headers}

## Locations where activity tracking events are sent to {{site.data.keyword.at_full_notm}} hosted event search
{: #at-legacy-locations}



{{site.data.keyword.cis_short_notm}} sends activity tracking events to {{site.data.keyword.at_full_notm}} hosted event search in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #at-table-1}
{: tab-title="Americas"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #at-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #at-table-3}
{: tab-title="Europe"}
{: tab-group="at"}
{: class="simple-tab-table"}
{: row-headers}

## Locations where activity tracking events are sent by {{site.data.keyword.atracker_full_notm}}
{: #atracker-locations}



{{site.data.keyword.cis_short_notm}} sends activity tracking events by {{site.data.keyword.atracker_full_notm}} in the regions that are indicated in the following table.

| Dallas (`us-south`) | Washington (`us-east`)  | Toronto (`ca-tor`) | Sao Paulo (`br-sao`) |
|---------------------|-------------------------|-------------------|----------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Americas locations" caption-side="top"}
{: #atracker-table-1}
{: tab-title="Americas"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Tokyo (`jp-tok`)    | Sydney (`au-syd`) |  Osaka (`jp-osa`) | Chennai (`in-che`) |
|---------------------|------------------|------------------|--------------------|
| [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Asia Pacific locations" caption-side="top"}
{: #atracker-table-2}
{: tab-title="Asia Pacific"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}

| Frankfurt (`eu-de`)  | London (`eu-gb`) | Madrid (`eu-es`) |
|---------------------------------------------------------------|---------------------|------------------|
| [Yes]{: tag-green} | [No]{: tag-red} | [No]{: tag-red} |
{: caption="Regions where activity tracking events are sent in Europe locations" caption-side="top"}
{: #atracker-table-3}
{: tab-title="Europe"}
{: tab-group="atracker"}
{: class="simple-tab-table"}
{: row-headers}




## Viewing activity tracking events for {{site.data.keyword.cis_short_notm}}
{: #at-viewing}



You can use {{site.data.keyword.logs_full_notm}} to visualize and alert on events that are generated in your account and routed by {{site.data.keyword.atracker_full_notm}} to an {{site.data.keyword.logs_full_notm}} instance.

### Launching {{site.data.keyword.logs_full_notm}} from the Observability page
{: #at-log-launch-standalone}



For information on launching the {{site.data.keyword.logs_full_notm}} UI, see [Launching the UI in the {{site.data.keyword.logs_full_notm}} documentation.](/docs/cloud-logs?topic=cloud-logs-instance-launch)

## Events for DNS domains
{: #at_actions_dns-domains}

|Action|Description|
|-|-|
|`internet-svcs.zones.create`|Create a DNS domain.|
|`internet-svcs.zones.update`|Update a DNS domain.|
|`internet-svcs.zones.delete`|Delete a DNS domain.|
|`internet-svcs.zones-activation-check.update`|Run activation check for a DNS domain.|
|`internet-svcs.dnssec.update`|Enable or disable DNSSEC for a DNS domain.|
{: caption="Actions that generate DNS domain events" caption-side="bottom"}

## Events for DNS records
{: #at_actions_dns-records}

The following table lists the actions that are related to DNS records and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.dns-records.create`|Create a DNS record.|
|`internet-svcs.dns-records.update`|Update a DNS record.|
|`internet-svcs.dns-records.delete`|Delete a DNS record.|
|`internet-svcs.dns-records-bulk.create`|Import DNS records from zone file.|
{: caption="Actions that generate DNS record events" caption-side="bottom"}

## Events for load balancers
{: #at_actions_load-balancers}

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
{: caption="Actions that generate load balancer events" caption-side="bottom"}

## Events for purging the cache
{: #at_actions_purge-cache}

The following table lists the actions that are related to purging the cache and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.purge-cache-all.update`|Purge all cached assets of a domain from edge server.|
|`internet-svcs.purge-cache-by-urls.update`|Purge cached assets by URLs from edge server.|
|`internet-svcs.purge-cache-by-cache-tags.update`|Purge cached assets by cache tags from edge server.|
|`internet-svcs.purge-cache-by-hosts.update`|Purge cached assets by hostnames from edge server.|
{: caption="Actions that generate cache purge events" caption-side="bottom"}


## Events for page rules
{: #at_actions_page-rules}

The following table lists the actions that are related to page rules and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.pagerules.create`|Create a page rule.|
|`internet-svcs.pagerules.update`|Update a page rule.|
|`internet-svcs.pagerules.delete`|Delete a page rule.|
{: caption="Actions that generate page rule events" caption-side="bottom"}

## Events for firewalls
{: #at_actions_firewalls}

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
{: caption="Actions that generate firewall events" caption-side="bottom"}

## Events for rate limiting
{: #at_actions_rate-limiting}

The following table lists the actions that are related to rate limiting and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.rate-limits.create`|Create a rate limiting rule.|
|`internet-svcs.rate-limits.update`|Update a rate limiting rule.|
|`internet-svcs.rate-limits.delete`|Delete a rate limiting rule.|
{: caption="Actions that generate a rate limiting events" caption-side="bottom"}

## Events for routing
{: #at_actions_routing}

The following table lists the actions that are related to routing and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.smart-routing.update`|Enable or disable smart routing.|
|`internet-svcs.tiered-caching.update`|Enable or disable tiered caching.|
{: caption="Actions that generate routing events" caption-side="bottom"}

## Events for certificate packs
{: #at_actions_certificate-packs}

The following table lists the actions that are related to certificate packs and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.certificate-packs.create`|Order a dedicated wildcard or custom certificate.|
|`internet-svcs.certificate-packs.delete`|Delete a dedicated wildcard or custom certificate.|
{: caption="Actions that generate certificate pack events" caption-side="bottom"}

## Events for custom certificates
{: #at_actions_custom-certificates}

The following table lists the actions that are related to custom certificates and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.custom-certificates.create`|Upload a custom certificate.|
|`internet-svcs.custom-certificates.update`|Update a custom certificate.|
|`internet-svcs.custom-certificates.delete`|Delete a custom certificate.|
{: caption="Actions that generate custom certificate events" caption-side="bottom"}

## Events for origin certificates
{: #at_actions_origin-certificates}

The following table lists the actions that are related to origin certificates and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.origin-certificates.create`|Create an origin certificate.|
|`internet-svcs.origin-certificates.delete`|Revoke an origin certificate.|
{: caption="Actions that generate origin certificate events" caption-side="bottom"}

## Events for edge functions
{: #at_actions_edge-functions}

The following table lists the actions that are related to edge functions and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.edge-functions-scripts.create`|Create an edge functions script.|
|`internet-svcs.edge-functions-scripts.update`|Update a new version of edge functions script.|
|`internet-svcs.edge-functions-scripts.delete`|Delete an edge functions script.|
|`internet-svcs.edge-functions-routes.create`|Create an edge functions route.|
|`internet-svcs.edge-functions-routes.update`|Update an edge functions route.|
|`internet-svcs.edge-functions-routes.delete`|Delete an edge functions route.|
{: caption="Actions that generate edge functions events" caption-side="bottom"}

## Events for range applications
{: #at_actions_range-applications}

The following table lists the actions that are related to range applications and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.range-apps.create`|Create a range application.|
|`internet-svcs.range-apps.update`|Update a range application.|
|`internet-svcs.range-apps.delete`|Delete a range application.|
{: caption="Actions that generate range events" caption-side="bottom"}

## Events for Logpush
{: #at_actions_logpush}

The following table lists the actions that are related to Logpush and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.logpush-ownership.create`|Initiate Logpush ownership challenge.|
|`internet-svcs.logpush-ownership-validate.create`|Validate Logpush ownership challenge.|
|`internet-svcs.logpush-jobs.create`|Create a Logpush job.|
|`internet-svcs.logpush-jobs.update`|Update a Logpush job.|
|`internet-svcs.logpush-jobs.delete`|Delete a Logpush job.|
{: caption="Actions that generate logpush events" caption-side="bottom"}

## Events for custom error pages
{: #at_actions_custom-error-pages}

The following table lists the actions that are related to custom error pages and generate an event:

|Action|Description|
|-|-|
|`internet-svcs.custom-pages.create`|Create a custom error page.|
|`internet-svcs.custom-pages.update`|Update a custom error page.|
{: caption="Actions that generate custom error page events" caption-side="bottom"}

## Events for settings
{: #at_actions_settings}

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
{: caption="Actions that generate settings events" caption-side="bottom"}

## Additional information
{: #info}

When you monitor {{site.data.keyword.at_full_notm}} events that are generated by the {{site.data.keyword.cis_full_notm}}, and you identify an API request for which you need additional information, check the `requestData` field in the event.

Open a Support case and include the value of the field **requestId** that is available in `requestData`.

## Analyzing {{site.data.keyword.cis_short_notm}} activity tracking events
{: #at_events_iam_analyze}

For more information about calling auditing events with the API, see the Auditing section of each method in the [{{site.data.keyword.cis_short_notm}} API documentation](/apidocs/cis).
