---

copyright:
  years: 2020, 2026
lastupdated: "2026-10-08"

keywords: IBM Cloud, observability

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# IAM and Activity Tracker actions by API
{: #at_iam_CIS}

List of IAM actions and Activity Tracker actions by API method.
{: shortdesc}



## Overview
{: #at_iam_CIS_overview}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get an overview | `get_zone_overview` | `GET /v2/{crn}/zones/{domain_id}/overview` | `internet-svcs.zones.read` | `internet-svcs.overview.read` |
{: caption="Overview" caption-side="bottom"}



## DNS Domains
{: #at_iam_CIS_domains}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| List the domains or get domain details | `list_zones` | `GET /v1/{crn}/zones` | `internet-svcs.zones.read` | `internet-svcs.zones.read` |
| Create a domain | `create_zone` | `POST /v1/{crn}/zones` | `internet-svcs.zones.manage` | `internet-svcs.zones.create` |
| Update a domain | `update_zone` | `PATCH /v1/{crn}/zones/{domain_id}` | `internet-svcs.reliability.update` | `internet-svcs.zones.update` |
| Delete a domain | `delete_zone` | `DELETE /v1/{crn}/zones/{domain_id}` | `internet-svcs.reliability.manage` | `internet-svcs.zones.delete` |
| Run an activation check on a domain | `replace_zone_activation_check` | `PUT /v1/{crn}/zones/{domain_id}/activation_check` | `internet-svcs.reliability.update` | `internet-svcs.zones-activation-check.update` |
| Get the DNSSEC configuration | `get_zone_dnssec` | `GET /v1/{crn}/zones/{domain_id}/dnssec` | `internet-svcs.reliability.read` | `internet-svcs.dnssec.read` |
| Enable or disable DNSSEC | `update_zone_dnssec` | `PATCH /v1/{crn}/zones/{domain_id}/dnssec` | `internet-svcs.reliability.update` | `internet-svcs.dnssec.update` |
| Get the zone subscription | `get_zone_subscription` | `GET /v1/{crn}/zones/{domain_id}/subscription` | `internet-svcs.zones.read` | `internet-svcs.zone_subscription.read` |
| Update the zone subscription | `update_zone_subscription` | `PUT /v1/{crn}/zones/{domain_id}/subscription` | `internet-svcs.zones.manage` | `internet-svcs.zone_subscription.update` |
| Get zone hold | `get_zone_hold` | `GET /v1/{crn}/zones/{domain_id}/hold` | `internet-svcs.reliability.read` | `internet-svcs.zone_hold.read` |
| Create zone hold | `create_zone_hold` | `POST /v1/{crn}/zones/{domain_id}/hold` | `internet-svcs.reliability.manage` | `internet-svcs.zone_hold.create` |
| Delete zone hold | `delete_zone_hold` | `DELETE /v1/{crn}/zones/{domain_id}/hold` | `internet-svcs.reliability.read` | `internet-svcs.zone_hold.read` |
| Trace a request | `trace_request` | `POST /v1/{crn}/zones/{domain_id}/trace` | `internet-svcs.zones.read` | `internet-svcs.trace-request.create` |
{: caption="DNS domains" caption-side="bottom"}


## DNS Records
{: #at_iam_CIS_records}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the DNS records | `list_zone_dns_records` | `GET /v1/{crn}/zones/{domain_id}/dns_records` | `internet-svcs.reliability.read` | `internet-svcs.dns-records.read` |
| Create a DNS record | `create_zone_dns_record` | `POST /v1/{crn}/zones/{domain_id}/dns_records` | `internet-svcs.reliability.manage` | `internet-svcs.dns-records.create` |
| Update a DNS record | `replace_zone_dns_record` | `PUT /v1/{crn}/zones/{domain_id}/dns_records/{record_id}` | `internet-svcs.reliability.update` | `internet-svcs.dns-records.update` |
| Delete a DNS record | `delete_zone_dns_record` | `DELETE /v1/{crn}/zones/{domain_id}/dns_records/{record_id}` | `internet-svcs.reliability.manage` | `internet-svcs.dns-records.delete` |
| Import the DNS records from zone file | `get_dns_records_bulk` | `GET /v1/{crn}/zones/{domain_id}/dns_records_bulk` | `internet-svcs.reliability.read` | `internet-svcs.dns-records-bulk.read` |
| Export the DNS records to a zone file | `post_dns_records_bulk` | `POST /v1/{crn}/zones/{domain_id}/dns_records_bulk` | `internet-svcs.reliability.manage` | `internet-svcs.dns-records-bulk.create` |
{: caption="DNS records" caption-side="bottom"}



## GLB
{: #at_iam_CIS_GLB}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the global load balancers | `list_zone_load_balancers` | `GET /v1/{crn}/zones/{domain_id}/load_balancers` | `internet-svcs.reliability.read` | `internet-svcs.load-balancers.read` |
| Create a global load balancer | `create_zone_load_balancer` | `POST /v1/{crn}/zones/{domain_id}/load_balancers` | `internet-svcs.reliability.manage` | `internet-svcs.load-balancers.create` |
| Update a global load balancer | `replace_zone_load_balancer` | `PUT /v1/{crn}/zones/{domain_id}/load_balancers/{glb_id}` | `internet-svcs.reliability.update` | `internet-svcs.load-balancers.update` |
| Delete a global load balancer | `delete_zone_load_balancer` | `DELETE /v1/{crn}/zones/{domain_id}/load_balancers/{glb_id}` | `internet-svcs.reliability.manage` | `internet-svcs.load-balancers.delete` |
| Get the load balancer events | `get_load_balancer_events` | `GET /v1/{crn}/load_balancers/events` | `internet-svcs.zones.read` | `internet-svcs.load-balancer-events.read` |
| Get the health monitors | `list_load_balancer_monitors` | `GET /v1/{crn}/load_balancers/monitors` | `internet-svcs.zones.read` | `internet-svcs.load-balancer-monitors.read` |
| Create a health monitor | `create_load_balancer_monitor` | `POST /v1/{crn}/load_balancers/monitors` | `internet-svcs.zones.manage` | `internet-svcs.load-balancer-monitors.create` |
| Update a health monitor | `edit_load_balancer_monitor` | `PUT /v1/{crn}/load_balancers/monitors/{monitor_id}` | `internet-svcs.zones.update` | `internet-svcs.load-balancer-monitors.update` |
| Delete a health monitor | `delete_load_balancer_monitor` | `DELETE /v1/{crn}/load_balancers/monitors/{monitor_id}` | `internet-svcs.zones.manage` | `internet-svcs.load-balancer-monitors.delete` |
| Get the load balancer pools | `list_load_balancer_pools` | `GET /v1/{crn}/load_balancers/pools` | `internet-svcs.zones.read` | `internet-svcs.load-balancer-pools.read` |
| Create a load balancer pool | `create_load_balancer_pool` | `POST /v1/{crn}/load_balancers/pools` | `internet-svcs.zones.manage` | `internet-svcs.load-balancer-pools.create` |
| Update a load balancer pool | `edit_load_balancer_pool` | `PUT /v1/{crn}/load_balancers/pools/{pool_id}` | `internet-svcs.zones.update` | `internet-svcs.load-balancer-pools.update` |
| Delete a load balancer pool | `delete_load_balancer_pool` | `DELETE /v1/{crn}/load_balancers/pools/{pool_id}` | `internet-svcs.zones.manage` | `internet-svcs.load-balancer-pools.delete` |
{: caption="GLB" caption-side="bottom"}


## Metrics
{: #at_iam_CIS_Metrics}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the dashboard analytics | `analytics_dashboard` | `GET /v1/{crn}/zones/{domain_id}/analytics/dashboard` | `internet-svcs.reliability.read` | `internet-svcs.dashboard-analytics.read` |
| Get the HTTP requests analytics | `analytics_http_requests` | `GET /v1/{crn}/zones/{domain_id}/analytics/http_requests` | `internet-svcs.reliability.read` | `internet-svcs.http-requests-analytics.read` |
| Get the HTTP requests analytics by colocations | `analytics_by_colos` | `GET /v1/{crn}/zones/{domain_id}/analytics/colos` | `internet-svcs.reliability.read` | `internet-svcs.colos-analytics.read` |
| Get the DNS analytics | `dns_analytics` | `GET /v1/{crn}/zones/{domain_id}/dns_analytics/report` | `internet-svcs.reliability.read` | `internet-svcs.dns-analytics.read` |
{: caption="Metrics" caption-side="bottom"}



## WAF
{: #at_iam_CIS_WAF}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| [Deprecated]{: tag-red}Get the WAF packages | `list_zone_firewall_waf_packages` | `GET /v1/{crn}/zones/{domain_id}/firewall/waf/packages` | `internet-svcs.security.read` | `internet-svcs.waf-packages.read` |
| Change the sensitivity and action mode of a WAF package | `update_zone_firewall_waf_package` | `PATCH /v1/{crn}/zones/{domain_id}/firewall/waf/packages/{package_id}` | `internet-svcs.security.update` | `internet-svcs.waf-packages.update` |
| [Deprecated]{: tag-red}Get the WAF groups | `list_zone_firewall_waf_package_groups` | `GET /v1/{crn}/zones/{domain_id}/firewall/waf/packages/{package_id}/groups` | `internet-svcs.security.read` | `internet-svcs.waf-groups.read` |
| Enable or disable a WAF group | `update_zone_firewall_waf_package_group` | `PATCH /v1/{crn}/zones/{domain_id}/firewall/waf/packages/{package_id}/groups/{group_id}` | `internet-svcs.security.update` | `internet-svcs.waf-groups.update` |
| [Deprecated]{: tag-red}Get the WAF rules | `list_zone_firewall_waf_package_rules` | `GET /v1/{crn}/zones/{domain_id}/firewall/waf/packages/{package_id}/rules` | `internet-svcs.security.read` | `internet-svcs.waf-rules.read` |
| Change the action mode of a WAF rule | `update_zone_firewall_waf_package_rule` | `PATCH /v1/{crn}/zones/{domain_id}/firewall/waf/packages/{package_id}/rules/{rule_id}` | `internet-svcs.security.update` | `internet-svcs.waf-rules.update` |
{: caption="WAF" caption-side="bottom"}



## IP Firewall
{: #at_iam_CIS_ip}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the IP firewall rules | `list_zone_firewall_access_rule_rules` | `GET /v1/{crn}/zones/{domain_id}/firewall/access_rules/rules` | `internet-svcs.security.read` | `internet-svcs.ip-firewall-rules.read` |
| Create an IP firewall rule | `create_zone_firewall_access_rule_rule` | `POST /v1/{crn}/zones/{domain_id}/firewall/access_rules/rules` | `internet-svcs.security.manage` | `internet-svcs.ip-firewall-rules.create` |
| Update an IP firewall rule | `update_zone_firewall_access_rule_rule` | `PATCH /v1/{crn}/zones/{domain_id}/firewall/access_rules/rules/{rule_id}` | `internet-svcs.security.update` | `internet-svcs.ip-firewall-rules.update` |
| Delete an IP firewall rule | `delete_zone_firewall_access_rule_rule` | `DELETE /v1/{crn}/zones/{domain_id}/firewall/access_rules/rules/{rule_id}` | `internet-svcs.security.manage` | `internet-svcs.ip-firewall-rules.delete` |
| Get the user-agent blocking rules | `list_zone_firewall_ua_rules` | `GET /v1/{crn}/zones/{domain_id}/firewall/ua_rules` | `internet-svcs.security.read` | `internet-svcs.ua-rules.read` |
| Create a user-agent blocking rule | `create_zone_firewall_ua_rule` | `POST /v1/{crn}/zones/{domain_id}/firewall/ua_rules` | `internet-svcs.security.manage` | `internet-svcs.ua-rules.create` |
| Update a user-agent blocking rule | `replace_zone_firewall_ua_rule` | `PUT /v1/{crn}/zones/{domain_id}/firewall/ua_rules/{rule_id}` | `internet-svcs.security.update` | `internet-svcs.ua-rules.update` |
| Delete a user-agent blocking rule | `delete_zone_firewall_ua_rule` | `DELETE /v1/{crn}/zones/{domain_id}/firewall/ua_rules/{rule_id}` | `internet-svcs.security.manage` | `internet-svcs.ua-rules.delete` |
| Get the domain lockdown rules | `list_zone_firewall_lockdowns` | `GET /v1/{crn}/zones/{domain_id}/firewall/lockdowns` | `internet-svcs.security.read` | `internet-svcs.domain-lockdown-rules.read` |
| Create a domain lockdown rule | `create_zone_firewall_lockdown` | `POST /v1/{crn}/zones/{domain_id}/firewall/lockdowns` | `internet-svcs.security.manage` | `internet-svcs.domain-lockdown-rules.create` |
| Update a domain lockdown rule | `replace_zone_firewall_lockdown` | `PUT /v1/{crn}/zones/{domain_id}/firewall/lockdowns/{rule_id}` | `internet-svcs.security.update` | `internet-svcs.domain-lockdown-rules.update` |
| Delete a domain lockdown rule | `delete_zone_firewall_lockdown` | `DELETE /v1/{crn}/zones/{domain_id}/firewall/lockdowns/{rule_id}` | `internet-svcs.security.manage` | `internet-svcs.domain-lockdown-rules.delete` |
{: caption="IP firewall" caption-side="bottom"}

## Firewall Rules
{: #at_iam_CIS_fw}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the firewall rules | `list_firewall_rules` | `GET /v1/{crn}/zones/{domain_id}/firewall/rules` | `internet-svcs.security.read` | `internet-svcs.firewall-rules.read` |
| Create a firewall rule | `create_firewall_rules` | `POST /v1/{crn}/zones/{domain_id}/firewall/rules` | `internet-svcs.security.manage` | `internet-svcs.firewall-rules.create` |
| Update a firewall rule | `update_firewallrule` | `PATCH /v1/{crn}/zones/{domain_id}/firewall/rules/{rule_id}` | `internet-svcs.security.update` | `internet-svcs.firewall-rules.update` |
| Delete a firewall rule | `delete_firewall_rule` | `DELETE /v1/{crn}/zones/{domain_id}/firewall/rules/{rule_id}` | `internet-svcs.security.manage` | `internet-svcs.firewall-rules.delete` |
| Get the filters | `list_filters` | `GET /v1/{crn}/zones/{domain_id}/filters` | `internet-svcs.security.read` | `internet-svcs.filters.read` |
| Create a filter | `create_filter` | `POST /v1/{crn}/zones/{domain_id}/filters` | `internet-svcs.security.manage` | `internet-svcs.filters.create` |
| Update a filter | `update_filter` | `PATCH /v1/{crn}/zones/{domain_id}/filters/{filter_id}` | `internet-svcs.security.update` | `internet-svcs.filters.update` |
| Delete a filter | `delete_filter` | `DELETE /v1/{crn}/zones/{domain_id}/filters/{filter_id}` | `internet-svcs.security.manage` | `internet-svcs.filters.delete` |
| Validate the expression of a filter | `validate_filter_expression` | `POST /v1/{crn}/zones/{domain_id}/filters/validate-expr` | `internet-svcs.security.manage` | `internet-svcs.filters-validate-expr.create` |
{: caption="Firewall rules" caption-side="bottom"}

## Security Events
{: #at_iam_CIS_secevents}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the security events | `security_events` | `GET /v1/{crn}/zones/{domain_id}/security/events` | `internet-svcs.security.read` | `internet-svcs.security-events.read` |
| Get the firewall events (Deprecated) | `firewall_events_analytics` | `GET /v1/{crn}/zones/{domain_id}/analytics/firewall_events [DEPRECATED]` | `internet-svcs.security.read` | `internet-svcs.firewall-events-analytics.read` |
{: caption="Security events" caption-side="bottom"}

## Rate Limiting
{: #at_iam_CIS_rate}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the rate-limiting rules | `list_zone_rate_limits` | `GET /v1/{crn}/zones/{domain_id}/rate_limits` | `internet-svcs.security.read` | `internet-svcs.rate-limits.read` |
| Create a rate-limiting rule | `create_zone_rate_limit` | `POST /v1/{crn}/zones/{domain_id}/rate_limits` | `internet-svcs.security.manage` | `internet-svcs.rate-limits.create` |
| Update a rate-limiting rule | `replace_zone_rate_limit` | `PUT /v1/{crn}/zones/{domain_id}/rate_limits/{ratelimit_id}` | `internet-svcs.security.update` | `internet-svcs.rate-limits.update` |
| Delete a rate-limiting rule | `delete_zone_rate_limit` | `DELETE /v1/{crn}/zones/{domain_id}/rate_limits/{ratelimit_id}` | `internet-svcs.security.manage` | `internet-svcs.rate-limits.delete` |
| Get the rate limiting analytics | `get_rate_limit_analytics` | `GET /v1/{crn}/zones/{domain_id}/rate_limit_analytics` | `internet-svcs.security.read` | `internet-svcs.rate-limit-analytics.read` |
{: caption="Rate limiting" caption-side="bottom"}


## Caching
{: #at_iam_CIS_Caching}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Purge all cached assets of a domain from edge server | `replace_zone_purge_cache_purge_all` | `PUT /v1/{crn}/zones/{domain_id}/purge_cache/purge_all` | `internet-svcs.performance.update` | `internet-svcs.purge-cache-all.update` |
| Purge the cached assets by URLs from edge server | `replace_zone_purge_cache_purge_by_urls` | `PUT /v1/{crn}/zones/{domain_id}/purge_cache/purge_by_urls` | `internet-svcs.performance.update` | `internet-svcs.purge-cache-by-urls.update` |
| Purge the cached assets by cache tags from edge server | `replace_zone_purge_cache_purge_by_cache_tags` | `PUT /v1/{crn}/zones/{domain_id}/purge_cache/purge_by_cache_tags` | `internet-svcs.performance.update` | `internet-svcs.purge-cache-by-cache-tags.update` |
| Purge the cached assets by hostnames from edge server | `replace_zone_purge_cache_purge_by_hosts` | `PUT /v1/{crn}/zones/{domain_id}/purge_cache/purge_by_hosts` | `internet-svcs.performance.update` | `internet-svcs.purge-cache-by-hosts.update` |
{: caption="Caching" caption-side="bottom"}

## Routing
{: #at_iam_CIS_Routing}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the smart routing configurations | `get_smart_routing` | `GET /v1/{crn}/zones/{domain_id}/routing/smart_routing` | `internet-svcs.performance.read` | `internet-svcs.smart-routing.read` |
| Enable or disable smart routing | `update_zone_routing_smart_routing` | `PATCH /v1/{crn}/zones/{domain_id}/routing/smart_routing` | `internet-svcs.performance.update` | `internet-svcs.smart-routing.update` |
| Get the tiered caching configurations | `get_routing_tiered_caching` | `GET /v1/{crn}/zones/{domain_id}/routing/tiered_caching` | `internet-svcs.performance.read` | `internet-svcs.tiered-caching.read` |
| Enable or disable tiered caching | `update_zone_routing_tiered_caching` | `PATCH /v1/{crn}/zones/{domain_id}/routing/tiered_caching` | `internet-svcs.performance.update` | `internet-svcs.tiered-caching.update` |
{: caption="Routing" caption-side="bottom"}


## Page Rules
{: #at_iam_CIS_pagerules}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the page rules | `list_zone_pagerules` | `GET /v1/{crn}/zones/{domain_id}/pagerules` | `internet-svcs.performance.read` | `internet-svcs.pagerules.read` |
| Create a page rule | `create_zone_pagerule` | `POST /v1/{crn}/zones/{domain_id}/pagerules` | `internet-svcs.performance.manage` | `internet-svcs.pagerules.create` |
| Update a page rule | `replace_zone_pagerule` | `PUT /v1/{crn}/zones/{domain_id}/pagerules/{rule_id}` | `internet-svcs.performance.update` | `internet-svcs.pagerules.update` |
| Delete a page rule | `delete_zone_pagerule` | `DELETE /v1/{crn}/zones/{domain_id}/pagerules/{rule_id}` | `internet-svcs.performance.manage` | `internet-svcs.pagerules.delete` |
{: caption="Page rules" caption-side="bottom"}



## TLS
{: #at_iam_CIS_TLS}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the universal SSL setting | `get_universal_certificate_setting` | `GET /v1/{crn}/zones/{domain_id}/ssl/universal/settings` | `internet-svcs.security.read` | `internet-svcs.universal-ssl-setting.read` |
| Update the universal SSL setting | `update_zone_ssl_universal_setting` | `PATCH /v1/{crn}/zones/{domain_id}/ssl/universal/settings` | `internet-svcs.security.update` | `internet-svcs.universal-ssl-setting.update` |
| Get the edge certificates ordered from CIS | `list_certificates` | `GET /v1/{crn}/zones/{domain_id}/ssl/certificate_packs` | `internet-svcs.security.read` | `internet-svcs.certificate-packs.read` |
| Order an edge certificate | `order_certificate` | `POST /v1/{crn}/zones/{domain_id}/ssl/certificate_packs` | `internet-svcs.security.manage` | `internet-svcs.certificate-packs.create` |
| Order an advanced certificate | `order_advanced_certificate` | `POST /v1/{crn}/zones/{domain_id}/ssl/certificate_packs/order` | `internet-svcs.security.manage` | `internet-svcs.certificate-packs.create` |
| Update an SSL certificate pack | `update_zone_ssl_certificate_pack` | `PATCH /v1/{crn}/zones/{domain_id}/ssl/certificate_packs/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.certificate-packs.update` |
| Delete an edge certificate | `delete_certificate` | `DELETE /v1/{crn}/zones/{domain_id}/ssl/certificate_packs/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.certificate-packs.delete` |
| Delete an SSL certificate pack | `delete_zone_ssl_certificate_pack` | `DELETE /v1/{crn}/zones/{domain_id}/ssl/certificate_packs/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.certificate-packs.delete` |
| Get the uploaded certificates | `list_zone_custom_certificates` | `GET /v1/{crn}/zones/{domain_id}/custom_certificates` | `internet-svcs.security.read` | `internet-svcs.custom-certificates.read` |
| Upload a certificate to CIS edge | `create_zone_custom_certificate` | `POST /v1/{crn}/zones/{domain_id}/custom_certificates` | `internet-svcs.security.manage` | `internet-svcs.custom-certificates.create` |
| Update the certificate uploaded to CIS edge | `update_zone_custom_certificate` | `PATCH /v1/{crn}/zones/{domain_id}/custom_certificates/{cert_id}` | `internet-svcs.security.update` | `internet-svcs.custom-certificates.update` |
| Delete a certificate uploaded to CIS edge | `delete_zone_custom_certificate` | `DELETE /v1/{crn}/zones/{domain_id}/custom_certificates/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.custom-certificates.delete` |
| Get origin certificates issued by CIS | `list_zone_origin_certificates` | `GET /v1/{crn}/zones/{domain_id}/origin_certificates` | `internet-svcs.security.read` | `internet-svcs.origin-certificates.read` |
| Create an origin certificate issued by CIS | `create_zone_origin_certificate` | `POST /v1/{crn}/zones/{domain_id}/origin_certificates` | `internet-svcs.security.manage` | `internet-svcs.origin-certificates.create` |
| Get a single origin certificate | `get_zone_origin_certificate` | `GET /v1/{crn}/zones/{domain_id}/origin_certificates/{cert_id}` | `internet-svcs.security.read` | `internet-svcs.origin-certificates.read` |
| Revoke an origin certificate issued by CIS | `delete_zone_origin_certificate` | `DELETE /v1/{crn}/zones/{domain_id}/origin_certificates/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.origin-certificates.delete` |
| Get Total TLS settings | `get_tls_settings` | `GET /v1/{crn}/zones/{domain_id}/tls/total_tls` | `internet-svcs.reliability.read` | `internet-svcs.total_tls.read` |
| Update Total TLS settings | `update_total_tls` | `PATCH /v1/{crn}/zones/{domain_id}/tls/total_tls` | `internet-svcs.reliability.update` | `internet-svcs.total_tls.update` |
| Get the Origin CA API key | `get_origin_ca_key` | `GET /v1/{crn}/zones/{domain_id}/origin_ca_key` | `internet-svcs.zones.create` | `internet-svcs.origin_ca_key.create` |
{: caption="TLS" caption-side="bottom"}

## Keyless SSL
{: #at_iam_CIS_keyless}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| List keyless SSL configurations | `get_keyless_ssl` | `GET /v1/{crn}/zones/{domain_id}/keyless_certificates` | `internet-svcs.reliability.read` | `internet-svcs.keyless_certificates.read` |
| Create a keyless SSL configuration | `create_keyless_ssl` | `POST /v1/{crn}/zones/{domain_id}/keyless_certificates` | `internet-svcs.reliability.manage` | `internet-svcs.keyless_certificates.create` |
| Get a keyless SSL configuration | `get_keyless_ssl_single` | `GET /v1/{crn}/zones/{domain_id}/keyless_certificates/{keyless_id}` | `internet-svcs.reliability.read` | `internet-svcs.keyless_certificates.read` |
| Update a keyless SSL configuration | `update_keyless_ssl` | `PATCH /v1/{crn}/zones/{domain_id}/keyless_certificates/{keyless_id}` | `internet-svcs.reliability.manage` | `internet-svcs.keyless_certificates.update` |
| Delete a keyless SSL configuration | `delete_keyless_ssl` | `DELETE /v1/{crn}/zones/{domain_id}/keyless_certificates/{keyless_id}` | `internet-svcs.reliability.read` | `internet-svcs.keyless_certificates.read` |
{: caption="Keyless SSL" caption-side="bottom"}


## Edge Functions
{: #at_iam_edge-func}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the edge function scripts | `list_worker_scripts` | `GET /v1/{crn}/workers/scripts` | `internet-svcs.performance.read` | `internet-svcs.edge-functions-scripts.read` |
| Create an edge function script | `create_worker_script` | `POST /v1/{crn}/workers/scripts` | `internet-svcs.performance.manage` | `internet-svcs.edge-functions-scripts.create` |
| Update an edge function script | `replace_worker_script` | `PUT /v1/{crn}/workers/scripts/{script_name}` | `internet-svcs.performance.update` | `internet-svcs.edge-functions-scripts.update` |
| Delete an edge function script | `delete_worker_script` | `DELETE /v1/{crn}/workers/scripts/{script_name}` | `internet-svcs.performance.manage` | `internet-svcs.edge-functions-scripts.delete` |
| Get the edge function routes | `list_zone_worker_routes` | `GET /v1/{crn}/zones/{domain_id}/workers/routes` | `internet-svcs.performance.read` | `internet-svcs.edge-functions-routes.read` |
| Create an edge function route | `create_zone_worker_route` | `POST /v1/{crn}/zones/{domain_id}/workers/routes` | `internet-svcs.performance.manage` | `internet-svcs.edge-functions-routes.create` |
| Update an edge function route | `replace_zone_worker_route` | `PUT /v1/{crn}/zones/{domain_id}/workers/routes/{route_id}` | `internet-svcs.performance.update` | `internet-svcs.edge-functions-routes.update` |
| Delete an edge function route | `delete_zone_worker_route` | `DELETE /v1/{crn}/zones/{domain_id}/workers/routes/{route_id}` | `internet-svcs.performance.manage` | `internet-svcs.edge-functions-routes.delete` |
{: caption="Edge functions" caption-side="bottom"}

## Range
{: #at_iam_range}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the range apps | `list_zone_range_apps` | `GET /v1/{crn}/zones/{domain_id}/range/apps` | `internet-svcs.security.read` | `internet-svcs.range-apps.read` |
| Create a range app | `create_zone_range_app` | `POST /v1/{crn}/zones/{domain_id}/range/apps` | `internet-svcs.security.manage` | `internet-svcs.range-apps.create` |
| Update a range app | `replace_zone_range_app` | `PUT /v1/{crn}/zones/{domain_id}/range/apps/{app_id}` | `internet-svcs.security.update` | `internet-svcs.range-apps.update` |
| Delete a range app | `delete_zone_range_app` | `DELETE /v1/{crn}/zones/{domain_id}/range/apps/{app_id}` | `internet-svcs.security.manage` | `internet-svcs.range-apps.delete` |
| Get the analytics of range apps | `range_analytics` | `GET /v1/{crn}/zones/{domain_id}/range/analytics/events/summary` | `internet-svcs.security.read` | `internet-svcs.range-analytics.read` |
{: caption="Range" caption-side="bottom"}

## Logpush
{: #at_iam_Logpush}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the Logpush fields | `get_logpush_fields` | `GET /v1/{crn}/zones/{domain_id}/logpush/datasets/{dataset}/fields` | `internet-svcs.zones.read` | `internet-svcs.logpush-fields.read` |
| Get the Logpush jobs | `get_logpush_jobs` | `GET /v1/{crn}/zones/{domain_id}/logpush/jobs` | `internet-svcs.zones.read` | `internet-svcs.logpush-jobs.read` |
| Create a Logpush job | `create_logpush_job` | `POST /v1/{crn}/zones/{domain_id}/logpush/jobs` | `internet-svcs.zones.manage` | `internet-svcs.logpush-jobs.create` |
| Update a Logpush job | `update_logpush_job` | `PUT /v1/{crn}/zones/{domain_id}/logpush/jobs/{job_id}` | `internet-svcs.zones.update` | `internet-svcs.logpush-jobs.update` |
| Delete a Logpush job | `delete_logpush_job` | `DELETE /v1/{crn}/zones/{domain_id}/logpush/jobs/{job_id}` | `internet-svcs.zones.manage` | `internet-svcs.logpush-jobs.delete` |
| Initiate the Logpush ownership challenge | `initiate_logpush_ownership` | `POST /v1/{crn}/zones/{domain_id}/logpush/ownership` | `internet-svcs.zones.manage` | `internet-svcs.logpush-ownership.create` |
| Validate the Logpush ownership challenge token | `validate_logpush_ownership` | `POST /v1/{crn}/zones/{domain_id}/logpush/ownership/validate` | `internet-svcs.zones.manage` | `internet-svcs.logpush-ownership-validate.create` |
{: caption="Logpush" caption-side="bottom"}

## Custom Pages
{: #at_iam_edge-Custom-Pages}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the custom error pages | `list_zone_custom_pages` | `GET /v1/{crn}/zones/{domain_id}/custom_pages` | `internet-svcs.zones.read` | `internet-svcs.custom-pages.read` |
| Update the custom error page | `replace_zone_custom_page` | `PUT /v1/{crn}/zones/{domain_id}/custom_pages/{page_id}` | `internet-svcs.zones.update` | `internet-svcs.custom-pages.update` |
{: caption="Custom pages" caption-side="bottom"}

## Mutual TLS
{: #at_iam_tls}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the certificates uploaded for mTLS | `list_mtls_certificates` | `GET /v1/{crn}/zones/{domain_id}/access/certificates` | `internet-svcs.security.read` | `internet-svcs.access-certificates.read` |
| Upload a certificate for mTLS | `create_mtls_certificate` | `POST /v1/{crn}/zones/{domain_id}/access/certificates` | `internet-svcs.security.manage` | `internet-svcs.access-certificates.create` |
| Update a certificate for mTLS | `update_mtls_certificate` | `PUT /v1/{crn}/zones/{domain_id}/access/certificates/{cert_id}` | `internet-svcs.security.update` | `internet-svcs.access-certificates.update` |
| Delete a certificate for mTLS | `delete_mtls_certificate` | `DELETE /v1/{crn}/zones/{domain_id}/access/certificates/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.access-certificates.delete` |
| Get the mTLS applications | `list_mtls_apps` | `GET /v1/{crn}/zones/{domain_id}/access/apps` | `internet-svcs.security.read` | `internet-svcs.access-apps.read` |
| Create a mTLS application | `create_mtls_app` | `POST /v1/{crn}/zones/{domain_id}/access/apps` | `internet-svcs.security.manage` | `internet-svcs.access-apps.create` |
| Update a mTLS application | `update_mtls_app` | `PUT /v1/{crn}/zones/{domain_id}/access/apps/{app_id}` | `internet-svcs.security.update` | `internet-svcs.access-apps.update` |
| Delete a mTLS application | `delete_mtls_app` | `DELETE /v1/{crn}/zones/{domain_id}/access/apps/{app_id}` | `internet-svcs.security.manage` | `internet-svcs.access-apps.delete` |
| Get the mTLS policies | `list_mtls_policies` | `GET /v1/{crn}/zones/{domain_id}/access/apps/{app_id}/policies` | `internet-svcs.security.read` | `internet-svcs.access-policies.read` |
| Create a mTLS policy | `create_mtls_policy` | `POST /v1/{crn}/zones/{domain_id}/access/apps/{app_id}/policies` | `internet-svcs.security.manage` | `internet-svcs.access-policies.create` |
| Update a mTLS policy | `update_mtls_policy` | `PUT /v1/{crn}/zones/{domain_id}/access/apps/{app_id}/policies/{policy_id}` | `internet-svcs.security.update` | `internet-svcs.access-policies.update` |
| Delete a mTLS policy | `delete_mtls_policy` | `DELETE /v1/{crn}/zones/{domain_id}/access/apps/{app_id}` | `internet-svcs.security.manage` | `internet-svcs.access-policies.delete` |
{: caption="Mutual TLS" caption-side="bottom"}

## Origin TLS Client Authentication
{: #at_iam_tls-client-auth}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| List the certificates used for origin TLS client authentication | `list_origin_tls_client_auth` | `GET /v1/{crn}/zones/{domain_id}/origin_tls_client_auth` | `internet-svcs.security.read` | `internet-svcs.origin-tls-client-auth.read` |
| Create a certificate for origin TLS client authentication | `create_origin_tls_client_auth` | `POST /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.origin-tls-client-auth.create` |
| Delete a certificate for origin TLS client authentication | `delete_origin_tls_client_auth` | `DELETE /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.origin-tls-client-auth.delete` |
| Get the origin TLS client authentication settings | `get_origin_tls_client_auth_settings` | `GET /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/settings` | `internet-svcs.security.read` | `internet-svcs.origin-tls-client-auth-settings.read` |
| Update the origin TLS client authentication settings | `update_origin_tls_client_auth_settings` | `PUT /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/settings` | `internet-svcs.security.update` | `internet-svcs.origin-tls-client-auth-settings.update` |
| Get the origin TLS client authentication settings for the hostname | `get_origin_tls_client_auth_hostname` | `GET /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/hostnames/{hostname}` | `internet-svcs.security.read` | `internet-svcs.origin-tls-client-auth-hostnames.read` |
| Update the origin TLS client authentication settings for a hostname | `update_origin_tls_client_auth_hostname` | `PUT /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/hostnames` | `internet-svcs.security.update` | `internet-svcs.origin-tls-client-auth-hostnames.update` |
| Get the origin TLS client authentication certificates at the hostname level | `get_origin_tls_client_auth_hostname_cert` | `GET /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/hostnames/certificates/{cert_id}` | `internet-svcs.security.read` | `internet-svcs.origin-tls-client-auth-hostname-certificates.read` |
| Create an origin TLS client authentication certificate at the hostname level | `create_origin_tls_client_auth_hostname_cert` | `POST /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/hostnames/certificates` | `internet-svcs.security.manage` | `internet-svcs.origin-tls-client-auth-hostname-certificates.create` |
| Delete an origin TLS client authentication certificate at the hostname level | `delete_origin_tls_client_auth_hostname_cert` | `DELETE /v1/{crn}/zones/{domain_id}/origin_tls_client_auth/hostnames/certificates/{cert_id}` | `internet-svcs.security.manage` | `internet-svcs.origin-tls-client-auth-hostname-certificates.delete` |
{: caption="Origin TLS Client Authentication" caption-side="bottom"}

## Rulesets (Instance-level)
{: #at_iam_CIS_rulesets-instance}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| List rulesets | `list_rulesets` | `GET /v1/{crn}/rulesets` | `internet-svcs.zones.read` | `internet-svcs.rulesets.read` |
| Get a ruleset | `get_ruleset` | `GET /v1/{crn}/rulesets/{ruleset_id}` | `internet-svcs.zones.read` | `internet-svcs.rulesets.read` |
| Replace a ruleset | `replace_ruleset` | `PUT /v1/{crn}/rulesets/{ruleset_id}` | `internet-svcs.zones.manage` | `internet-svcs.rules.update` |
| Delete a ruleset | `delete_ruleset` | `DELETE /v1/{crn}/rulesets/{ruleset_id}` | `internet-svcs.zones.manage` | `internet-svcs.rulesets.delete` |
| List ruleset versions | `list_ruleset_versions` | `GET /v1/{crn}/rulesets/{ruleset_id}/versions` | `internet-svcs.zones.read` | `internet-svcs.rulesets-versions.read` |
| Get a ruleset version | `get_ruleset_version` | `GET /v1/{crn}/rulesets/{ruleset_id}/versions/{version}` | `internet-svcs.zones.read` | `internet-svcs.rulesets-versions.read` |
| Delete a ruleset version | `delete_ruleset_version` | `DELETE /v1/{crn}/rulesets/{ruleset_id}/versions/{version}` | `internet-svcs.zones.manage` | `internet-svcs.rulesets-versions.delete` |
| Get the ruleset phase entrypoint | `get_ruleset_phase_entrypoint` | `GET /v1/{crn}/rulesets/phases/{phase}/entrypoint` | `internet-svcs.zones.read` | `internet-svcs.rulesets-phases-entrypoint.read` |
| Replace the ruleset phase entrypoint | `replace_ruleset_phase_entrypoint` | `PUT /v1/{crn}/rulesets/phases/{phase}/entrypoint` | `internet-svcs.zones.manage` | `internet-svcs.rulesets-phases-entrypoint.update` |
| List ruleset phase entrypoint versions | `list_ruleset_phase_entrypoint_versions` | `GET /v1/{crn}/rulesets/phases/{phase}/entrypoint/versions` | `internet-svcs.zones.read` | `internet-svcs.rulesets-phases-entrypoint-versions.read` |
| Get a ruleset phase entrypoint version | `get_ruleset_phase_entrypoint_version` | `GET /v1/{crn}/rulesets/phases/{phase}/entrypoint/versions/{version}` | `internet-svcs.zones.read` | `internet-svcs.rulesets-phases-entrypoint-versions.read` |
| Create a ruleset rule | `create_ruleset_rule` | `POST /v1/{crn}/rulesets/{ruleset_id}/rules` | `internet-svcs.zones.manage` | `internet-svcs.rulesets-rules.create` |
| Update a ruleset rule | `update_ruleset_rule` | `PATCH /v1/{crn}/rulesets/{ruleset_id}/rules/{rule_id}` | `internet-svcs.zones.manage` | `internet-svcs.rulesets-rules.update` |
| Delete a ruleset rule | `delete_ruleset_rule` | `DELETE /v1/{crn}/rulesets/{ruleset_id}/rules/{rule_id}` | `internet-svcs.zones.read` | `internet-svcs.rulesets-rules.read` |
| Get ruleset version by tag | `get_ruleset_version_by_tag` | `GET /v1/{crn}/rulesets/{ruleset_id}/versions/{version}/by_tag/{tag}` | `internet-svcs.zones.read` | `internet-svcs.rulesets-versions-by-tag.read` |
{: caption="Rulesets (Instance-level)" caption-side="bottom"}

## Rulesets (Zone-level)
{: #at_iam_CIS_rulesets-zone}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| List zone rulesets | `list_zone_rulesets` | `GET /v1/{crn}/zones/{domain_id}/rulesets` | `internet-svcs.security.read` | `internet-svcs.zone-rulesets.read` |
| Get a zone ruleset | `get_zone_ruleset` | `GET /v1/{crn}/zones/{domain_id}/rulesets/{ruleset_id}` | `internet-svcs.security.read` | `internet-svcs.zone-rulesets.read` |
| Replace a zone ruleset | `replace_zone_ruleset` | `PUT /v1/{crn}/zones/{domain_id}/rulesets/{ruleset_id}` | `internet-svcs.security.manage` | `internet-svcs.zone-rulesets.update` |
| Delete a zone ruleset | `delete_zone_ruleset` | `DELETE /v1/{crn}/zones/{domain_id}/rulesets/{ruleset_id}` | `internet-svcs.security.manage` | `internet-svcs.zone-rulesets.delete` |
| List zone ruleset versions | `list_zone_ruleset_versions` | `GET /v1/{crn}/zones/{domain_id}/rulesets/{ruleset_id}/versions` | `internet-svcs.security.read` | `internet-svcs.zone-rulesets-versions.read` |
| Get a zone ruleset version | `get_zone_ruleset_version` | `GET /v1/{crn}/zones/{domain_id}/rulesets/{ruleset_id}/versions/{version}` | `internet-svcs.security.read` | `internet-svcs.zone-rulesets-versions.read` |
| Delete a zone ruleset version | `delete_zone_ruleset_version` | `DELETE /v1/{crn}/zones/{domain_id}/rulesets/{ruleset_id}/versions/{version}` | `internet-svcs.security.manage` | `internet-svcs.zone-rulesets-versions.delete` |
| Get the zone ruleset phase entrypoint | `get_zone_ruleset_phase_entrypoint` | `GET /v1/{crn}/zones/{domain_id}/rulesets/phases/{phase}/entrypoint` | `internet-svcs.security.read` | `internet-svcs.zone-rulesets-phases-entrypoint.read` |
| Replace the zone ruleset phase entrypoint | `replace_zone_ruleset_phase_entrypoint` | `PUT /v1/{crn}/zones/{domain_id}/rulesets/phases/{phase}/entrypoint` | `internet-svcs.security.manage` | `internet-svcs.zone-rulesets-phases-entrypoint.update` |
| List zone ruleset phase entrypoint versions | `list_zone_ruleset_phase_entrypoint_versions` | `GET /v1/{crn}/zones/{domain_id}/rulesets/phases/{phase}/entrypoint/versions` | `internet-svcs.security.read` | `internet-svcs.zone-rulesets-phases-entrypoint-versions.read` |
| Get a zone ruleset phase entrypoint version | `get_zone_ruleset_phase_entrypoint_version` | `GET /v1/{crn}/zones/{domain_id}/rulesets/phases/{phase}/entrypoint/versions/{version}` | `internet-svcs.security.read` | `internet-svcs.zone-rulesets-phases-entrypoint-versions.read` |
| Create a zone ruleset rule | `create_zone_ruleset_rule` | `POST /v1/{crn}/zones/{domain_id}/rulesets/{ruleset_id}/rules` | `internet-svcs.security.manage` | `internet-svcs.zone-rulesets-rules.create` |
| Update a zone ruleset rule | `update_zone_ruleset_rule` | `PATCH /v1/{crn}/zones/{domain_id}/rulesets/{ruleset_id}/rules/{rule_id}` | `internet-svcs.security.manage` | `internet-svcs.zone-rulesets-rules.update` |
| Delete a zone ruleset rule | `delete_zone_ruleset_rule` | `DELETE /v1/{crn}/zones/{domain_id}/rulesets/{ruleset_id}/rules/{rule_id}` | `internet-svcs.security.manage` | `internet-svcs.zone-rulesets-rules.delete` |
{: caption="Rulesets (Zone-level)" caption-side="bottom"}

## Bot Management
{: #at_iam_CIS_bot-management}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the Bot Management settings | `get_bot_management` | `GET /v1/{crn}/zones/{domain_id}/bot_management` | `internet-svcs.security.read` | `internet-svcs.bot_management.read` |
| Update the Bot Management settings | `replace_zone_bot_management` | `PUT /v1/{crn}/zones/{domain_id}/bot_management` | `internet-svcs.security.update` | `internet-svcs.bot_management.update` |
| Get the Bot Analytics Score Source | `get_bot_score` | `GET /v1/{crn}/zones/{domain_id}/bot_analytics/score_source` | `internet-svcs.security.read` | `internet-svcs.bot_score.read` |
| Get the Bot Analytics Timeseries | `get_bot_timeseries` | `GET /v1/{crn}/zones/{domain_id}/bot_analytics/timeseries` | `internet-svcs.security.read` | `internet-svcs.bot_timeseries.read` |
| Get the Bot Analytics Top Attributes | `get_bot_topns` | `GET /v1/{crn}/zones/{domain_id}/bot_analytics/top_ns` | `internet-svcs.security.read` | `internet-svcs.bot_topns.read` |
{: caption="Bot management" caption-side="bottom"}

## URL Normalization
{: #at_iam_CIS_url-normalization}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get URL normalization settings | `get_url_normalization` | `GET /v1/{crn}/zones/{domain_id}/url_normalization` | `internet-svcs.reliability.read` | `internet-svcs.url_normalization.read` |
| Update URL normalization settings | `update_url_normalization` | `PATCH /v1/{crn}/zones/{domain_id}/url_normalization` | `internet-svcs.security.update` | `internet-svcs.url_normalization.update` |
{: caption="URL normalization" caption-side="bottom"}

## Domain settings
{: #at_iam_CIS_domain-settings}

| Action | Operation ID | Method | IAM ACTION | AT ACTION |
|--------|-------------|--------|------------|-----------|
| Get the CNAME flattening settings | `get_cname_flattening` | `GET /v1/{crn}/zones/{domain_id}/setting/cname_flattening` | `internet-svcs.reliability.read` | `internet-svcs.cname-flattening-setting.read` |
| Update the CNAME flattening settings | `update_cname_flattening` | `PUT /v1/{crn}/zones/{domain_id}/setting/cname_flattening` | `internet-svcs.reliability.update` | `internet-svcs.cname-flattening-setting.update` |
| Get the cache level settings | `get_cache_level` | `GET /v1/{crn}/zones/{domain_id}/setting/cache_level` | `internet-svcs.performance.read` | `internet-svcs.cache-level-setting.read` |
| Update the cache level settings | `update_cache_level` | `PUT /v1/{crn}/zones/{domain_id}/setting/cache_level` | `internet-svcs.performance.update` | `internet-svcs.cache-level-setting.update` |
| Get the browser cache TTL settings | `get_browser_cache_ttl` | `GET /v1/{crn}/zones/{domain_id}/setting/browser_cache_ttl` | `internet-svcs.performance.read` | `internet-svcs.browser-cache-ttl-setting.read` |
| Update the browser cache TTL settings | `update_browser_cache_ttl` | `PUT /v1/{crn}/zones/{domain_id}/setting/browser_cache_ttl` | `internet-svcs.performance.update` | `internet-svcs.browser-cache-ttl-setting.update` |
| Get the always online settings | `get_always_online` | `GET /v1/{crn}/zones/{domain_id}/setting/always_online` | `internet-svcs.performance.read` | `internet-svcs.always-online-setting.read` |
| Update the always online settings | `update_always_online` | `PUT /v1/{crn}/zones/{domain_id}/setting/always_online` | `internet-svcs.performance.update` | `internet-svcs.always-online-setting.update` |
| Get the development mode settings | `get_development_mode` | `GET /v1/{crn}/zones/{domain_id}/setting/development_mode` | `internet-svcs.performance.read` | `internet-svcs.development-mode-setting.read` |
| Update the development mode settings | `update_development_mode` | `PUT /v1/{crn}/zones/{domain_id}/setting/development_mode` | `internet-svcs.performance.update` | `internet-svcs.development-mode-setting.update` |
| Get the sort query string for cache settings | `get_sort_query_string_for_cache` | `GET /v1/{crn}/zones/{domain_id}/setting/sort_query_string_for_cache` | `internet-svcs.performance.read` | `internet-svcs.sort-query-string-for-cache-setting.read` |
| Update the sort query string for cache settings | `update_sort_query_string_for_cache` | `PUT /v1/{crn}/zones/{domain_id}/setting/sort_query_string_for_cache` | `internet-svcs.performance.update` | `internet-svcs.sort-query-string-for-cache-setting.update` |
| Get the SSL settings | `get_ssl` | `GET /v1/{crn}/zones/{domain_id}/setting/ssl` | `internet-svcs.security.read` | `internet-svcs.ssl-setting.read` |
| Update the SSL settings | `update_ssl` | `PUT /v1/{crn}/zones/{domain_id}/setting/ssl` | `internet-svcs.security.update` | `internet-svcs.ssl-setting.update` |
| Get the security level settings | `get_security_level` | `GET /v1/{crn}/zones/{domain_id}/setting/security_level` | `internet-svcs.security.read` | `internet-svcs.security-level-setting.read` |
| Update the security level settings | `update_security_level` | `PUT /v1/{crn}/zones/{domain_id}/setting/security_level` | `internet-svcs.security.update` | `internet-svcs.security-level-setting.update` |
| Get the TLS 1.2 settings | `get_tls_1_2_only` | `GET /v1/{crn}/zones/{domain_id}/setting/tls_1_2_only` | `internet-svcs.security.read` | `internet-svcs.tls-1-2-only-setting.read` |
| Update the TLS 1.2 settings | `update_tls_1_2_only` | `PUT /v1/{crn}/zones/{domain_id}/setting/tls_1_2_only` | `internet-svcs.security.update` | `internet-svcs.tls-1-2-only-setting.update` |
| Get the TLS 1.3 settings | `get_tls_1_3` | `GET /v1/{crn}/zones/{domain_id}/setting/tls_1_3` | `internet-svcs.security.read` | `internet-svcs.tls-1-3-setting.read` |
| Update the TLS 1.3 settings | `update_tls_1_3` | `PUT /v1/{crn}/zones/{domain_id}/setting/tls_1_3` | `internet-svcs.security.update` | `internet-svcs.tls-1-3-setting.update` |
| Get the automatic HTTPS rewrites settings | `get_automatic_https_rewrites` | `GET /v1/{crn}/zones/{domain_id}/setting/automatic_https_rewrites` | `internet-svcs.security.read` | `internet-svcs.automatic-https-rewrites-setting.read` |
| Update the automatic HTTPS rewrites settings | `update_automatic_https_rewrites` | `PUT /v1/{crn}/zones/{domain_id}/setting/automatic_https_rewrites` | `internet-svcs.security.update` | `internet-svcs.automatic-https-rewrites-setting.update` |
| Get the WAF settings | `get_waf` | `GET /v1/{crn}/zones/{domain_id}/setting/waf` | `internet-svcs.security.read` | `internet-svcs.waf-setting.read` |
| Update the WAF settings | `update_waf` | `PUT /v1/{crn}/zones/{domain_id}/setting/waf` | `internet-svcs.security.update` | `internet-svcs.waf-setting.update` |
| Get the browser integrity check settings | `get_browser_check` | `GET /v1/{crn}/zones/{domain_id}/setting/browser_check` | `internet-svcs.security.read` | `internet-svcs.browser-check-setting.read` |
| Update the browser integrity check settings | `update_browser_check` | `PUT /v1/{crn}/zones/{domain_id}/setting/browser_check` | `internet-svcs.security.update` | `internet-svcs.browser-check-setting.update` |
| Get the opportunistic encryption settings | `get_opportunistic_encryption` | `GET /v1/{crn}/zones/{domain_id}/setting/opportunistic_encryption` | `internet-svcs.security.read` | `internet-svcs.opportunistic-encryption-setting.read` |
| Update the opportunistic encryption settings | `update_opportunistic_encryption` | `PUT /v1/{crn}/zones/{domain_id}/setting/opportunistic_encryption` | `internet-svcs.security.update` | `internet-svcs.opportunistic-encryption-setting.update` |
| Get the challenge TTL settings | `get_challenge_ttl` | `GET /v1/{crn}/zones/{domain_id}/setting/challenge_ttl` | `internet-svcs.security.read` | `internet-svcs.challenge-ttl-setting.read` |
| Update the challenge TTL settings | `update_challenge_ttl` | `PUT /v1/{crn}/zones/{domain_id}/setting/challenge_ttl` | `internet-svcs.security.update` | `internet-svcs.challenge-ttl-setting.update` |
| Get the always use HTTPS settings | `get_always_use_https` | `GET /v1/{crn}/zones/{domain_id}/setting/always_use_https` | `internet-svcs.security.read` | `internet-svcs.always-use-https-setting.read` |
| Update the always use HTTPS settings | `update_always_use_https` | `PUT /v1/{crn}/zones/{domain_id}/setting/always_use_https` | `internet-svcs.security.update` | `internet-svcs.always-use-https-setting.update` |
| Get the true client IP header settings | `get_true_client_ip_header` | `GET /v1/{crn}/zones/{domain_id}/setting/true_client_ip_header` | `internet-svcs.zones.read` | `internet-svcs.true-client-ip-header-setting.read` |
| Update the true client IP header settings | `update_true_client_ip_header` | `PUT /v1/{crn}/zones/{domain_id}/setting/true_client_ip_header` | `internet-svcs.zones.update` | `internet-svcs.true-client-ip-header-setting.update` |
| Get the image size optimization settings | `get_image_size_optimization` | `GET /v1/{crn}/zones/{domain_id}/setting/image_size_optimization` | `internet-svcs.performance.read` | `internet-svcs.image-size-optimization-setting.read` |
| Update the image size optimization settings | `update_image_size_optimization` | `PUT /v1/{crn}/zones/{domain_id}/setting/image_size_optimization` | `internet-svcs.performance.update` | `internet-svcs.image-size-optimization-setting.update` |
| Get the script load optimization settings | `get_script_load_optimization` | `GET /v1/{crn}/zones/{domain_id}/setting/script_load_optimization` | `internet-svcs.performance.read` | `internet-svcs.script-load-optimization-setting.read` |
| Update the script load optimization settings | `update_script_load_optimization` | `PUT /v1/{crn}/zones/{domain_id}/setting/script_load_optimization` | `internet-svcs.performance.update` | `internet-svcs.script-load-optimization-setting.update` |
| Get the image load optimization settings | `get_image_load_optimization` | `GET /v1/{crn}/zones/{domain_id}/setting/image_load_optimization` | `internet-svcs.performance.read` | `internet-svcs.image-load-optimization-setting.read` |
| Update the image load optimization settings | `update_image_load_optimization` | `PUT /v1/{crn}/zones/{domain_id}/setting/image_load_optimization` | `internet-svcs.performance.update` | `internet-svcs.image-load-optimization-setting.update` |
| Get the minification settings | `get_minify` | `GET /v1/{crn}/zones/{domain_id}/setting/minify` | `internet-svcs.performance.read` | `internet-svcs.minify-setting.read` |
| Update the minification settings | `update_minify` | `PUT /v1/{crn}/zones/{domain_id}/setting/minify` | `internet-svcs.performance.update` | `internet-svcs.minify-setting.update` |
| Get the minimum TLS version settings | `get_min_tls_version` | `GET /v1/{crn}/zones/{domain_id}/setting/min_tls_version` | `internet-svcs.security.read` | `internet-svcs.min-tls-version-setting.read` |
| Update the minimum TLS version settings | `update_min_tls_version` | `PUT /v1/{crn}/zones/{domain_id}/setting/min_tls_version` | `internet-svcs.security.update` | `internet-svcs.min-tls-version-setting.update` |
| Get the IP geolocation settings | `get_ip_geolocation` | `GET /v1/{crn}/zones/{domain_id}/setting/ip_geolocation` | `internet-svcs.zones.read` | `internet-svcs.ip-geolocation-setting.read` |
| Update the IP geolocation settings | `update_ip_geolocation` | `PUT /v1/{crn}/zones/{domain_id}/setting/ip_geolocation` | `internet-svcs.zones.update` | `internet-svcs.ip-geolocation-setting.update` |
| Get the server-side exclude settings | `get_server_side_exclude` | `GET /v1/{crn}/zones/{domain_id}/setting/server_side_exclude` | `internet-svcs.security.read` | `internet-svcs.server-side-exclude-setting.read` |
| Update the server-side exclude settings | `update_server_side_exclude` | `PUT /v1/{crn}/zones/{domain_id}/setting/server_side_exclude` | `internet-svcs.security.update` | `internet-svcs.server-side-exclude-setting.update` |
| Get the security header settings | `get_security_header` | `GET /v1/{crn}/zones/{domain_id}/setting/security_header` | `internet-svcs.security.read` | `internet-svcs.security-header-setting.read` |
| Update the security header settings | `update_security_header` | `PUT /v1/{crn}/zones/{domain_id}/setting/security_header` | `internet-svcs.security.update` | `internet-svcs.security-header-setting.update` |
| Get the mobile redirect settings | `get_mobile_redirect` | `GET /v1/{crn}/zones/{domain_id}/setting/mobile_redirect` | `internet-svcs.performance.read` | `internet-svcs.mobile-redirect-setting.read` |
| Update the mobile redirect settings | `update_mobile_redirect` | `PUT /v1/{crn}/zones/{domain_id}/setting/mobile_redirect` | `internet-svcs.performance.update` | `internet-svcs.mobile-redirect-setting.update` |
| Get the prefetch / preload settings | `get_prefetch_preload` | `GET /v1/{crn}/zones/{domain_id}/setting/prefetch_preload` | `internet-svcs.performance.read` | `internet-svcs.prefetch-preload-setting.read` |
| Update the prefetch / preload settings | `update_prefetch_preload` | `PUT /v1/{crn}/zones/{domain_id}/setting/prefetch_preload` | `internet-svcs.performance.update` | `internet-svcs.prefetch-preload-setting.update` |
| Get the HTTP2 settings | `get_http2` | `GET /v1/{crn}/zones/{domain_id}/setting/http2` | `internet-svcs.security.read` | `internet-svcs.http2-setting.read` |
| Update the HTTP2 settings | `update_http2` | `PUT /v1/{crn}/zones/{domain_id}/setting/http2` | `internet-svcs.security.update` | `internet-svcs.http2-setting.update` |
| Get the IPv6 settings | `get_ipv6` | `GET /v1/{crn}/zones/{domain_id}/setting/ipv6` | `internet-svcs.zones.read` | `internet-svcs.ipv6-setting.read` |
| Update the IPv6 settings | `update_ipv6` | `PUT /v1/{crn}/zones/{domain_id}/setting/ipv6` | `internet-svcs.zones.update` | `internet-svcs.ipv6-setting.update` |
| Get the websocket settings | `get_websocket` | `GET /v1/{crn}/zones/{domain_id}/setting/websocket` | `internet-svcs.zones.read` | `internet-svcs.websockets-setting.read` |
| Update the websocket settings | `update_websocket` | `PUT /v1/{crn}/zones/{domain_id}/setting/websocket` | `internet-svcs.zones.update` | `internet-svcs.websockets-setting.update` |
| Get the response buffering settings | `get_response_buffering` | `GET /v1/{crn}/zones/{domain_id}/setting/response_buffering` | `internet-svcs.performance.read` | `internet-svcs.response-buffering-setting.read` |
| Update the response buffering settings | `update_response_buffering` | `PUT /v1/{crn}/zones/{domain_id}/setting/response_buffering` | `internet-svcs.performance.update` | `internet-svcs.response-buffering-setting.update` |
| Get the hotlink protection settings | `get_hotlink_protection` | `GET /v1/{crn}/zones/{domain_id}/setting/hotlink_protection` | `internet-svcs.performance.read` | `internet-svcs.hotlink-protection-setting.read` |
| Update the hotlink protection settings | `update_hotlink_protection` | `PUT /v1/{crn}/zones/{domain_id}/setting/hotlink_protection` | `internet-svcs.performance.update` | `internet-svcs.hotlink-protection-setting.update` |
| Get the maximum upload size settings | `get_max_upload` | `GET /v1/{crn}/zones/{domain_id}/setting/max_upload` | `internet-svcs.performance.read` | `internet-svcs.max-upload-setting.read` |
| Update the maximum upload size settings | `update_max_upload` | `PUT /v1/{crn}/zones/{domain_id}/setting/max_upload` | `internet-svcs.performance.update` | `internet-svcs.max-upload-setting.update` |
| Get the TLS client authentication settings | `get_tls_client_auth` | `GET /v1/{crn}/zones/{domain_id}/setting/tls_client_auth` | `internet-svcs.security.read` | `internet-svcs.tls-client-auth-setting.read` |
| Update the TLS client authentication settings | `update_tls_client_auth` | `PUT /v1/{crn}/zones/{domain_id}/setting/tls_client_auth` | `internet-svcs.security.update` | `internet-svcs.tls-client-auth-setting.update` |
| Get the pseudo IPv4 settings | `get_pseudo_ipv4` | `GET /v1/{crn}/zones/{domain_id}/setting/pseudo_ipv4` | `internet-svcs.zones.read` | `internet-svcs.pseudo-ipv4-setting.read` |
| Update the pseudo IPv4 settings | `update_pseudo_ipv4` | `PUT /v1/{crn}/zones/{domain_id}/setting/pseudo_ipv4` | `internet-svcs.zones.update` | `internet-svcs.pseudo-ipv4-setting.update` |
| Get the origin error page passthrough settings | `get_origin_error_page_pass_thru` | `GET /v1/{crn}/zones/{domain_id}/setting/origin_error_page_pass_thru` | `internet-svcs.zones.read` | `internet-svcs.origin-error-page-pass-thru-setting.read` |
| Update the origin error page passthrough settings | `update_origin_error_page_pass_thru` | `PUT /v1/{crn}/zones/{domain_id}/setting/origin_error_page_pass_thru` | `internet-svcs.zones.update` | `internet-svcs.origin-error-page-pass-thru-setting.update` |
| Get the brotli compression settings | `get_brotli` | `GET /v1/{crn}/zones/{domain_id}/setting/brotli` | `internet-svcs.performance.read` | `internet-svcs.brotli-setting.read` |
| Update the brotli compression settings | `update_brotli` | `PUT /v1/{crn}/zones/{domain_id}/setting/brotli` | `internet-svcs.performance.update` | `internet-svcs.brotli-setting.update` |
| Get the email obfuscation settings | `get_email_obfuscation` | `GET /v1/{crn}/zones/{domain_id}/setting/email_obfuscation` | `internet-svcs.security.read` | `internet-svcs.email-obfuscation-setting.read` |
| Update the email obfuscation settings | `update_email_obfuscation` | `PUT /v1/{crn}/zones/{domain_id}/setting/email_obfuscation` | `internet-svcs.security.update` | `internet-svcs.email-obfuscation-setting.update` |
| Get the ciphers settings | `get_ciphers` | `GET /v1/{crn}/zones/{domain_id}/setting/ciphers` | `internet-svcs.security.read` | `internet-svcs.ciphers-setting.read` |
| Update the ciphers settings | `update_ciphers` | `PUT /v1/{crn}/zones/{domain_id}/setting/ciphers` | `internet-svcs.security.update` | `internet-svcs.ciphers-setting.update` |
{: caption="Domain settings" caption-side="bottom"}
