---

copyright:
  years: 2018, 2020
lastupdated: "2020-06-05"

keywords: 

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
{:table: .aria-labeledby="caption"}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Troubleshooting your {{site.data.keyword.cis_short_notm}} network connection
{:#troubleshooting-your-cis-network-connection}

## How do I know if my data is passing through my {{site.data.keyword.cis_full_notm}} connection?
{:#how-do-i-know-if-my-data-is-passing-through-my-cis-connection}
{: help}
{: support}

{{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}) uses HTTP headers, which it can read, add, or modify. The header lets us trace how a request was routed, using a CF-Ray number. The CF-Ray number can be found by a `curl` command or with a Google Chrome plugin in called "Claire".

To know whether data has passed through {{site.data.keyword.cis_short_notm}}, locate the `Ray ID` which is present on every packet.

**Unix command line tools:**

 * curl for HTTP: `$ curl -vso /dev/null http://example.com`
 * dig for DNS: `$ dig www.example.com`
 * traceroute for network: `$ traceroute example.com`

**For example:**

Terminal command:  `curl -svo /dev/null YOUR_URL_HERE. -L`

Results in: `CF-RAY: 1ca349b6c1300da3-SJC`

## Adding CF-Ray headers
{: #add-cf-ray-headers}

The CF-RAY header is added to help trace a request to a website through the network. Use it when working with Support to help troubleshoot any related issues with connectivity. You can reveal this "Ray ID" in your logs by making some edits to configuration files in Apache and nginx.

### Apache
{:#troubleshooting-cis-apache}

```
LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-agent}i\" %{CF-Ray}i" cf_custom

CustomLog log/access_log cf_custom
```
{:pre}

### NGINX
{:#troubleshooting-cis-nginx}

```
log_format cf_custom '$remote_addr - $remote_user [$time_local]  '
                    '"$request" $status $body_bytes_sent '
                    '"$http_referer" "$http_user_agent" '
                    '$http_cf_ray';

access_log  /var/log/nginx/access.log cf_custom;
```
{:pre}

## What do I do if I use the Cloudflare Origin root certificate, and it's expiring?
{: #update-origin-root-ca}

Some origin web servers (such as IIS and cPanel) validate origin root CA certificates and require you to upload one.

If you are using the RSA version of the Cloudflare origin root CA, it expires on November 11, 2019 (2019-11-14T01:43:50Z). You must take the following actions to avoid site disruptions.

### Download and install new certificate
{: #download-new-cert}

Select one of the following root certificates to download and install.

  * [RSA version certificate.](https://cloud.ibm.com/media/docs/downloads/cis/origin_ca_rsa_root.pem) The previous version expires on 2019-11-14T01:43:50Z.  
  * [ECC version certificate.](https://cloud.ibm.com/media/docs/downloads/cis/origin_ca_ecc_root.pem) The previous version expires on 2021-02-22T00:24:00Z.

## How do I trace a route?
{:#how-do-i-trace-a-route}
{: help}
{: support}

To see whether a route goes through your {{site.data.keyword.cis_short_notm}} pathway, you can perform a `dig` in a Terminal window for Mac or Linux or use `nslookup` in the Windows command prompt for Windows.

If the packet has a CF-Ray value, then it has traveled through {{site.data.keyword.cis_short_notm}}.

The `traceroute` command shows the entire path that an IP request has taken.

The support team makes use of these commands to assist you.

## If you see a privacy warning
{:#troubleshooting-cis-privacy-warning}

The certificates issued by {{site.data.keyword.cis_short_notm}} cover the root domain (`example.com`) and one level of subdomain (`*.example.com`). If you’re trying to reach a second-level subdomain (`*.*.example.com`) a privacy warning appears in your browser, because these host names are not added to the SAN.

Allow up to 15 minutes for one of our partner Certificates Authorities (CAs) to issue a new certificate. A privacy warning appears in your browser if your new certificate has not yet been issued.

## What do I do if I’m under a DDoS attack?
{:#troubleshooting-cis-ddos-attack}
{: help}
{: support}

 * **Step 1:** Turn on "Defense Mode" from your dashboard.
 * **Step 2:** Set your DNS records for maximum security.
 * **Step 3:** Do not rate-limit or throttle requests from {{site.data.keyword.cis_short_notm}}.

During "Defense Mode", each new visitor is met with a "Captcha" security challenge, which they must pass before being given a cookie for unchallenged access. That way, botnet traffic is blocked until the "Defense Mode" is turned off. Visitors that do not meet the security challenge are added to the (bad) IP Reputation database.

## Other problems you might encounter
{:#troubleshooting-cis-other-problems}

Here are some common error messages you or your support team might see:

| Error Code    | Reason |
| ------------- | ------------- |
| 1001  | DNS Resolution Error. Either the customer recently signed up and their DNS information has not yet propagated, or whomever is managing the DNS has a failure. |
| 521  | Origin web server refused connection from {{site.data.keyword.cis_short_notm}}. Either the origin web server is not running, or something is blocking {{site.data.keyword.cis_short_notm}} IP addresses. |
| 522  | Connection timeout to the origin server (30 second default). Either CIS might be rate-limited, the web server could be consuming all resources (shared server), or there might be network connectivity issues between the web server and {{site.data.keyword.cis_short_notm}}. |
| 523  | Origin server is unreachable. Ensure that the origin IP address for the DNS record is the same as the one appearing in the {{site.data.keyword.cis_short_notm}} DNS Settings page. |
| 524  | {{site.data.keyword.cis_short_notm}} could make a TCP connection but did not receive a response from the web server. A long-running application or database query is interfering. |

### Not seeing any network traffic
{:#troubleshooting-cis-network-traffic}
{: help}
{: support}

If you’re not seeing traffic, and you’re using a CNAME, make sure that there are no redirects in place that are routing the traffic to the root domain. Remember that some DNS propagations can take up to 48 hours to complete.

### Website offline
{:#troubleshooting-cis-website-offline}

Here is what you might see: `IBM CIS cannot connect to the origin server (error 521, 522, 523)`.

**Website offline - no cached version**

1. The server is online, but it is blocking the {{site.data.keyword.cis_short_notm}} request.
2. The origin server is offline and {{site.data.keyword.cis_short_notm}}S does not have a backup website image

What you can do:

* Verify that the {{site.data.keyword.cis_short_notm}} IP addresses are allowlisted.
* Make sure that {{site.data.keyword.cis_short_notm}} IPs are not being rate-limited.
* Review the list of [IPs to allowlist](/docs/cis?topic=cis-cis-allowlisted-ip-addresses).

### 502 error “The dreaded 502”
{:#troubleshooting-cis-502-error}
{: help}
{: support}

This error is one of the most common ones you might see. It typically occurs when a portion of a network is unavailable; for example, at the start of a DDoS attack. A particular data center might be unavailable for a time. Traffic is re-routed. It is recommended that you run a trace route.

Here is what you might see: `Error 502 - bad gateway error`

What happened:

* A portion of the {{site.data.keyword.cis_short_notm}} network is having an issue.
* Usually the problem is limited to one server in one data center.
* It affects only a portion of the site's visitors.
* The {{site.data.keyword.cis_short_notm}} Technical Operations team deals with these.

What you can do:

* Send the results from `www.YOUR_DOMAIN.com/cdn-cgi/trace` in a case to [IBM Support](/docs/get-support?topic=get-support-using-avatar).
* Temporarily toggle your DNS Records to off (No proxy).
