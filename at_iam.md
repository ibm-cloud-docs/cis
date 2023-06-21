---

copyright:
  years: 2020
lastupdated: "2020-09-29"

keywords: IBM Cloud, observability

subcollection: observability

---

{{site.data.keyword.attribute-definition-list}}

# IAM and Activity Tracker actions by API
{: #at_iam_CIS}

List of IAM actions and Activity Tracker actions by API method.
{: shortdesc}



## Overview
{: #at_iam_CIS_overview}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get overview | `GET /v2/{crn}/zones/{domain_id}/overview` | `internet-svcs.zones.read` | `internet-svcs.overview.read` |
{: caption="Table 1. Overview" caption-side="bottom"} 



## DNS Domains
{: #at_iam_CIS_domains}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| List domains or get domain details | `GET /v1/{crn}/zones` | `internet-svcs.zones.read` | `internet-svcs.zones.read` |
| Create a domain | `POST /v1/{crn}/zones` | `internet-svcs.zones.manage` | `internet-svcs.zones.create` |
| Update a domain | `PATCH /v1/{crn}/zones/{domain_id}` | `internet-svcs.reliability.update` | `internet-svcs.zones.update` |
| Delete a domain | `DELETE /v1/{crn}/zones/{domain_id}` | `internet-svcs.reliability.manage` | `internet-svcs.zones.delete` |
| Perform activation check on a domain | `PUT /v1/{crn}/zones/{domain_id}/activation_check` | `internet-svcs.reliability.update` | `internet-svcs.zones-activation-check.update` |
| Get DNSSEC configuration | `GET /v1/{crn}/zones/{domain_id}/dnssec` | `internet-svcs.reliability.read` | `internet-svcs.dnssec.read` |
| Enable / Disable DNSSEC | `PATCH /v1/{crn}/zones/{domain_id}/dnssec` | `internet-svcs.reliability.update` | `internet-svcs.dnssec.update` |
{: caption="Table 2. DNS Domains" caption-side="bottom"} 


## DNS Records
{: #at_iam_CIS_records}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get DNS records | `GET /v1/{crn}/zones/{domain_id}/dns_records` | `internet-svcs.reliability.read` | `internet-svcs.dns-records.read` |
| Create a DNS record | `POST /v1/{crn}/zones/{domain_id}/dns_records` | `internet-svcs.reliability.manage` | `internet-svcs.dns-records.create` |
| Update a DNS record | `PUT /v1/{crn}/zones/{domain_id}/dns_records/{record_id}` | `internet-svcs.reliability.update` | `internet-svcs.dns-records.update` |
| Delete a DNS record | `DELETE /v1/{crn}/zones/{domain_id}/dns_records/{record_id}` | `internet-svcs.reliability.manage` | `internet-svcs.dns-records.delete` |
| Import DNS records from zone file | `GET /v1/{crn}/zones/{domain_id}/dns_records_bulk` | `internet-svcs.reliability.read` | `internet-svcs.dns-records-bulk.read` |
| Export DNS records to a zone file | `POST /v1/{crn}/zones/{domain_id}/dns_records_bulk` | `internet-svcs.reliability.manage` | `internet-svcs.dns-records-bulk.create` |
{: caption="Table 3. DNS Records" caption-side="bottom"} 



## GLB
{: #at_iam_CIS_GLB}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get global load balancers | `GET /v1/{crn}/zones/{domain_id}/load_balancers` | `internet-svcs.reliability.read` | `internet-svcs.load-balancers.read` |
| Create a global load balancer | `POST /v1/{crn}/zones/{domain_id}/load_balancers` | `internet-svcs.reliability.manage` | `internet-svcs.load-balancers.create` |
| Update a global load balancer | `PUT /v1/{crn}/zones/{domain_id}/load_balancers/{glb_id}` | `internet-svcs.reliability.update` | `internet-svcs.load-balancers.update` |
| Delete a global load balancer | `DELETE /v1/{crn}/zones/{domain_id}/load_balancers/{glb_id}` | `internet-svcs.reliability.manage` | `internet-svcs.load-balancers.delete` |
| Get health monitors | `GET /v1/{crn}/load_balancers/monitors` | `internet-svcs.zones.read` | `internet-svcs.load-balancer-monitors.read` |
| Create a health monitor | `POST /v1/{crn}/load_balancers/monitors` | `internet-svcs.zones.manage` | `internet-svcs.load-balancer-monitors.create` |
| Update a health monitor | `PUT /v1/{crn}/load_balancers/monitors/{monitor_id}` | `internet-svcs.zones.update` | `internet-svcs.load-balancer-monitors.update` |
| Delete a health monitor | `DELETE /v1/{crn}/load_balancers/monitors/{monitor_id}` | `internet-svcs.zones.manage` | `internet-svcs.load-balancer-monitors.delete` |
| Get load balancer pools | `GET /v1/{crn}/load_balancers/pools` | `internet-svcs.zones.read` | `internet-svcs.load-balancer-pools.read` |
| Create a load balancer pool | `POST /v1/{crn}/load_balancers/pools` | `internet-svcs.zones.manage` | `internet-svcs.load-balancer-pools.create` |
| Update a load balancer pool | `PUT /v1/{crn}/load_balancers/pools/{pool_id}` | `internet-svcs.zones.update` | `internet-svcs.load-balancer-pools.update` |
| Delete a load balancer pool | `DELETE /v1/{crn}/load_balancers/pools/{pool_id}` | `internet-svcs.zones.manage` | `internet-svcs.load-balancer-pools.delete` |
| Get load balancer events | `GET /v1/{crn}/load_balancers/events` | `internet-svcs.zones.read` | `internet-svcs.load-balancer-events.read` |
{: caption="Table 4. GLB" caption-side="bottom"} 


## Metrics
{: #at_iam_CIS_Metrics}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get dashboard analytics | `GET /v1/{crn}/zones/{domain_id}/analytics/dashboard` | `internet-svcs.reliability.read` | `internet-svcs.dashboard-analytics.read` |
| Get HTTP requests analytics | `GET /v1/{crn}/zones/{domain_id}/analytics/http_requests` | `internet-svcs.reliability.read` | `internet-svcs.http-requests-analytics.read` |
| Get HTTP requests analytics by colocations | `GET /v1/{crn}/zones/{domain_id}/analytics/colos` | `internet-svcs.reliability.read` | `internet-svcs.colos-analytics.read` |
| Get DNS analytics | `GET /v1/{crn}/zones/{domain_id}/dns_analytics/report` | `internet-svcs.reliability.read` | `internet-svcs.dns-analytics.read` |
{: caption="Table 5. Metrics" caption-side="bottom"} 



## WAF
{: #at_iam_CIS_WAF}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get WAF packages | `GET /v1/{crn}/zones/{domain_id}/firewall/waf/packages` | `internet-svcs.security.read` | `internet-svcs.waf-packages.read` |
| Change the sensitivity and action mode of a WAF package | `PATCH /v1/{crn}/zones/{domain_id}/firewall/waf/packages/{package_id}` | `internet-svcs.security.update` | `internet-svcs.waf-packages.update` |
| Get WAF groups | `GET /v1/{crn}/zones/{domain_id}/firewall/waf/packages/{package_id}/groups` | `internet-svcs.security.read` | `internet-svcs.waf-groups.read` |
| Enable / disable a WAF group | `PATCH /v1/{crn}/zones/{domain_id}/firewall/waf/packages/{package_id}/groups/{group_id}` | `internet-svcs.security.update` | `internet-svcs.waf-groups.update` |
| Get WAF rules | `GET /v1/{crn}/zones/{domain_id}/firewall/waf/packages/{package_id}/rules` | `internet-svcs.security.read` | `internet-svcs.waf-rules.read` |
| Change the action mode of a WAF rule | `PATCH /v1/{crn}/zones/{domain_id}/firewall/waf/packages/{package_id}/rules/{rule_id}` | `internet-svcs.security.update` | `internet-svcs.waf-rules.update` |
{: caption="Table 6. WAF" caption-side="bottom"} 



## IP Firewall
{: #at_iam_CIS_ip}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get IP firewall rules | `GET /v1/{crn}/zones/{domain_id}/firewall/access_rules/rules` | `internet-svcs.security.read` | `internet-svcs.ip-firewall-rules.read` |
| Create an IP firewall rule | `POST /v1/{crn}/zones/{domain_id}/firewall/access_rules/rules` | `internet-svcs.security.manage` | `internet-svcs.ip-firewall-rules.create` |
| Update an IP firewall rule | `PATCH /v1/{crn}/zones/{domain_id}/firewall/access_rules/rules/{rule_id}` | `internet-svcs.security.update` | `internet-svcs.ip-firewall-rules.update` |
| Delete an IP firewall rule | `DELETE /v1/{crn}/zones/{domain_id}/firewall/access_rules/rules/{rule_id}` | `internet-svcs.security.manage` | `internet-svcs.ip-firewall-rules.delete` |
| Get user-agent blocking rules | `GET /v1/{crn}/zones/{domain_id}/firewall/ua_rules` | `internet-svcs.security.read` | `internet-svcs.ua-rules.read` |
| Create a user-agent blocking rule | `POST /v1/{crn}/zones/{domain_id}/firewall/ua_rules` | `internet-svcs.security.manage` | `internet-svcs.ua-rules.create` |
| Update a user-agent blocking rule | `PUT /v1/{crn}/zones/{domain_id}/firewall/ua_rules/{rule_id}` | `internet-svcs.security.update` | `internet-svcs.ua-rules.update` |
| Delete a user-agent blocking rule | `DELETE /v1/{crn}/zones/{domain_id}/firewall/ua_rules/{rule_id}` | `internet-svcs.security.manage` | `internet-svcs.ua-rules.delete` |
| Get domain lockdown rules | `GET /v1/{crn}/zones/{domain_id}/firewall/lockdowns` | `internet-svcs.security.read` | `internet-svcs.domain-lockdown-rules.read` |
| Create a domain lockdown rule | `POST /v1/{crn}/zones/{domain_id}/firewall/lockdowns` | `internet-svcs.security.manage` | `internet-svcs.domain-lockdown-rules.create` |
| Update a domain lockdown rule | `PUT /v1/{crn}/zones/{domain_id}/firewall/lockdowns/{rule_id}` | `internet-svcs.security.update` | `internet-svcs.domain-lockdown-rules.update` |
| Delete a domain lockdown rule | `DELETE /v1/{crn}/zones/{domain_id}/firewall/lockdowns/{rule_id}` | `internet-svcs.security.manage` | `internet-svcs.domain-lockdown-rules.delete` |
{: caption="Table 7. IP Firewall" caption-side="bottom"} 

## Firewall Rules
{: #at_iam_CIS_fw}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get firewall rules | `GET /v1/{crn}/zones/{domain_id}/firewall/rules` | `internet-svcs.security.read` | `internet-svcs.firewall-rules.read` |
| Create a firewall rule | `POST /v1/{crn}/zones/{domain_id}/firewall/rules` | `internet-svcs.security.manage` | `internet-svcs.firewall-rules.create` |
| Update a firewall rule | `PATCH /v1/{crn}/zones/{domain_id}/firewall/rules/{rule_id}` | `internet-svcs.security.update` | `internet-svcs.firewall-rules.update` |
| Delete a firewall rule | `DELETE /v1/{crn}/zones/{domain_id}/firewall/rules/{rule_id}` | `internet-svcs.security.manage` | `internet-svcs.firewall-rules.delete` |
| Get filters | `GET /v1/{crn}/zones/{domain_id}/filters` | `internet-svcs.security.read` | `internet-svcs.filters.read` |
| Create a filter | `POST /v1/{crn}/zones/{domain_id}/filters` | `internet-svcs.security.manage` | `internet-svcs.filters.create` |
| Update a filter | `PATCH /v1/{crn}/zones/{domain_id}/filters/{filter_id}` | `internet-svcs.security.update` | `internet-svcs.filters.update` |
| Delete a filter | `DELETE /v1/{crn}/zones/{domain_id}/filters/{filter_id}` | `internet-svcs.security.manage` | `internet-svcs.filters.delete` |
| Validate the expression of a filter. | `POST /v1/{crn}/zones/{domain_id}/filters/validate-expr` | `internet-svcs.security.manage` | `internet-svcs.filters-validate-expr.create` |
{: caption="Table 8. Firewall Rules" caption-side="bottom"} 


## Security Events
{: #at_iam_CIS_secevents}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get security events | `GET /v1/{crn}/zones/{domain_id}/security/events` | `internet-svcs.security.read` | `internet-svcs.security-events.read` |
| Get firewall events (Deprecated) | `GET /v1/{crn}/zones/{domain_id}/analytics/firewall_events  [DEPRECATED]` | `internet-svcs.security.read` | `internet-svcs.firewall-events-analytics.read` |
{: caption="Table 9. Security Events" caption-side="bottom"} 


## Rate Limiting
{: #at_iam_CIS_rate}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get rate limiting rules | `GET /v1/{crn}/zones/{domain_id}/rate_limits` | `internet-svcs.security.read` | `internet-svcs.rate-limits.read` |
| Create a rate limiting rule | `POST /v1/{crn}/zones/{domain_id}/rate_limits` | `internet-svcs.security.manage` | `internet-svcs.rate-limits.create` |
| Update a rate limiting rule | `PUT /v1/{crn}/zones/{domain_id}/rate_limits/{ratelimit_id}` | `internet-svcs.security.update` | `internet-svcs.rate-limits.update` |
| Delete a rate limiting rule | `DELETE /v1/{crn}/zones/{domain_id}/rate_limits/{ratelimit_id}` | `internet-svcs.security.manage` | `internet-svcs.rate-limits.delete` |
| Get rate limiting analytics | `GET /v1/{crn}/zones/{domain_id}/rate_limit_analytics` | `internet-svcs.security.read` | `internet-svcs.rate-limit-analytics.read` |
{: caption="Table 10. Rate Limiting" caption-side="bottom"} 


## Caching
{: #at_iam_CIS_Caching}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Purge all cached assets of a domain from edge server | `PUT /v1/{crn}/zones/{domain_id}/purge_cache/purge_all` | `internet-svcs.performance.update` | `internet-svcs.purge-cache-all.update` |
| Purge cached assets by URLs from edge server | `PUT /v1/{crn}/zones/{domain_id}/purge_cache/purge_by_urls` | `internet-svcs.performance.update` | `internet-svcs.purge-cache-by-urls.update` |
| Purge cached assets by cache tags from edge server | `PUT /v1/{crn}/zones/{domain_id}/purge_cache/purge_by_cache_tags` | `internet-svcs.performance.update` | `internet-svcs.purge-cache-by-cache-tags.update` |
| Purge cached assets by hostnames from edge server | `PUT /v1/{crn}/zones/{domain_id}/purge_cache/purge_by_hosts` | `internet-svcs.performance.update` | `internet-svcs.purge-cache-by-hosts.update` |
{: caption="Table 11. Caching" caption-side="bottom"} 


## Routing
{: #at_iam_CIS_Routing}


| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get smart routing configurations | `GET /v1/{crn}/zones/{domain_id}/routing/smart_routing` | `internet-svcs.performance.read` | `internet-svcs.smart-routing.read` |
| Enable / disable smart routing | `PATCH /v1/{crn}/zones/{domain_id}/routing/smart_routing` | `internet-svcs.performance.update` | `internet-svcs.smart-routing.update` |
| Get tiered caching configurations | `GET /v1/{crn}/zones/{domain_id}/routing/tiered_caching` | `internet-svcs.performance.read` | `internet-svcs.tiered-caching.read` |
| Enable / disable tiered caching | `PATCH /v1/{crn}/zones/{domain_id}/routing/tiered_caching` | `internet-svcs.performance.update` | `internet-svcs.tiered-caching.update` |
{: caption="Table 12. Routing" caption-side="bottom"} 


## Page Rules
{: #at_iam_CIS_pagerules}


| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get page rules | `GET /v1/{crn}/zones/{domain_id}/pagerules` | `internet-svcs.performance.read` | `internet-svcs.pagerules.read` |
| Create a page rule | `POST /v1/{crn}/zones/{domain_id}/pagerules` | `internet-svcs.performance.manage` | `internet-svcs.pagerules.create` |
| Update a page rule | `PUT /v1/{crn}/zones/{domain_id}/pagerules/{rule_id}` | `internet-svcs.performance.update` | `internet-svcs.pagerules.update` |
| Delete a page rule | `DELETE /v1/{crn}/zones/{domain_id}/pagerules/{rule_id}` | `internet-svcs.performance.manage` | `internet-svcs.pagerules.delete` |
{: caption="Table 13. Page Rules" caption-side="bottom"} 



## TLS
{: #at_iam_CIS_TLS}


| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get universal SSL setting | `GET /v1/{crn}/zones/{domain_id}/ssl/universal/settings` | `internet-svcs.security.read` | `internet-svcs.universal-ssl-setting.read` |
| Update universal SSL setting | `PATCH /v1/{crn}/zones/{domain_id}/ssl/universal/settings` | `internet-svcs.security.update` | `internet-svcs.universal-ssl-setting.update` |
| Get edge certificates ordered from CIS | `GET /v1/{crn}/zones/{domain_id}/ssl/certificate_packs` | `internet-svcs.security.read` | `internet-svcs.certificate-packs.read` |
| Order an edge certificate | `POST /v1/{crn}/zones/{domain_id}/ssl/certificate_packs` | `internet-svcs.security.manage` | `internet-svcs.certificate-packs.create` |
| Delete an edge certificate | `DELETE /v1/{crn}/zones/{domain_id}/ssl/certificate_packs/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.certificate-packs.delete` |
| Get uploaded certificates | `GET /v1/{crn}/zones/{domain_id}/custom_certificates` | `internet-svcs.security.read` | `internet-svcs.custom-certificates.read` |
| Upload a certificate to CIS edge | `POST /v1/{crn}/zones/{domain_id}/custom_certificates` | `internet-svcs.security.manage` | `internet-svcs.custom-certificates.create` |
| Update the certificate uploaded to CIS edge | `PATCH /v1/{crn}/zones/{domain_id}/custom_certificates/{cert_id}` | `internet-svcs.security.update` | `internet-svcs.custom-certificates.update` |
| Delete a certificate uploaded to CIS edge | `DELETE /v1/{crn}/zones/{domain_id}/custom_certificates/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.custom-certificates.delete` |
| Get origin certificate issued by CIS | `GET /v1/{crn}/zones/{domain_id}/origin_certificates` | `internet-svcs.security.read` | `internet-svcs.origin-certificates.read` |
| Create an origin certificate issued by CIS | `POST /v1/{crn}/zones/{domain_id}/origin_certificates` | `internet-svcs.security.manage` | `internet-svcs.origin-certificates.create` |
| Revoke an origin certificate issued by CIS | `DELETE /v1/{crn}/zones/{domain_id}/origin_certificates/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.origin-certificates.delete` |
{: caption="Table 14. TLS" caption-side="bottom"} 



## Edge Functions
{: #at_iam_edge-func}


| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get edge function scripts | `GET /v1/{crn}/workers/scripts` | `internet-svcs.performance.read` | `internet-svcs.edge-functions-scripts.read` |
| Create edge function script | `POST /v1/{crn}/workers/scripts` | `internet-svcs.performance.manage` | `internet-svcs.edge-functions-scripts.create` |
| Update edge function script | `PUT /v1/{crn}/workers/scripts/{script_name}` | `internet-svcs.performance.update` | `internet-svcs.edge-functions-scripts.update` |
| Delete edge function script | `DELETE /v1/{crn}/workers/scripts/{script_name}` | `internet-svcs.performance.manage` | `internet-svcs.edge-functions-scripts.delete` |
| Get edge function routes | `GET /v1/{crn}/zones/{domain_id}/workers/routes` | `internet-svcs.performance.read` | `internet-svcs.edge-functions-routes.read` |
| Create edge function route | `POST /v1/{crn}/zones/{domain_id}/workers/routes` | `internet-svcs.performance.manage` | `internet-svcs.edge-functions-routes.create` |
| Update edge function route | `PUT /v1/{crn}/zones/{domain_id}/workers/routes/{route_id}` | `internet-svcs.performance.update` | `internet-svcs.edge-functions-routes.update` |
| Delete edge function route | `DELETE /v1/{crn}/zones/{domain_id}/workers/routes/{route_id}` | `internet-svcs.performance.manage` | `internet-svcs.edge-functions-routes.delete` |
{: caption="Table 15. Edge Functions" caption-side="bottom"} 

## Range
{: #at_iam_range}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get range apps | `GET /v1/{crn}/zones/{domain_id}/range/apps` | `internet-svcs.security.read` | `internet-svcs.range-apps.read` |
| Create a range app | `POST /v1/{crn}/zones/{domain_id}/range/apps` | `internet-svcs.security.manage` | `internet-svcs.range-apps.create` |
| Update a range app | `PUT /v1/{crn}/zones/{domain_id}/range/apps/{app_id}` | `internet-svcs.security.update` | `internet-svcs.range-apps.update` |
| Delete a range app | `DELETE /v1/{crn}/zones/{domain_id}/range/apps/{app_id}` | `internet-svcs.security.manage` | `internet-svcs.range-apps.delete` |
| Get analytics of range apps | `GET /v1/{crn}/zones/{domain_id}/range/analytics/events/summary` </br>`GET /v1/{crn}/zones/{domain_id}/range/analytics/events/bytime` | `internet-svcs.security.read` |`internet-svcs.range-analytics.read` |
{: caption="Table 16. Range" caption-side="bottom"} 



## Logpush
{: #at_iam_Logpush}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get logpush fields | `GET /v1/{crn}/zones/{domain_id}/logpush/datasets/{dataset}/fields` | `internet-svcs.zones.read` | `internet-svcs.logpush-fields.read` |
| Get logpush jobs | `GET /v1/{crn}/zones/{domain_id}/logpush/jobs`| `internet-svcs.zones.read` | `internet-svcs.logpush-jobs.read` |
| Create a logpush job | `POST /v1/{crn}/zones/{domain_id}/logpush/jobs` | `internet-svcs.zones.manage` | `internet-svcs.logpush-jobs.create` |
| Update a logpush job | `PUT /v1/{crn}/zones/{domain_id}/logpush/jobs/{job_id}` | `internet-svcs.zones.update` | `internet-svcs.logpush-jobs.update` |
| Delete a logpush job | `DELETE /v1/{crn}/zones/{domain_id}/logpush/jobs/{job_id}` | `internet-svcs.zones.manage` | `internet-svcs.logpush-jobs.delete` |
| Initiate the logpush ownership challenge | `POST /v1/{crn}/zones/{domain_id}/logpush/ownership` | `internet-svcs.zones.manage` | `internet-svcs.logpush-ownership.create` |
| Validate the logpush ownership challenge token | `POST /v1/{crn}/zones/{domain_id}/logpush/ownership/validate` | `internet-svcs.zones.manage` | `internet-svcs.logpush-ownership-validate.create` |
{: caption="Table 17. Logpush" caption-side="bottom"} 




## Custom Pages
{: #at_iam_edge-Custom-Pages}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get custom error pages | `GET /v1/{crn}/zones/{domain_id}/custom_pages` | `internet-svcs.zones.read` | `internet-svcs.custom-pages.read` |
| Update custom error page | `PUT /v1/{crn}/zones/{domain_id}/custom_pages/{page_id}` | `internet-svcs.zones.update` | `internet-svcs.custom-pages.update` |
{: caption="Table 18. Custom Pages" caption-side="bottom"} 




## Mutual TLS
{: #at_iam_tls}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get certificates uploaded for mTLS | `GET /v1/{crn}/zones/{domain_id}/access/certificates` | `internet-svcs.security.read` | `internet-svcs.access-certificates.read` |
| Upload a certificate for mTLS | `POST /v1/{crn}/zones/{domain_id}/access/certificates` | `internet-svcs.security.manage` | `internet-svcs.access-certificates.create` |
| Update a certificate for mTLS | `PUT /v1/{crn}/zones/{domain_id}/access/certificates/{cert_id}` | `internet-svcs.security.update` | `internet-svcs.access-certificates.update` |
| Delete a certificate for mTLS | `DELETE /v1/{crn}/zones/{domain_id}/access/certificates/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.access-certificates.delete` |
| Get mTLS applications | `GET /v1/{crn}/zones/{domain_id}/access/apps` | `internet-svcs.security.read` | `internet-svcs.access-apps.read` |
| Create a mTLS application | `POST /v1/{crn}/zones/{domain_id}/access/apps` | `internet-svcs.security.manage` | `internet-svcs.access-apps.create` |
| Update a mTLS application | `PUT /v1/{crn}/zones/{domain_id}/access/apps/{app_id}` | `internet-svcs.security.update` | `internet-svcs.access-apps.update` |
| Delete a mTLS application | `DELETE /v1/{crn}/zones/{domain_id}/access/apps/{app_id}` | `internet-svcs.security.manage` | `internet-svcs.access-apps.delete` |
| Get mTLS policies | `GET /v1/{crn}/zones/{domain_id}/access/apps/{app_id}/policies` | `internet-svcs.security.read` | `internet-svcs.access-policies.read` |
| Create a mTLS policy | `POST /v1/{crn}/zones/{domain_id}/access/apps/{app_id}/policies` | `internet-svcs.security.manage` | `internet-svcs.access-policies.create` |
| Update a mTLS policy | `PUT /v1/{crn}/zones/{domain_id}/access/apps/{app_id}/policies/{policy_id}` | `internet-svcs.security.update` | `internet-svcs.access-policies.update` |
| Delete a mTLS policy | `DELETE /v1/{crn}/zones/{domain_id}/access/apps/{app_id}` | `internet-svcs.security.manage` | `internet-svcs.access-policies.delete` |
{: caption="Table 19. Mutual TLS" caption-side="bottom"} 



## Origin TLS Client Authentication
{: #at_iam_tls-client-auth}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
|List certificates used for origin TLS client authentication at domain level. | `GET /v1/{crn}/zones/{domain_id}/origin_tls_client_auth`|`internet-svcs.security.read`|`internet-svcs.origin-tls-client-auth.read`|
|Create a certificate used for origin TLS client authentication at domain level.| `POST /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.origin-tls-client-auth.create` |
|Delete a certificate used for origin TLS client authentication used at domain level.| `DELETE /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.origin-tls-client-auth.delete` |
|Get origin TLS client authentication settings used at domain level.| `GET /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/settings|internet-svcs.security.read|internet-svcs.origin-tls-client-auth-settings.read` |
|Update origin TLS client authentication settings used at domain level.| `PUT /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/settings` | `internet-svcs.security.update` | `internet-svcs.origin-tls-client-auth-settings.update` |
|Get origin TLS client authentication settings used for the hostname.| `GET /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/hostnames/{hostname}` | `internet-svcs.security.read` | `internet-svcs.origin-tls-client-auth-hostnames.read`|
|Update origin TLS client authentication settings for a hostname.| `PUT /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/hostnames` | `internet-svcs.security.update` | `internet-svcs.origin-tls-client-auth-hostnames.update`|
|Get origin TLS client authentication certificates used at hostname level.| `GET /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/hostnames/certificates/{cert_id}` | `internet-svcs.security.read` | `internet-svcs.origin-tls-client-auth-hostname-certificates.read` |
|Create origin TLS client authentication certificate used at hostname level.| `POST /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/hostnames/certificates` | `internet-svcs.security.manage` | `internet-svcs.origin-tls-client-auth-hostname-certificates.create` |
|Delete an origin TLS client authentication certificate used at hostname level.| `DELETE /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/hostnames/certificates/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.origin-tls-client-auth-hostname-certificates.delete` |
{: caption="Table 20. Edge Functions" caption-side="bottom"} 

## Domain settings
{: #at_iam_CIS_domain-settings}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
| Get CNAME flattening settings. | `GET /v1/{crn}/zones/{domain_id}/setting/cname_flattening` | `internet-svcs.reliability.read` | `internet-svcs.cname-flattening-setting.read` |
|Update CNAME flattening settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/cname_flattening` | `internet-svcs.reliability.update` | `internet-svcs.cname-flattening-setting.update`|
|Get cache level settings. | `GET /v1/{crn}/zones/{domain_id}/setting/cache_level` | `internet-svcs.performance.read` | `internet-svcs.cache-level-setting.read`|
|Update cache level settings. | `PUT /v1/{crn}/zones/{domain_id}/setting/cache_level` | `internet-svcs.performance.update` | `internet-svcs.cache-level-setting.update` |
|Get browser cache TTL settings. | `GET /v1/{crn}/zones/{domain_id}/setting/browser_cache_ttl` | `internet-svcs.performance.read` | `internet-svcs.browser-cache-ttl-setting.read` |
|Update browser cache TTL settings. | `PUT /v1/{crn}/zones/{domain_id}/setting/browser_cache_ttl` | `internet-svcs.performance.update` | `internet-svcs.browser-cache-ttl-setting.update` |
|Get always online (serve stale content) settings. | `GET /v1/{crn}/zones/{domain_id}/setting/always_online` | `internet-svcs.performance.read` | `internet-svcs.always-online-setting.read` |
|Update always online (serve stale content) settings. | `PUT /v1/{crn}/zones/{domain_id}/setting/always_online` | `internet-svcs.performance.update` | `internet-svcs.always-online-setting.update` |
|Get development mode settings. | `GET /v1/{crn}/zones/{domain_id}/setting/development_mode` | `internet-svcs.performance.read` | `internet-svcs.development-mode-setting.read` |
|Update development mode settings. | `PUT /v1/{crn}/zones/{domain_id}/setting/development_mode` | `internet-svcs.performance.update` | `internet-svcs.development-mode-setting.update` |
|Get sort query string for cache settings. | `GET /v1/{crn}/zones/{domain_id}/setting/sort_query_string_for_cache` | `internet-svcs.performance.read` | `internet-svcs.sort-query-string-for-cache-setting.read` |
|Update sort query string for cache settings. | `PUT /v1/{crn}/zones/{domain_id}/setting/sort_query_string_for_cache` | `internet-svcs.performance.update` | `internet-svcs.sort-query-string-for-cache-setting.update` |
|Get SSL settings. | `GET /v1/{crn}/zones/{domain_id}/setting/ssl` | `internet-svcs.security.read` | `internet-svcs.ssl-setting.read` |
|Update SSL settings. | `PUT /v1/{crn}/zones/{domain_id}/setting/ssl` | `internet-svcs.security.update` | `internet-svcs.ssl-setting.update` |
|Get security level settings. | `GET /v1/{crn}/zones/{domain_id}/setting/security_level` | `internet-svcs.security.read` | `internet-svcs.security-level-setting.read` |
|Update security level settings. | `PUT /v1/{crn}/zones/{domain_id}/setting/security_level` | `internet-svcs.security.update` | `internet-svcs.security-level-setting.update` |
|Get TLS 1.2 settings. | `GET /v1/{crn}/zones/{domain_id}/setting/tls_1_2_only` | `internet-svcs.security.read` | `internet-svcs.tls-1-2-only-setting.read` |
|Update TLS 1.2 settings. | `PUT /v1/{crn}/zones/{domain_id}/setting/tls_1_2_only` | `internet-svcs.security.update` | `internet-svcs.tls-1-2-only-setting.update` |
|Get TLS 1.3 only settings. | `GET /v1/{crn}/zones/{domain_id}/setting/tls_1_3` | `internet-svcs.security.read` | `internet-svcs.tls-1-3-setting.read` |
|Update TLS 1.3 only settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/tls_1_3` | `internet-svcs.security.update` | `internet-svcs.tls-1-3-setting.update`|
|Get automatic HTTPS rewrites settings. | `GET /v1/{crn}/zones/{domain_id}/setting/automatic_https_rewrites` | `internet-svcs.security.read` | `internet-svcs.automatic-https-rewrites-setting.read`|
|Update automatic HTTPS rewrites settings. | `PUT /v1/{crn}/zones/{domain_id}/setting/automatic_https_rewrites` | `internet-svcs.security.update` | `internet-svcs.automatic-https-rewrites-setting.update`|
|Get WAF settings.| `GET /v1/{crn}/zones/{domain_id}/setting/waf` | `internet-svcs.security.read` | `internet-svcs.waf-setting.read`|
|Update WAF settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/waf` | `internet-svcs.security.update` | `internet-svcs.waf-setting.update`|
|Get browser integrity check settings.| `GET /v1/{crn}/zones/{domain_id}/setting/browser_check` | `internet-svcs.security.read` | `internet-svcs.browser-check-setting.read`|
|Update browser integrity check settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/browser_check` | `internet-svcs.security.update` | `internet-svcs.browser-check-setting.update`|
|Get opportunistic encryption settings.| `GET /v1/{crn}/zones/{domain_id}/setting/opportunistic_encryption` | `internet-svcs.security.read` | `internet-svcs.opportunistic-encryption-setting.read`|
|Update opportunistic encryption settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/opportunistic_encryption` | `internet-svcs.security.update` | `internet-svcs.opportunistic-encryption-setting.update`|
|Get challenge TTL settings.| `GET /v1/{crn}/zones/{domain_id}/setting/challenge_ttl` | `internet-svcs.security.read` | `internet-svcs.challenge-ttl-setting.read`|
|Update challenge TTL settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/challenge_ttl` | `internet-svcs.security.update` | `internet-svcs.challenge-ttl-setting.update`|
|Get always use HTTPS settings.| `GET /v1/{crn}/zones/{domain_id}/setting/always_use_https` | `internet-svcs.security.read` | `internet-svcs.always-use-https-setting.read`|
|Update always use HTTPS settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/always_use_https` | `internet-svcs.security.update` | `internet-svcs.always-use-https-setting.update`|
|Get true client IP header settings.| `GET /v1/{crn}/zones/{domain_id}/setting/true_client_ip_header` | `internet-svcs.zones.read` | `internet-svcs.true-client-ip-header-setting.read`|
|Update true client IP header settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/true_client_ip_header` | `internet-svcs.zones.update` | `internet-svcs.true-client-ip-header-setting.update`|
|Get image size optimization settings.| `GET /v1/{crn}/zones/{domain_id}/setting/image_size_optimization` | `internet-svcs.performance.read` | `internet-svcs.image-size-optimization-setting.read`|
|Update image size optimization settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/image_size_optimization` | `internet-svcs.performance.update` | `internet-svcs.image-size-optimization-setting.update`|
|Get script load optimization settings.| `GET /v1/{crn}/zones/{domain_id}/setting/script_load_optimization` | `internet-svcs.performance.read` | `internet-svcs.script-load-optimization-setting.read`|
|Update script load optimization settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/script_load_optimization` | `internet-svcs.performance.update` | `internet-svcs.script-load-optimization-setting.update`|
|Get image load optimization settings.| `GET /v1/{crn}/zones/{domain_id}/setting/image_load_optimization` | `internet-svcs.performance.read` | `internet-svcs.image-load-optimization-setting.read`|
|Update image load optimization settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/image_load_optimization` | `internet-svcs.performance.update` | `internet-svcs.image-load-optimization-setting.update`|
|Get minification settings.| `GET /v1/{crn}/zones/{domain_id}/setting/minify` | `internet-svcs.performance.read` | `internet-svcs.minify-setting.read`|
|Update minification settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/minify` | `internet-svcs.performance.update` | `internet-svcs.minify-setting.update`|
|Get minimum TLS version settings.| `GET /v1/{crn}/zones/{domain_id}/setting/min_tls_version` | `internet-svcs.security.read` | `internet-svcs.min-tls-version-setting.read`|
|Update minimum TLS version settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/min_tls_version` | `internet-svcs.security.update` | `internet-svcs.min-tls-version-setting.update`|
|Get IP geolocation settings.| `GET /v1/{crn}/zones/{domain_id}/setting/ip_geolocation` | `internet-svcs.zones.read` | `internet-svcs.ip-geolocation-setting.read`|
|Update IP geolocation settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/ip_geolocation` | `internet-svcs.zones.update` | `internet-svcs.ip-geolocation-setting.update`|
|Get server side exclude settings.| `GET /v1/{crn}/zones/{domain_id}/setting/server_side_exclude` | `internet-svcs.security.read` | `internet-svcs.server-side-exclude-setting.read`|
|Update server-side exclude settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/server_side_exclude` | `internet-svcs.security.update` | `internet-svcs.server-side-exclude-setting.update`|
|Get security header settings.| `GET /v1/{crn}/zones/{domain_id}/setting/security_header` | `internet-svcs.security.read` | `internet-svcs.security-header-setting.read`|
|Update security header settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/security_header` | `internet-svcs.security.update` | `internet-svcs.security-header-setting.update`|
|Get mobile redirect settings.| `GET /v1/{crn}/zones/{domain_id}/setting/mobile_redirect` | `internet-svcs.performance.read` | `internet-svcs.mobile-redirect-setting.read`|
|Update mobile redirect settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/mobile_redirect` | `internet-svcs.performance.update` | `internet-svcs.mobile-redirect-setting.update`|
|Get prefetch / preload settings.| `GET /v1/{crn}/zones/{domain_id}/setting/prefetch_preload` | `internet-svcs.performance.read` | `internet-svcs.prefetch-preload-setting.read`|
|Update prefetch / preload settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/prefetch_preload` | `internet-svcs.performance.update` | `internet-svcs.prefetch-preload-setting.update`|
|Get HTTP2 settings.| `GET /v1/{crn}/zones/{domain_id}/setting/http2` | `internet-svcs.security.read` | `internet-svcs.http2-setting.read`|
|Update HTTP2 settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/http2` | `internet-svcs.security.update` | `internet-svcs.http2-setting.update`|
|Get IPv6 settings.| `GET /v1/{crn}/zones/{domain_id}/setting/ipv6` | `internet-svcs.zones.read` | `internet-svcs.ipv6-setting.read`|
|Update IPv6 settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/ipv6` | `internet-svcs.zones.update` | `internet-svcs.ipv6-setting.update`|
|Get websocket settings.| `GET /v1/{crn}/zones/{domain_id}/setting/websocket` | `internet-svcs.zones.read` | `internet-svcs.websockets-setting.read`|
|Update websocket settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/websocket` | `internet-svcs.zones.update` | `internet-svcs.websockets-setting.update`|
|Get response buffering settings.| `GET /v1/{crn}/zones/{domain_id}/setting/response_buffering` | `internet-svcs.performance.read` | `internet-svcs.response-buffering-setting.read`|
|Update response buffering settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/response_buffering` | `internet-svcs.performance.update` | `internet-svcs.response-buffering-setting.update`|
|Get hotlink protection settings.| `GET /v1/{crn}/zones/{domain_id}/setting/hotlink_protection` | `internet-svcs.performance.read` | `internet-svcs.hotlink-protection-setting.read`|
|Update hotlink protection settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/hotlink_protection` | `internet-svcs.performance.update` | `internet-svcs.hotlink-protection-setting.update`|
|Get maximum upload size settings.| `GET /v1/{crn}/zones/{domain_id}/setting/max_upload` | `internet-svcs.performance.read` | `internet-svcs.max-upload-setting.read`|
|Update maximum upload size settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/max_upload` | `internet-svcs.performance.update` | `internet-svcs.max-upload-setting.update`|
|Get TLS client authentication settings.| `GET /v1/{crn}/zones/{domain_id}/setting/tls_client_auth` | `internet-svcs.security.read` | `internet-svcs.tls-client-auth-setting.read`|
|Update TLS client authentication settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/tls_client_auth` | `internet-svcs.security.update` | `internet-svcs.tls-client-auth-setting.update`|
|Get pseudo IPv4 settings.| `GET /v1/{crn}/zones/{domain_id}/setting/pseudo_ipv4` | `internet-svcs.zones.read` | `internet-svcs.pseudo-ipv4-setting.read`|
|Update pseudo IPv4 settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/pseudo_ipv4` | `internet-svcs.zones.update` | `internet-svcs.pseudo-ipv4-setting.update`|
|Get origin error page passthrough settings.| `GET /v1/{crn}/zones/{domain_id}/setting/origin_error_page_pass_thru` | `internet-svcs.zones.read` | `internet-svcs.origin-error-page-pass-thru-setting.read`|
|Update origin error page passthrough settings.| `GET /v1/{crn}/zones/{domain_id}/setting/origin_error_page_pass_thru` | `internet-svcs.zones.update` | `internet-svcs.origin-error-page-pass-thru-setting.update`|
|Get brotli compression settings.| `GET /v1/{crn}/zones/{domain_id}/setting/brotli` | `internet-svcs.performance.read` | `internet-svcs.brotli-setting.read`|
|Update brotli compression settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/brotli` | `internet-svcs.performance.update` | `internet-svcs.brotli-setting.update`|
|Get Email obfuscation settings.| `GET /v1/{crn}/zones/{domain_id}/setting/email_obfuscation` | `internet-svcs.security.read` | `internet-svcs.email-obfuscation-setting.read`|
|Update Email obfuscation settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/email_obfuscation` | `internet-svcs.security.update` | `internet-svcs.email-obfuscation-setting.update`|
|Get ciphers settings.| `GET /v1/{crn}/zones/{domain_id}/setting/ciphers` | `internet-svcs.security.read` | `internet-svcs.ciphers-setting.read`|
|Update ciphers settings.| `PUT /v1/{crn}/zones/{domain_id}/setting/ciphers` | `internet-svcs.security.update` | `internet-svcs.ciphers-setting.update`|
{: caption="Table 21. Domain settings" caption-side="bottom"}


## Bot Management
{: #at_iam_CIS_bot-management}

| Action                                    | Method            | IAM ACTION   |  AT ACTION |
|-------------------------------------------|-------------------|--------------|------------|
|Get Bot Management settings.| `GET /v1/{crn}/zones/{domain_id}/bot_management}` | `internet-svcs.reliability.read` | `internet-svcs.bot-management.read`|
|Update Bot Management settings.| `PUT /v1/{crn}/zones/{domain_id}/bot_management}` | `internet-svcs.reliability.update` | `internet-svcs.bot-management.update`|
|Get Bot Analytics Score Source.| `GET /v1/{crn}/zones/{domain_id}/bot_analytics/score_source}` | `internet-svcs.security.read` | `internet-svcs.bot-analytics.read`|
|Get Bot Analytics Timeseries.| `GET /v1/{crn}/zones/{domain_id}/bot_analytics/timeseries}` | `internet-svcs.security.read` | `internet-svcs.bot-analytics.read`|
|Get Bot Analytics Top Attributes.| `GET /v1/{crn}/zones/{domain_id}/bot_analytics/top_ns}` | `internet-svcs.security.read` | `internet-svcs.bot-analytics.read`|
{: caption="Table 22. Bot Management" caption-side="bottom"}
