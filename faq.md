---

copyright:
  years: 2018, 2026
lastupdated: "2026-04-06"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# FAQ for {{site.data.keyword.cis_full_notm}}
{: #faq}

Have a question about {{site.data.keyword.cis_full}}? Review these frequently asked questions, which provide answers to provisioning concerns, application access, and other common inquiries.

If you have additional questions you'd like to see addressed here, open an issue by using the **Open doc issue** or **Edit topic** links at the end of this page.

## Plans, trials, and billing
{: #faq-plans-trials-billing}

### What is included in the Free Trial plan?
{: #cis-faq-free-trial-plan}
{: faq}

The Free Trial plan allows one zone per account. You should create only one instance and verify the zone name before adding it. The zone name must be verified before it is accepted. If you delete a zone during the Free Trial period, you cannot add the same zone or a different zone again under the Free Trial plan.

### How many Free Trial instances are allowed per account?
{: #cis-faq-free-trial-instances}
{: faq}

Only one Free Trial instance is allowed per account for the lifetime of the account. If you create a Free Trial instance, whether you delete it or allow it to expire, you cannot create another Free Trial instance. However, you can create instances under paid plans at any time.

### Can Standard Next be downgraded to the Free Trial plan?
{: #cis-faq-downgrade-standard-to-free-plan}
{: faq}

No. Downgrading from Standard Next plan to a Free Trial plan is not supported. You can't downgrade any plan to the Free Trial plan.

### What happens when a Free Trial plan expires?
{: #cis-faq-free-trial-plan-expired}
{: faq}

To avoid data loss, upgrade the instance to a paid plan before the expiration date. After expiration, you can either upgrade the plan or delete the instance. If the instance is not upgraded or deleted within 45 days of creation, {{site.data.keyword.cis_short_notm}} automatically deletes:

* The configuration domain
* Global load balancers
* Origin pools
* Health checks

### What happened to the Enterprise Package plan?
{: #enterprise-package-expiration}
{: faq}

As of 11 August 2023, the Enterprise Package plan was discontinued. The functionality of this plan was split across various tiers and is now available in Enterprise Essential, Enterprise Advanced, and Enterprise Premier plans. For more information, see [Transition updated plans](/docs/cis?topic=cis-transition-plans).

### Is DDoS attack traffic billed?
{: #traffic-ddos-charge}
{: faq}

No. {{site.data.keyword.cis_short_notm}} provides unlimited and unmetered DDoS protection. Traffic identified as part of a DDoS attack is excluded from billing. There are no limits on the size, duration, or number of identified attacks.

### How does {{site.data.keyword.cis_short_notm}} protect against unexpected billing charges?
{: #cost-protection}
{: faq}

{{site.data.keyword.cis_short_notm}} does not meter or bill for traffic that is blocked by DDoS mitigation, firewall, or rate limiting. Only traffic that passes through {{site.data.keyword.cis_short_notm}} and reaches the origin is counted for usage or billing.

{{site.data.keyword.cis_short_notm}} also helps keep egress bandwidth charges from your origin under control by only passing along good requests that the origin needs to respond to. All {{site.data.keyword.cis_short_notm}} plans offer unlimited and unmetered mitigation of DDoS attacks. You are never charged for attack traffic, and there’s no penalty or chargeback for traffic spikes caused by attacks.

## Account and access management
{: #faq-account-access-management}

### Why does a user receive authentication errors after being granted access?
{: #cis-faq-user-authentication-issue}
{: faq}

Authentication errors usually occur because the user was not assigned the required service access roles. {{site.data.keyword.cis_short_notm}} uses two types of roles:

* Platform access: Allow users to create and manage service instances.
* Service access: Allow users to perform service-specific operations within an instance.

Both role types must be assigned as appropriate for the user’s responsibilities. To update roles in the console, go to **Manage > Security > Identity and Access**.

### How do I find the service instance ID?
{: #cis-faq-service-instance-id}
{: faq}

To find your service instance ID, copy the CRN on the Overview page. For example:

```sh
crn:v1:test:public:internet-svcs:global:a/2c38d9a9913332006a27665dab3d26e8:836f33a5-d3e1-4bc6-876a-982a8668b1bb::
```
{: pre}

The last part of the CRN is your service instance: `836f33a5-d3e1-4bc6-876a-982a8668b1bb`.

Alternatively, you can click the row containing the {{site.data.keyword.cis_short_notm}} instance on the resource list main page and copy the GUID for the service instance ID.

## Domain onboarding and DNS setup
{: #faq-domain-onboarding-dns-setup}

### Why is my domain in Pending state, and how do I activate it?
{: #cis-faq-pending-domain}
{: faq}

A domain remains in `Pending` status until the required name server (NS) records are correctly configured.

When you add a domain (or subdomain) to {{site.data.keyword.cis_short_notm}}, you are provided with two {{site.data.keyword.cis_short_notm}} name servers. You must configure both name servers in one of the following locations:

* At your domain registrar (when adding a domain)
* At your existing DNS provider (when adding a subdomain)

{{site.data.keyword.cis_short_notm}} periodically checks public DNS for the required NS records. After the name server change is detected (which can take up to 24 hours), the domain status changes to `Active`.
You can manually trigger a check by selecting **Recheck name servers** on the Overview page.

### How do I identify my domain registrar?
{: #cis-faq-who-is-registrar}
{: faq}

You can look up your domain registrar using the ICANN WHOIS tool: [https://whois.icann.org/](https://whois.icann.org){: external}

To add your domain to {{site.data.keyword.cis_short_notm}}, you must have administrator privilege to edit the domain's configuration at the registrar to update or add the name servers for your domain. If you don't know who the registrar is for the domain you're trying to add to {{site.data.keyword.cis_short_notm}}, it is unlikely you have the administrator privilege. Work with the owner of the domain in your organization to make the necessary changes.
{: note}

### Can I delegate a subdomain to {{site.data.keyword.cis_short_notm}} while keeping my current DNS provider?
{: #cis-faq-keep-current-dns-provider}
{: faq}

Yes. You can delegate a subdomain to {{site.data.keyword.cis_short_notm}} without changing the authoritative DNS provider for the parent domain.

When you add the subdomain to {{site.data.keyword.cis_short_notm}}, you receive two {{site.data.keyword.cis_short_notm}} name servers. Create NS records for the subdomain at your existing DNS provider that point to those {{site.data.keyword.cis_short_notm}} name servers.
After the NS records are publicly visible and verified, {{site.data.keyword.cis_short_notm}} activates the subdomain. If you do not manage the parent domain, work with the domain owner to add the required NS records.

### Can I onboard a domain to {{site.data.keyword.cis_short_notm}} without changing the authoritative DNS provider?
{: #cis-faq-cname-setup}
{: faq}

Yes. {{site.data.keyword.cis_short_notm}} supports a [CNAME (partial)](/docs/cis?topic=cis-cname-setup) setup. This configuration allows you to proxy specific hostnames through the {{site.data.keyword.cis_short_notm}} network while keeping your existing authoritative DNS provider. In a partial setup:

* You create CNAME records at your authoritative DNS provider.
* Those CNAME records point to {{site.data.keyword.cis_short_notm}}.
* Only the specified hostnames are proxied.

DNS resolution behavior differs from a full name server setup.
{: note}

### What is the default DNS TTL value?
{: #cis-faq-dnsttl-defaults}
{: faq}

For A and CNAME records, the default automatic TTL is 300 seconds.

### Can I configure a CNAME at the root of my domain?
{: #cis-faq-add-cname-root-record}
{: faq}

Yes. {{site.data.keyword.cis_short_notm}} supports "CNAME Flattening," which allows you to configure a CNAME at the root (apex) of your domain. Instead of returning the CNAME record itself, {{site.data.keyword.cis_short_notm}} resolves the CNAME target and returns the corresponding A or AAAA records. This allows the root domain to behave like a CNAME without violating DNS standards.

### What is a proxied record, and when should I use one?
{: #cis-faq-proxied-record}
{: faq}

A proxied DNS record routes traffic through {{site.data.keyword.cis_short_notm}} before it reaches your origin server. Only proxied records receive {{site.data.keyword.cis_short_notm}} benefits, including IP masking, where a {{site.data.keyword.cis_short_notm}} IP is substituted for your origin IP to protect it:

```sh
$ whois 104.28.22.57 | grep OrgName
OrgName:        IBM
```
{: pre}

If you would rather bypass {{site.data.keyword.cis_short_notm}} on a domain (we still resolve DNS), then non-proxying the record is a possible solution.

### How do I resolve DNS validation error 1004?
{: #cis-faq-dns-validation-error}
{: faq}

For page rules to work, DNS needs to resolve for your zone. As a result, you must have a proxied DNS record for your zone.

### Can I use {{site.data.keyword.cis_short_notm}} with private (RFC1918) IP addresses?
{: #can-i-use-private-ips}
{: faq}

Yes, but with limitations. If you configure a non-proxied DNS record that points to a private (RFC1918) IP address:

* {{site.data.keyword.cis_short_notm}} performs DNS resolution only.
* Advanced features, such as CDN, WAF, and DDoS protection are not applied.

{{site.data.keyword.cis_short_notm}} does not provide connectivity to private networks. Network access to the private IP must be handled by your infrastructure.

## SSL/TLS and certificates
{: #faq-ssl-tls-certifications}

### Why do I see a browser privacy warning?
{: #cis-faq-privacy-warning}
{: faq}

The TLS certificates issued by IBM Cloud {{site.data.keyword.cis_short_notm}} cover the root domain (`example.com`) and one level of subdomain (`*.example.com`). If you’re trying to reach a second-level subdomain (`*.*.example.com`), a privacy warning appears in your browser, because these host names are not added to the SAN.

Allow up to 15 minutes for one of our partner Certificate Authorities (CAs) to issue a new certificate. A privacy warning appears in your browser if your new certificate has not yet been issued.

### How do I resolve error 526: Invalid SSL certificate?
{: #cis-faq-invalid-ssl-cert-error}
{: faq}

Error 526 indicates that the origin server is presenting an invalid or untrusted SSL/TLS certificate.

When the {{site.data.keyword.cis_short_notm}} proxy is enabled and the SSL mode is **End-to-end CA Signed** (default for new domains), the origin must present a valid certificate that is signed by a trusted certificate authority.

To resolve the error:

* Ensure the origin certificate is valid (not expired or self-signed).
* Verify that the certificate matches the hostname.
* Confirm the certificate chain is complete.
* Install a valid CA-signed certificate on the origin server.

If necessary, you can change the SSL mode to a less strict setting. However, this is not recommended for production environments because it reduces security.

### How does {{site.data.keyword.cis_short_notm}} mitigate SSL/TLS negotiation and handshake attacks?
{: #ddos-ssl-tls}
{: faq}

{{site.data.keyword.cis_short_notm}} mitigates SSL/TLS negotiation and handshake-based attacks by terminating TLS sessions at the edge network before traffic reaches the origin server. It enforces secure TLS settings and cipher suites to protect against known vulnerabilities such as BEAST, POODLE, and CRIME. {{site.data.keyword.cis_short_notm}} forwards traffic to the origin only after a successful TLS handshake, preventing TLS exhaustion attacks. Automated DDoS systems then analyze traffic patterns, cipher behavior, and request metadata to detect and block additional SSL/TLS based attacks.

## DDoS protection
{: #faq-ddos-protection}

### What is a distributed denial-of-service (DDoS) attack?
{: #cis-faq-what-is-ddos}
{: faq}

A distributed denial-of-service (DDoS) attack attempts to make an online service unavailable by overwhelming it with traffic from multiple sources.

Attackers use compromised systems to generate large volumes of traffic or malformed requests that:

* Exhaust server resources
* Disrupt network connectivity
* Prevent legitimate users from accessing the service

DDoS attacks can target applications (Layer 7), protocols (Layer 3/4), or network infrastructure.

### What are LOIC and HOIC attack tools?
{: #ddos-loic-hoic}
{: faq}

The Low Orbit Ion Cannon (LOIC) and High Orbit Ion Cannon (HOIC) are tools associated with DoS attacks and often referenced in discussions of Layer 7 DDoS mitigation.

LOIC generates large volumes of TCP, UDP, or HTTP requests to overwhelm a target. It is known for:

* Simple interface and low barrier to use
* High volumes of repetitive traffic
* Overwhelming smaller or poorly protected systems

HOIC is an evolution of LOIC, generating higher-volume, more flexible HTTP traffic, targeting multiple sites simultaneously, and supporting “boosters” to extend attack scope. This makes HOIC attacks harder for signature-based defenses to detect.

Both tools exploit network behaviors to cause denial of service. Use outside controlled testing environments is illegal and unethical. Organizations should rely on defenses such as rate limiting and managed DDoS protection.

### What should I do if I am under a DDoS attack?
{: #cis-faq-what-to-do-in-ddos}
{: faq}

If you suspect an active DDoS attack:

1. Enable “Defense mode" from the **Overview** page.
1. Set your DNS records for maximum security.
1. Do not rate-limit or throttle requests from {{site.data.keyword.cis_short_notm}}, IBM needs the bandwidth to assist you with your situation.
1. Block specific countries and visitors, if necessary.

These actions allow {{site.data.keyword.cis_short_notm}} to inspect, absorb, and mitigate attack traffic at the edge network.

### How does {{site.data.keyword.cis_short_notm}} protect against low-and-slow DDoS attacks?
{: #ddos-low-slow-attack}
{: faq}

{{site.data.keyword.cis_short_notm}} protects against low-and-slow attacks by acting as an HTTP reverse proxy in front of the origin. The proxy buffers and validates requests at the edge, waiting for a complete HTTP request before forwarding it. Slow, incomplete, or malformed requests are absorbed or dropped, and never reach the origin.

{{site.data.keyword.cis_short_notm}} also enforces timeouts and applies WAF and firewall checks without requiring a traffic threshold, preventing attacks, such as Slowloris and RUDY from exhausting server resources.

### Can I exclude specific user agents from HTTP DDoS mitigation?
{: #ddos-http-protection}
{: faq}

Yes, you can create a custom rule [override](/docs/cis?topic=cis-custom-rules-fields-and-expressions) and use the expression fields to match against HTTP requests with the `User-Agent` header. There are a variety of [fields](/docs/cis?topic=cis-custom-rules-fields-and-expressions#custom-rule-available-fields) that you can use.

You can then adjust the [sensitivity level](/docs/cis?topic=cis-http-ddos&interface=api#sensitivity-level) or [mitigation action](/docs/cis?topic=cis-http-ddos&interface=api#ddos-action).

Use this capability carefully to avoid weakening protection for legitimate traffic patterns.

### How does {{site.data.keyword.cis_short_notm}} handle traffic scrubbing?
{: #traffic-scrubbing}
{: faq}

{{site.data.keyword.cis_short_notm}} uses its 388 Tbps global edge network to mitigate high-volume DDoS attacks without scrubbing centers. Attacks are analyzed and blocked at the edge, near the source. Only protected traffic (clean requests and responses) is billed. Malicious traffic is excluded.

## Load balancing and health checks
{: #faq-load-balancing-health-checks}

### What is the default health check timeout value?
{: #cis-faq-default-health-check-timeout}
{: faq}

The default health check timeout for the Free Trial and Standard plans is 60 seconds.

### Can health checks be configured for non-HTTP/HTTPS traffic?
{: #cis-faq-health-check-non-http-traffic}
{: faq}

No, health checks only support HTTP/HTTPS.

### Can global load balancers be configured for non-HTTP/HTTPS protocols?
{: #cis-faq-glb-non-http-traffic}
{: faq}

No. Global load balancers only support HTTP/HTTPS.

### What happens if all origins in a pool are disabled?
{: #cis-faq-disabling-origins-disable-origin-pool}
{: faq}

Yes. If all origins in a pool are disabled, traffic is routed to the next-priority pool or fallback pool.

### Which network does {{site.data.keyword.cis_short_notm}} use for global traffic and health checks?
{: #anycast-network}
{: faq}

{{site.data.keyword.cis_short_notm}} runs its data plane on Cloudflare’s global Anycast network, which spans hundreds of cities worldwide. This network ensures fast, reliable traffic routing and DDoS mitigation.

Health check requests originate from this distributed network, so the available regions for health checks are based on the [Cloudflare Global Anycast Network](https://www.cloudflare.com/network/){: external}.

## Performance and optimization
{: #performance-optimization}

### Does {{site.data.keyword.cis_short_notm}} apply content compression (gzip or Brotli)?
{: #cis-compress-resources}
{: faq}

Yes. {{site.data.keyword.cis_short_notm}} applies gzip and Brotli compression to some content types and can compress items based on the browser’s User-Agent to improve page load times.

If your origin already uses gzip, {{site.data.keyword.cis_short_notm}} honors those settings when the web server includes them in headers.

{{site.data.keyword.cis_short_notm}} only supports gzip for origin content and delivers content as gzip, Brotli, or uncompressed. Its reverse proxy can convert between compressed and uncompressed formats independently of caching.

The `Accept-Encoding` header from the client is removed and not respected.

### What is the payload limit for WAF?
{: #waf-traffic-limit}
{: faq}

{{site.data.keyword.cis_short_notm}} Web Application Firewall (WAF) now inspects request payloads up to 1 MB for all plans. This allows the WAF to detect more complex threats that may appear in larger request bodies. For more information, see [Request body inspection limit](/docs/cis?topic=cis-managed-rules-overview#request-body-inspection-limit).

### What is the API rate limit for {{site.data.keyword.cis_short_notm}}?
{: #request-limit-api}
{: faq}

The global rate limit for the {{site.data.keyword.cis_short_notm}} API is 1200 requests per five minutes per user, across all interfaces (UI, CLI, Terraform, API).

## Networking and infrastructure
{: #networking-infrastructure}

### What port range is used for edge-to-origin traffic?
{: #port-range-edge-traffic}
{: faq}

When the proxy is enabled, traffic is routed through the Cloudflare network to the origin server. This traffic can originate from any port within the range of `1024-65535`. When configuring Network Access Control Lists (NACLs) for your environment, ensure that both ingress and egress traffic from this port range is allowed.

### How does {{site.data.keyword.cis_short_notm}} manage clock synchronization (NTP)?
{: #clock-synchronization}
{: faq}

To meet ISO 27001 requirements, all relevant systems must synchronize with a unified time source. IBM {{site.data.keyword.cis_short_notm}} ensures clock synchronization across its infrastructure by using Network Time Protocol (NTP) servers. {{site.data.keyword.cis_short_notm}} uses the following internal NTP servers:

* `time.adn.networklayer.com`
* `time.service.networklayer.com`

### Does {{site.data.keyword.cis_short_notm}} support outbound (egress) traffic filtering?
{: #outbound-traffic-filtering}
{: faq}

No. {{site.data.keyword.cis_short_notm}} secures inbound traffic only. It doesn't inspect, log, or filter outbound traffic from cloud resources, such as virtual server instances, containers, or VPC resources.

{{site.data.keyword.cis_short_notm}} acts as a reverse proxy to protect traffic coming into your applications. {{site.data.keyword.cis_short_notm}} doesn't function as a forward proxy or egress filter.
{: note}

For outbound traffic control, consider:

- [VPC Security Groups](/docs/vpc?topic=vpc-using-security-groups): Control outbound ports/IPs at the instance level.
- [VPC Network ACLs (NACLs)](/docs/vpc?topic=vpc-using-acls): Subnet-level inbound/outbound rules.
- Firewall appliances: Deploy third-party firewalls within your VPC.
- DNS filtering: Use DNS-based services to restrict domains.

### What is the CF-Connecting-IP header?
{: #cf-connecting-ip}

The `CF-Connecting-IP` header provides the original client IP address to the origin web server. CIS adds this header at the edge, and it is included only in requests that are forwarded from the CIS edge to the origin server. 

## Troubleshooting and error codes
{: #troubleshooting-error-codes}

### How do I resolve error 522 (connection timed out)?
{: #cis-faq-522-error}
{: faq}

A 522 error occurs when {{site.data.keyword.cis_short_notm}} cannot connect to your origin server. After ~15 seconds of failed connection, the request times out and the 522 page is displayed.

This usually happens if a firewall or security software blocks {{site.data.keyword.cis_short_notm}} IPs. Because {{site.data.keyword.cis_short_notm}} is a reverse proxy, connections appear to come from {{site.data.keyword.cis_short_notm}} IP ranges, which must be allowlisted. See the [{{site.data.keyword.cis_short_notm}} allowlisted IP addresses](/docs/cis?topic=cis-cis-allowlisted-ip-addresses) page.

Also check that your server and network are healthy and not overloaded.

If issues persist, contact IBM {{site.data.keyword.cis_short_notm}} support with a recent Ray ID and confirm that:

* All {{site.data.keyword.cis_short_notm}} IP ranges are allowlisted
* Your server/network is online and healthy

### How do I resolve a 502 error when saving an Edge Functions action?
{: #cis-faq-502-error}
{: faq}

Contact [IBM Support](/docs/cis?topic=cis-gettinghelp) and provide the script that you were attempting to save.

### How do I resolve a Kubernetes Ingress hostname validation error?
{: #cis-faq-kubernetes-ingress-error}
{: faq}

The hostname in a Kubernetes ingress must consist of lower case alphanumeric characters, `-` or `.`, and must start and end with an alphanumeric character. Using `_` in the load balancer name, though permitted, can cause an ingress error in Kubernetes clusters. Avoid the use of `-` in load balancer names to avoid issues with Kubernetes clusters.
