---

copyright:
  years: 2018, 2025
lastupdated: "2025-12-30"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# FAQ for {{site.data.keyword.cis_full_notm}}
{: #faq}

Have a question about {{site.data.keyword.cis_full}}? Review these frequently asked questions, which provide answers to provisioning concerns, application access, and other common inquiries.

If you have additional questions you'd like to see addressed here, open an issue by using the **Open doc issue** or **Edit topic** links at the end of this page.

## What do I get with a Free Trial Plan?
{: #cis-faq-free-trial-plan}
{: faq}

The Free Trial plan, by design, allows only one zone per account. It is recommended that you create only one instance per account and that you verify the zone name. It is critical that the zone name be verified before it is added. If a zone is deleted, another zone or the same zone can't be added during the Free Trial Plan.

## How many Free Trial instances can I have?
{: #cis-faq-free-trial-instances}
{: faq}

You can have, at most, one Free Trial instance per account, for the lifetime of the account. If you already have a free trial instance, if you delete a free trial instance, or if the free trial expires, you are not allowed to create another free trial instance. However, you can create instances of other paid plan types, independent of any free trials you might have created.

## Can I downgrade from Standard Next to the Free Trial?
{: #cis-faq-downgrade-standard-to-free-plan}
{: faq}

No. Downgrading from Standard Next to a Free Trial plan is not allowed.

## My Free Trial expired. What are my options?
{: #cis-faq-free-trial-plan-expired}
{: faq}

To avoid any data loss, you must upgrade from Free Trial to Standard before the expiration date. After that expiration, you can only upgrade the plan or delete the CIS instance. If the instance is not deleted or upgraded after 45 days (from the initiation of the instance) the configuration domain, global load balancers, pools, and health checks are deleted automatically.

## What happened to Enterprise Package plans?
{: #enterprise-package-expiration}
{: faq}

Starting on 11 August 2023, you can no longer configure the Enterprise Package plan. The functionality of this plan was split across various tiers and are now available in Enterprise Essential, Enterprise Advanced, and Enterprise Premier plans. See [Transition updated plans](/docs/cis?topic=cis-transition-plans).

## I added a user to my account and gave that user permission to manage Internet Services instances. Why does that user have authentication issues?
{: #cis-faq-user-authentication-issue}
{: faq}

It's possible that you did not assign "service access roles" to the user. Note the two separate sets of roles:

* Platform access
* Service access

You need platform access roles to create and manage service instances, while service access roles perform service-specific operations on service instances. In the console, these settings can be updated by selecting **Manage > Security > Identity and Access**.

## Why is my domain in Pending state? How do I activate it?
{: #cis-faq-pending-domain}
{: faq}

When you add a domain to CIS, you are given some name servers to configure at your registrar (or at your DNS provider, if you are adding a subdomain). The domain or subdomain remains in pending state until you configure the name servers correctly. Make sure you add both the name servers to your registrar or DNS provider. CIS periodically scans the public DNS system to check whether the name servers were configured as instructed. As soon as CIS can verify the name server change (which can take up to 24 hours), your domain is activated. You can submit a request to recheck name servers by clicking **Recheck name servers** in the overview page.

## Who is the registrar for my domain?
{: #cis-faq-who-is-registrar}
{: faq}

Consult https://whois.icann.org/ for this information.

To add your domain to CIS, you must have administrator privilege to edit the domain's configuration at the registrar to update or add the name servers for your domain. If you don't know who the registrar is for the domain you're trying to add to CIS, it is unlikely you have the administrator privilege. Work with the owner of the domain in your organization to make the necessary changes.
{: note}

## I want to keep my current DNS provider for my domain (`example.com`). Can I delegate a subdomain (`subdomain.example.com`) from my current DNS provider to {{site.data.keyword.cis_short_notm}}?
{: #cis-faq-keep-current-dns-provider}
{: faq}

Yes. The process is similar to adding a domain, but instead of the registrar, you work with the DNS provider for the higher-level domain. When you add a subdomain to {{site.data.keyword.cis_short_notm}}, you are given two name servers to configure, as usual. You configure a name server (NS) record for each of the two name servers as DNS records within your domain that is being managed by the other DNS provider. When {{site.data.keyword.cis_short_notm}} is able to verify that the required NS records have been added, {{site.data.keyword.cis_short_notm}} activates your subdomain. If you do not manage the higher-level domain within your organization, you must work with the owner of the higher-level domain to get the NS records added.

## I want onboard my domain to {{site.data.keyword.cis_short_notm}} while still maintaining its current primary and authoritative DNS provider. Is this possible?
{: #cis-faq-cname-setup}
{: faq}

Yes. {{site.data.keyword.cis_short_notm}} supports a [CNAME (partial)](/docs/cis?topic=cis-cname-setup) configuration. This option allows you to proxy only individual domains through {{site.data.keyword.cis_short_notm}}’s global network in the scenario where you can't change your authoritative DNS provider. Once you are on a partial setup, the actual resolution of your records to {{site.data.keyword.cis_short_notm}} depends on CNAME records added at your authoritative DNS provider. Keep in mind that CIS resolves DNS records differently in a partial setup.

## What are the defaults for DNS TTL?
{: #cis-faq-dnsttl-defaults}
{: faq}

The following are defaults for DNS time-to-live (TTL), in seconds.
* For records such as A records and CNAMEs, the automatic TTL is 300s.

## Why do I see a privacy warning?
{: #cis-faq-privacy-warning}
{: faq}

The TLS certificates issued by IBM Cloud CIS cover the root domain (`example.com`) and one level of subdomain (`*.example.com`). If you’re trying to reach a second-level subdomain (`*.*.example.com`) a privacy warning appears in your browser, because these host names are not added to the SAN.

Allow up to 15 minutes for one of our partner Certificates Authorities (CAs) to issue a new certificate. A privacy warning appears in your browser if your new certificate has not yet been issued.

## Why do I see invalid SSL certificate error?
{: #cis-faq-invalid-ssl-cert-error}
{: faq}

If you see "Error 526, Invalid SSL Certificate" when visiting your site, it might mean your origin certificate is invalid. When the CIS proxy is enabled, a valid CA-signed certificate is required at the origin in the default SSL mode, which is "End-to-end CA Signed". Note that the default setting for the SSL mode was previously "End-to-end Flexible", which ignores the validity of certificates presented by the origin. The new default is applied only to newly added domains. If your domain was added when the default SSL mode was End-to-end Flexible, that setting is not overwritten. You can change the mode to a less strict mode, but that is not recommended for production environments.

## What is DDoS?
{: #cis-faq-what-is-ddos}
{: faq}

A distributed denial-of-service (DDoS) attack is an attempt to make an online service unavailable by overwhelming it with traffic from multiple sources. In a DDoS attack, multiple compromised computer systems attack a target such as a server, website, or other network resource, affecting users of the targeted resource.

The flood of incoming messages, connection requests, or malformed packets to the target system forces it to slow down or even crash and shut down, thereby denying service to legitimate users or systems. DDoS attacks have been carried out by diverse threat actors, ranging from individual criminal hackers to organized crime rings and government agencies.

## What do I do if I’m under a DDoS attack?
{: #cis-faq-what-to-do-in-ddos}
{: faq}

**Step 1:** Turn on “Defense mode" in the **Overview** page.

**Step 2:** Set your DNS records for maximum security.

**Step 3:** Do not rate-limit or throttle requests from IBM CIS, we need the bandwidth to assist you with your situation.

**Step 4:** Block specific countries and visitors, if necessary.

## I got a 522 error, what do I do now?
{: #cis-faq-522-error}
{: faq}

A 522 error indicates we weren't able to establish a connection with your origin server (that is, your host). After about 15 seconds of connection failure, we close the connection and display a 522 error page.

This issue usually is caused by firewall or security software that accidentally blocks our IP addresses. Because CIS acts as a reverse proxy, connections to your site appear to come from a range of CIS IPs. This behavior can cause certain firewalls to block these connections, which prevents us from serving content to your site visitors properly.

To fix this issue, ask your host to allowlist all of the CIS IP ranges, listed in the [CIS allowlisted IP addresses](/docs/cis?topic=cis-cis-allowlisted-ip-addresses) page.

All of these IPs must be allowlisted to avoid 522 errors. It's also worth checking to see if any IPs in these ranges are blocked.

522 errors can also be caused by network connectivity issues, so confirm that your server and network is generally healthy and not overloaded.

If after taking the above steps you still receive errors, contact IBM CIS support and confirm the following:

* You've allowlisted our IP ranges
* Your server/network is online and generally healthy

If you contact our support team, provide a Ray ID from a recent 522 error. We can use this to determine which CIS data center you were hitting and run further tests.

## What is a proxied record and why do I need them?
{: #cis-faq-proxied-record}
{: faq}

Proxied records are records that proxy their traffic through IBM CIS. Only proxied records receive CIS benefits, such as IP masking, where a CIS IP is substituted for your origin IP to protect it:

```sh
$ whois 104.28.22.57 | grep OrgName
OrgName:        IBM
```
{: pre}

If you would rather bypass CIS on a domain (we still resolve DNS), then non-proxying the record is a possible solution.

## I got a DNS Validation error: 1004; now what can I do?
{: #cis-faq-dns-validation-error}
{: faq}

For page rules to work, DNS needs to resolve for your zone. As a result, you must have a proxied DNS record for your zone.

## Can I add a CNAME for a root record?
{: #cis-faq-add-cname-root-record}
{: faq}

Yes. IBM CIS supports a feature called "CNAME Flattening" which allows our users to add a CNAME as a root record. Our authoritative DNS servers enumerate the CNAME target's records and respond with those records instead of the CNAME itself, effectively hiding the fact that the user configured a CNAME at the root of the domain.

## What is the default health check timeout?
{: #cis-faq-default-health-check-timeout}
{: faq}

The default health check timeout for the Free Trial and Standard plans is 60 seconds.

## Can health checks be configured for non-HTTP/HTTPS traffic?
{: #cis-faq-health-check-non-http-traffic}
{: faq}

No, health checks can only be configured with HTTP/HTTPS.

## Can global load balancers be configured for non-HTTP/HTTPS traffic?
{: #cis-faq-glb-non-http-traffic}
{: faq}

No, global load balancers can only be configured with HTTP/HTTPS.

## Does disabling all of my origins in an origin pool disable the entire pool itself?
{: #cis-faq-disabling-origins-disable-origin-pool}
{: faq}

Yes, if the origin pool is being used in a load balancer, the traffic is routed to the next highest priority pool or the fallback pool.

## I have an error in my Kubernetes Ingress, what do I do?
{: #cis-faq-kubernetes-ingress-error}
{: faq}

The hostname in a Kubernetes ingress must consist of lower case alphanumeric characters, `-` or `.`, and must start and end with an alphanumeric character. Using `_` in the load balancer name, though permitted, can cause an ingress error in Kubernetes clusters. We recommend that you not use `-` in the load balancer name to avoid issues with Kubernetes clusters.

## I got a 502 error attempting to save an Edge Functions Action, what do I do?
{: #cis-faq-502-error}
{: faq}

Contact [IBM support](/docs/cis?topic=cis-gettinghelp) and provide the script that you were attempting to save.

## How do I find my service instance ID?
{: #cis-faq-service-instance-id}
{: faq}

To find your service instance ID, copy the CRN on the overview page. For example:

```sh
crn:v1:test:public:internet-svcs:global:a/2c38d9a9913332006a27665dab3d26e8:836f33a5-d3e1-4bc6-876a-982a8668b1bb::
```
{: pre}

The last part of the CRN is your service instance: `836f33a5-d3e1-4bc6-876a-982a8668b1bb`.

Alternatively, you can click the row containing the {{site.data.keyword.cis_short_notm}} instance on the resource list main page and copy the GUID for the service instance ID.

## Does {{site.data.keyword.cis_short_notm}} compress resources?
{: #cis-compress-resources}
{: faq}

Yes, {{site.data.keyword.cis_short_notm}} applies "gzip" and "brotli" compression to some types of content. {{site.data.keyword.cis_short_notm}} also compresses items based on the browser's UserAgent to speed up page loading time.

If you're already using gzip {{site.data.keyword.cis_short_notm}} honors your gzip settings as long as you're passing the details in a header from your web server for the files.

{{site.data.keyword.cis_short_notm}} only supports the content type "gzip" towards your origin server and can also only deliver content either gzip-compressed, brotli-compressed, or not compressed.

{{site.data.keyword.cis_short_notm}}'s reverse proxy is also able to convert between compressed formats and uncompressed formats, meaning that it can pull content from a customer's origin server via gzip and serve it to clients uncompressed (or vice versa). This is done independently of caching.

The Accept-Encoding header is not respected and is removed.
{: note}

## How many requests can I make to the {{site.data.keyword.cis_short_notm}} API?
{: #request-limit-api}
{: faq}

The global rate limit for the {{site.data.keyword.cis_short_notm}} API is 1200 requests per five minutes per user, and applies cumulatively regardless of whether the request is made through the UI, CLI, Terraform, or API.

## Can I use {{site.data.keyword.cis_short_notm}} with private IPs?
{: #can-i-use-private-ips}
{: faq}

Private IPs (RFC1918) can be reached with DNS lookup through the non-proxied {{site.data.keyword.cis_short_notm}} setup. However, you can't access most of {{site.data.keyword.cis_short_notm}}'s advanced features such as CDN and WAF with this setup. For private IPs, {{site.data.keyword.cis_short_notm}} handles Name-to-Address translation only. Connectivity to the private network is the responsibility of the customer.

## What port range does Cloudflare's network use for the edge traffic?
{: #port-range-edge-traffic}

When the proxy is enabled, traffic is routed through the Cloudflare network to the origin server. This traffic can originate from any port within the range of `1024-65535`. When configuring Network Access Control Lists (ACLs) for your environment, ensure that both ingress and egress traffic from this port range is allowed.

## How does CIS handle clock synchronization?
{: #clock-synchronization}

To meet ISO 27001 requirements, all relevant systems must synchronize with a unified time source.
IBM {{site.data.keyword.cis_short_notm}} ensures clock synchronization across its infrastructure by using Network Time Protocol (NTP) servers. {{site.data.keyword.cis_short_notm}} uses the following internal NTP servers:

* `time.adn.networklayer.com`
* `time.service.networklayer.com`

## How does CIS handle traffic scrubbing?
{: #traffic-scrubbing}

{{site.data.keyword.cis_short_notm}} uses its 388 Tbps global edge network to mitigate high-volume DDoS attacks without scrubbing centers. Attacks are analyzed and blocked at the edge, near the source. Only protected traffic (clean requests and responses) is billed. Malicious traffic is excluded.

## What network does CIS use for global traffic and health checks?
{: #anycast-network}

{{site.data.keyword.cis_short_notm}} runs its data plane on Cloudflare’s global Anycast network, which spans hundreds of cities worldwide. This network ensures fast, reliable traffic routing and DDoS mitigation.

Health check requests originate from this distributed network, so the available regions for health checks are based on the [Cloudflare Global Anycast Network](https://www.cloudflare.com/network/){: external}.

## How does CIS provide cost protection?
{: #cost-protection}

{{site.data.keyword.cis_short_notm}} does not meter or bill for traffic that is blocked as part of DDoS mitigation, firewall, or rate limiting. Only requests that are passed through the {{site.data.keyword.cis_short_notm}} network to the origin destination incur charges or usage.

{{site.data.keyword.cis_short_notm}} also helps keep egress bandwidth charges from your origin under control by only passing along good requests that the origin needs to respond to. All {{site.data.keyword.cis_short_notm}} plans offer unlimited and unmetered mitigation of DDoS attacks. You are never charged for attack traffic, and there’s no penalty or chargeback for traffic spikes caused by attacks.

## Does CIS support outbound traffic filtering?
{: #outbound-traffic-filtering}

No. CIS is designed to secure inbound traffic to your IBM Cloud applications. It doesn't inspect, log, or filter outbound traffic from cloud resources, such as virtual server instances, containers, or VPC resources.

CIS acts as a reverse proxy to protect traffic coming into your applications. CIS doesn't function as a forward proxy or egress filter.
{: note}

For outbound traffic control, consider:

- [VPC Security Groups](/docs/vpc?topic=vpc-using-security-groups)  – Control outbound ports/IPs at the instance level.
- [VPC Network ACLs (NACLs)](/docs/vpc?topic=vpc-using-acls)– Subnet-level inbound/outbound rules.
- **Firewall appliances** – Deploy third-party firewalls within your VPC.
- **DNS filtering** – Use DNS-based services to restrict domains.

## What changed in the WAF payload limit and why is the payload limit increasing?
{: #waf-traffic-limit}
 
For all plans, CIS Web Application Firewall (WAF) inspects request payloads up to 1 MB. This helps the WAF to detect more complex threats that appear in larger request bodies.
