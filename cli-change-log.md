---

copyright:
  years:  2024, 2025
lastupdated: "2025-06-25"

keywords: change log for cis cli, updates to cis-cli-plugin

subcollection: cis

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}


# {{site.data.keyword.cis_short_notm}} CLI change log
{: #cli-change-log}

In this change log, you can learn about the latest changes, improvements, and updates for the {{site.data.keyword.cis_full_notm}} CLI.
{: shortdesc}

## Version 1.16.4
{: #cli-1164}

Version 1.16.4 of the CLI was released on April 7, 2025.
:   Add [WAF managed rules](/docs/cis?topic=cis-cis-cli#waf-managed-rules).
:   Add [WAF custom rules](/docs/cis?topic=cis-cis-cli#waf-custom-rules). 

## Version 1.16.3
{: #cli-1163}

Version 1.16.3 of the CLI was released on July 19, 2024.
:   Fix CVE certifi.
:   Add `replace_insecure_js` domain setting.
:   Fix managed rules and advanced rate-limiting rule bugs.
:   CLI GVT translation.
:   Update the dependency `requests` to v2.32.3.

## Version 1.16.2
{: #cli-1162}

Version 1.16.2 of the CLI was released on June 13, 2024.
:   Support Advanced rate-limiting rules.
:   Update the description of listing dns record per page.

## Version 1.16.1
{: #cli-1161}

Version 1.16.1 of the CLI was released on May 11, 2024.
:   Fix WAF overrides list and domain settings issue.
:   Display WAF migration notice.

## Version 1.16.0
{: #cli-1160}

Version 1.16.0 of the CLI was released on May 6, 2024.
:   Support managed WAF rules.

## Version 1.15.13
{: #cli-11513}

Version 1.15.13 of the CLI was released on Apr 12, 2024.
:   Add Origin max HTTP version support.
:   Add origin post quantum encryption support.

## Version 1.15.12
{: #cli-11512}

Version 1.15.12 of the CLI was released on Mar 22, 2024.
:   Enhance the custom certificates.
:   Go modules upgrade.

## Version 1.15.11
{: #cli-11511}

Version 1.15.11 of the CLI was released on Feb 28, 2024.
:   Fix listing certificate issue.

## Version 1.15.10
{: #cli-11510}

Version 1.15.10 of the CLI was released on Feb 1, 2024.
:   Support HTTP origin alert policy.

## Version 1.15.8
{: #cli-1158}

Version 1.15.8 of the CLI was released on Jan 11, 2023.
:   fix bug of deleting filter and firewall rules.
:   gvt translation.
:   Update go to v20.

## Version 1.15.7
{: #cli-1157}

Version 1.15.7 of the CLI was released on Nov 8, 2023.
:   Support ddos `L3/L4` alerting policy.
:   Support mtls certificate expiration alerting policy.
:   Failing Logpush job disabled alerting policy.
:   Fix bot metrics issue.

## Version 1.15.6
{: #cli-1156}

Version 1.15.6 of the CLI was released on Oct 16, 2023.
:   Support instant logs.

## Version 1.15.5
{: #cli-1155}

Version 1.15.5 of the CLI was released on Sep 7, 2023.
:   Support alert policy test.
:   Support maintenance event alert policy.
:   Bug fix: certificate deletion issue.

## Version 1.15.4
{: #cli-1154}

Version 1.15.4 of the CLI was released on Aug 29, 2023.
:   Support `dns_logs` dataset for logpush job.
:   Update security fields for logpull.
:   Support Web analytic report alert policy.

## Version 1.15.3
{: #cli-1153}

Version 1.15.3 of the CLI was released on Jul 23, 2023.
:   Support `linux/arm64` binary.

## Version 1.15.2
{: #cli-1152}

Version 1.15.2 of the CLI was released on June 6, 2023.
:   Support Zone hold.
:   Support Image Resizing.
:   Fix bugs of alerts.

## Version 1.15.0
{: #cli-1150}

Version 1.15.0 of the CLI was released on Apr 24, 2023.
:   Enterprise 2.0 plan support.
:   Bot management support.
:   FVT/GVT.

## Version 1.14.11
{: #cli-11411}

Version 1.14.11 of the CLI was released on 16 March 2023.
:   Unhide standard plan.

## Version 1.14.10
{: #cli-11410}

Version 1.14.10 of the CLI was released on 2 March 2023.
:   Add URL normalization for domain setting.
:   Add certificate authority options.
:   Add universal CA options.
:   Add binary M1 and s390x support.
:   Fix origin certificate list issue.
:   Upgrade go dependency package versions.
:   Unhide the standard plan for 45 days.

## Version 1.14.9
{: #cli-1149}

Version 1.14.9 of the CLI was released on 27 October 2022.
:   Add authenticated origin pull list.
:   Enhance certificates order.
:   Add `probe_zone` option for the GLB monitor.

## Version 1.14.8
{: #cli-1148}

Version 1.14.8 of the CLI was released on 26 August 2022.
:   Add new alert policies.
:   Enable Domain CNAME setup.
:   Extend rate limit threshold range.

## Version 1.14.5
{: #cli-1145}

Version 1.14.5 of the CLI was released on 09 August 2022.
:   Fix edge functions trigger.
:   Fix cross account resource access.
:   Add `ppc64le` binary release.
:   Page rule action remove always online.

## Version 1.14.4
{: #cli-1144}

Version 1.14.4 of the CLI was released on 23 March 2022.
:   Add customer cert type.
:   Add domain security level setting.
:   Deprecate edge trigger disable option.
:   Support onion routing.

## Version 1.14.3
{: #cli-1143}

Version 1.14.3 of the CLI was released on 8 March 2022.
:   Add session affinity attributes.

## Version 1.14.2
{: #cli-1142}

Version 1.14.2 of the CLI was released on 1 March 2022.
:   Added Log Analysis instance support to the CLI for creating and configuring Logpush jobs.
:   Allow short aliases name `cis` for plugin `install/upgrade/delete`.
