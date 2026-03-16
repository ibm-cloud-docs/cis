---

copyright:
  years: 2026
lastupdated: "2026-03-16"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Supporting network ports in the CIS proxy
{: #suppoer-network-ports}


## Network ports compatible with CIS proxy
{: #network-ports-compatible-cis-proxy}

By default, CIS proxies traffic destined for the HTTP/HTTPS ports listed.

### Supporting HTTP ports
{: #http-ports-support}

CIS supports the following HTTP ports:

* 80
* 8080
* 8880
* 2052
* 2082
* 2086
* 2095

### Supporting HTTPS ports
{: #https-ports-support}

CIS supports the following HTTPs ports:

* 443
* 2053
* 2083
* 2087
* 2096
* 8443

## Enabling CIS proxy for additional ports
{: #enable-cis-proxy-additional}

If traffic for your domain is destined for a different port than the ones listed above, for example you have an SSH server that listens for incoming connections on port 22, either:

Change your subdomain to be gray-clouded, via your Cloudflare DNS app, to bypass the Cloudflare network and connect directly to your origin.
Configure a Spectrum application for the hostname running the server. Spectrum supports all ports. Spectrum for all TCP and UDP ports is only available on the Enterprise plan. If you would like to know more about Cloudflare plans, please reach out to your Cloudflare account team.
