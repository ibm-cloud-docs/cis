---

copyright:
  years: 2018
lastupdated: "2018-06-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}


# DNS Concepts

This document contains some concepts and definitions related to the internet's domain name system (DNS) and how it affects your IBM Cloud Internet Services (CIS) deployment. 

The Domain Name System (DNS) underpins the web we use every day. It works transparently in the background, converting human-readable website names into computer-readable, numerical IP addresses that follow the [internet's RFC 1918 guidelines for IPv4 and RFC 4193 for IPv6](https://en.wikipedia.org/wiki/Private_network). In short, DNS servers match domain names, such as 'ibm.com', to their associated IP addresses, which most people do not need to know.

The DNS system looks up this IP address and host name information on a network of linked DNS servers across the internet, similarly to how people might look for someplace using a phone book or a map.

## Name Servers
A **name server** implements services that provide responses to queries against a directory service. It translates meaningful, text-based web or host identifiers into IP addresses.

**Name server delegation** takes place when a name server for a domain receives a request for a subdomain's records and responds with the name server's reference to the delegate server. This capability allows you to decentralize the management of a large domain (such as `ibm.com`).

A **custom domain name server** allows you to utilize the DNS provider's servers with the customized reference name of your own domain. For example, you can define your name server to be `ns1.cloud.ibm.com` instead of `ns1.acme.com`.

## Secure DNS

**DNSSec** is a technology to digitally 'sign' DNS data so you can be assured it is valid. To eliminate vulnerability from the internet, DNSSec must be deployed at each step in the lookup, from root zone to final domain name (for example, www.icann.org).

## Root Record CNAME Flattening

IBM CIS supports a feature called "CNAME Flattening." Using this method, root records can overcome the IETF RFC restriction that if a root record is a CNAME, it cannot have any other records for that domain. CIS Authoritative servers overcome this restriction by returning the A records corresponding to the CNAME target instead of returning the CNAME itself, effectively hiding the CNAME. This technique allows other records such as MX records to be added to the domain, even though the root record is a CNAME.

## Proxying DNS Records

IBM CIS supports the ability to toggle whether a record is proxied or not. When a record is proxied, it means that its traffic will run directly through IBM CIS. Currently, records with types **A**, **AAAA**, or **CNAME** can be proxied.
