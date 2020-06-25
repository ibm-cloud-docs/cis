---

copyright:
  years: 2018, 2020
lastupdated: "2020-06-24"

keywords: Helpful tools, whois, IPv4

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
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Helpful tools for managing your CIS deployment
{:#helpful-tools-for-managing-your-cis-deployment}

Some public-domain Unix system administration tools can help you manage your {{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}) deployment.
{: shortdesc}

## Sysadmin tools
{:#cis-sysadmin-tools}

 * `whois` (domain identification tool)
 * `dig` (DNS tool)
 * `cURL` (HTTP and HTTPS tool)
 * `netcat` (IP and port tool)
 * `traceroute` (network tool)

## Commercial tools for external and remote testing
{:#commercial-tools-for-external-and-remote-testing}

 * GTMetrix (http)
 * Web page test (http)
 * WhatsMyDNS (DNS tool)
 * G Suite Toolbox (DNS and HTTP)

## Tools for looking at logs and history
{:#tools-for-looking-at-logs-and-history}

HTTP Archive files (HAR files)

### Using `whois`
{:#using-whois}

`whois` is a Unix system command line tool you can use to look up registrar information for a given domain name or IP address. For example, the domain’s given authoritative servers or the owner of a particular IP address.

Examples:

`whois example.com`

`whois 8.8.8.8`

### Using `dig`
{:#using-dig}

`dig` is a Unix command line tool that can perform DNS queries and check DNS records for a specific domain. It is similar to `nslookup`.

The schema of this command is `dig <record_type> <domainname> <options>`

**Examples:**

`dig example.com`

`dig my.example.com`

`dig example.com +trace`

`dig NS example.com`

`dig example.com @ns.example.com`

### Using `cURL`
{:#using-curl}

`cURL` is a Unix command line tool that lets you transmit data using the URL syntax. It’s commonly used to make HTTP requests or compare server responses.

The schema for this command is: `curl -option1 -option2 http://example.com/url`

**Examples:**

`curl -svo /dev/null http://www.example.com`

`curl -svo /dev/null -A “USER_AGENT_STRING” http://www.example.com`

`curl -svo /dev/null -H “host: www.example.com” http://ORIGIN_IP`

`curl -svo /dev/null -H https://www.example.com --resolve www.example.com:443:ORIGIN_IP`

### Using `mtr` and `traceroute`
{:#using-mtr-and-traceroute}

`mtr` and `traceroute` are Unix command line tools that let you measure performance or latency along a specific network path to a specified host or destination server.

**Examples:**

`mtr -rwc 20 example.com -T -4`
`mtr -rwc 20 8.8.8.8 -T -6`

`traceroute example.com -T -4`

`traceroute 8.8.8.8 -T -6`

| Option | Definition |
|---------|-----------|
| -c | Sets the number of pings sent |
| -T | Forces a TCP traceroute (normally ICMP) |
| -4 | Forces the use of IPv4 |
| -6 | Forces the use of IPv6 |

### Generating an HAR file
{:#generating-a-har-file}

An HAR file is a recording of HTTP requests from a web browser. Browsers, such as Chrome, have a Developer Tools section that can help you get set up to make HAR files.
