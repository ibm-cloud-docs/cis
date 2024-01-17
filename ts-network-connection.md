---

copyright:
  years: 2018, 2021
lastupdated: "2021-09-13"

keywords: 

subcollection: cis

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Troubleshooting your {{site.data.keyword.cis_short_notm}} network connection
{: #troubleshoot-your-cis-network-connection}
{: troubleshoot}

Use the following methods to gather information that can help you to troubleshoot your network connection. 
{: shortdesc}


## Determine if your data is passing through your {{site.data.keyword.cis_full_notm}} connection
{: #is-data-passing-through-cis-connection}
{: help}
{: support}

{{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}) uses HTTP headers, which it can read, add, or modify. The header lets us trace how a request was routed, using a CF-Ray number. The CF-Ray number can be found by a `curl` command or with a Google Chrome plugin in called "Claire".

To know whether data has passed through {{site.data.keyword.cis_short_notm}}, locate the `Ray ID` which is present on every packet.

### Unix command line tools
{: #unix-cli-tools}

* curl for HTTP: `$ curl -vso /dev/null http://example.com`
* dig for DNS: `$ dig www.example.com`
* traceroute for network: `$ traceroute example.com`

For example, the terminal command `curl -svo /dev/null YOUR_URL_HERE. -L` results in the following:

`CF-RAY: 1ca349b6c1300da3-SJC`
{: screen}

## Perform a traceroute?
{: #trace-route}
{: help}
{: support}

To see whether a route goes through your {{site.data.keyword.cis_short_notm}} pathway, you can perform a `dig` in a Terminal window for Mac or Linux or use `nslookup` in the Windows command prompt for Windows.

If the packet has a CF-Ray value, then it has traveled through {{site.data.keyword.cis_short_notm}}.

The `traceroute` command shows the entire path that an IP request has taken.

The Support team makes use of these commands to assist you.


## Adding CF-Ray headers
{: #add-cf-ray-headers}

The CF-RAY header is added to help trace a request to a website through the network. Use it when working with Support to help troubleshoot any related issues with connectivity. You can reveal this "Ray ID" in your logs by making some edits to configuration files in Apache and nginx.

### Apache
{: #troubleshooting-cis-apache}

```sh
LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-agent}i\" %{CF-Ray}i" cf_custom

CustomLog log/access_log cf_custom
```
{: pre}

### NGINX
{: #troubleshooting-cis-nginx}

```sh
log_format cf_custom '$remote_addr - $remote_user [$time_local]  '
                    '"$request" $status $body_bytes_sent '
                    '"$http_referer" "$http_user_agent" '
                    '$http_cf_ray';

access_log  /var/log/nginx/access.log cf_custom;
```
{: pre}
