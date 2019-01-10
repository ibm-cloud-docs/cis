---

copyright:
  years: 2018
lastupdated: "2019-01-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# CIS Command Line Interface
The following families of commands are available from the command line interface (CLI) in CIS. At these links, you'll find the full set of commands within each set, including `Create`, `Delete`, `Update`, and so forth.
  
  * [Resource Instance](cli/cli-resource-instance.html)
  * [Domain](cli/cli-domain.html)
  * [DNS Record](cli/cli-dns-record.html)
  * [GLB](cli/cli-glb.html)
  * [Cache](cli/cli-cache.html)
  * [TLS](cli/cli-tls.html)
  * [WAF](cli/cli-waf.html)
  * [Pagerule](cli/cli-pagerule.html)
  * [Firewall](cli/cli-firewall.html)
  * [Metrics](cli/cli-metrics.html)
  * [Routing](cli/cli-routing.html)
  * [RateLimit](cli/cli-ratelimit.html)
  * [Overview](#the-overview-command-definition)
  * [Log](cli/cli-log.md)

The CIS CLI documentation is shown in modified `man` page format. The `overview` command also is one of the CLI commands available to you. It just happens to make a good example as well, so we included it here.

## The Overview command definition

**NAME**

  `cloud-internet-services overview` - Show the overview information for an instance. 

**USAGE**

  `ibmcloud cis overview DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [--output FORMAT]`

**OPTIONS**

 `-i, --instance INSTANCE_NAME`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
 `--output FORMAT`    Specify output format, only JSON is supported now.


**Output messages**

  * Service Mode
  * Service Details
    *  Domain Name
    * Status
    * ID
    * Service Plan

  * Security
    * Web Application Firewall
    * TLS Mode
    * Dedicated Certificates
    * Custom Certificates

  * Performance 
    * Page Rules
    * Browser Expiration
    * Caching Level

  * Reliability:
    * DNS Records
    * DNS Security
    * Load Balancers
              
`Service Mode` is displayed only when the domain is paused or in defense mode.
