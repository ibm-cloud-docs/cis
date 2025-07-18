---

copyright:
  years: 2018, 2025
lastupdated: "2025-07-18"

keywords: health checks, Free Trial plan, dedicated certificate, known issues

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Known issues and limitations
{: #known-limitations}

The following information describes some limitations when working with {{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}), as well as some suggested courses of action to improve your experience.
{: shortdesc}

* It is recommended that you use Chrome.
* The free trial plan is limited to one instance per account. After you create a resource instance and add a domain to it, you are not allowed to add new resource instances for CIS. This restriction is enforced even if you delete a trial domain and then attempt to add a domain again to the same resource instance. You'll encounter an error if you attempt to do so.
* For this service, we support subdomain delegation only using NS records from another provider. CNAME delegation is not supported.
* A, AAAA, and CNAME wildcard records ("*") can't be proxied.
* When you delete a dedicated certificate, it might reappear in the list for a short time before the deletion is complete.
* To modify your custom dedicated certificate’s hostnames after ordering, you must order a new certificate and then delete the old one.
* IP rules created with two letter country codes can only be made with the `Challenge` action. If you want to block visitors from a country, upgrade to the Enterprise plan or place rules on your server to fully block.

## Certificates
{: #known-limitations-certificates}

* **Universal CA:** CIS can change the CA of Universal certificates without prior notice, and will not notify you of these changes. If you prefer to select your own issuing certificate authority, order an advanced certificate.
* **Certificate pinning:** Certificate pinning is not supported natively in {{site.data.keyword.cis_short_notm}}. If you want to use certificate pinning, you must use custom certificates.
* **Full setup:** Universal SSL certificates only support SSL for the root or first-level subdomains such as `example.com` and `www.example.com`. To enable SSL support on second, third, and fourth-level subdomains such as `dev.www.example.com` or `app3.dev.www.example.com` use either an advanced certificate or a custom certificate.
* **CNAME (partial) setup:** On a CNAME setup zone, each subdomain has its own Universal SSL certificate and does not require extra features or purchases.
* **Range:** Universal SSL is not compatible with an {{site.data.keyword.cis_short_notm}} Range application. If you are trying to use Range, use either an advanced certificate or a custom certificate.

## DNS
{: #known-limitations-dns}

* Exporting DNS records includes Cloudflare CNAME records that should be hidden. These records begin with `_` and usually have a second record with  the same name but the `_` is removed.

    ```sh
    Ex.
    _cf.generate.yourdomain.com 0   IN  CNAME address.alias.com
    cf.generate.yourdomain.com 0    IN  CNAME address2.alias.com
    ```
    {: pre}

    These records must be removed from the zone file to properly import.

* Exporting CAA DNS records does not work correctly. The `<tag>` and `<value>` are HEX encoded.

    CAA `<flags>` `<tag>` `<value>`
    {: note}

    ```sh
    Ex.
    Original CAA record
    caa.yourdomain.com. 1 IN CAA 0 issue "letsencrypt.org"

    Exported CAA record
    caa.yourdomain.com. 1 IN CAA 0 6973737565 "6c657473656e63727970742e6f7267"
    ```
    {: codeblock}

    These records must be converted from HEX to string or removed and added manually before importing.
  
## Edge functions
{: #known-limitations-edge-functions}

Before changing your CIS instance from an Enterprise plan to a Standard plan, you must remove all edge function actions and triggers first. Any edge function actions and triggers brought from an Enterprise plan to a Standard plan are not editable, which might cause damage to the normal datapath behavior on your domain. After your plan downgrade is complete, you can recreate the edge functions actions and triggers in the new plan.

## Global load balancer
{: #known-limitations-glb}

* Cloud Internet Services allows you to use the character `_` in load balancer hostnames. However, Kubernetes clusters can't use `_`.
* The Standard plan permits a maximum of 5 load balancers, pools, and health checks. Each pool can have a total of 6 origins, but only 6 unique origins are permitted throughout each CIS instance.
* Health check events for deleted pools and origins can't be filtered, but they still appear in the table.
* If you filter Health check events by `Pool Health`, `Degraded` pools are included because they technically are healthy, but might contain 1 or more critical origins.
* When adding the request header name for a health check, use `Host`, capitalized. Using a lower-case `host` for a health check fails.

## Page rules
{: #known-limitations-pagerules}

* Updating page rules settings using the CIS plugin for IBM Cloud CLI might result in an error if the page rule ID is not included in the JSON string or JSON file for the update. To work around this, submit the update using a complete JSON configuration file for the page rule, including the ID.
* Removing page rule settings using the CIS UI might not remove the setting, even though the UI reports a successful update. To work around this problem, use the CIS plugin for IBM Cloud CLI to remove the setting and include the page rule ID in the JSON update document:

    ```sh
    $> ibmcloud cis page-rule-update <domain-id> <rule-id> -j <file>
    ```
    {: pre}

    The JSON file should include the complete page rule configuration, including ID, with the necessary updates.

## Protocols
{: #limitations-protocols}
 
The following limitations apply to supported protocols:

* HTTPS: Currently, HTTPS applications do not support HTTP/3.
* UDP: Currently, CIS doesn't support UDP packet fragmentation. If a packet is fragmented, the CIS edge drops it.
* Minecraft: Minecraft Java Edition is supported, but Minecraft Bedrock Edition is not supported.
