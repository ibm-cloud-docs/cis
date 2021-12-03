---

copyright:
  years: 2021
lastupdated: "2021-02-05"

keywords: 

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Why am I not seeing any network traffic?
{: #troubleshooting-cis-network-traffic}
{: help}
{: support}

You don't see any network traffic.
{: tsSymptoms}

There might be a redirect that is routing the traffic to the root domain.
{: tsCauses}

If you’re not seeing traffic, and you’re using a CNAME, make sure that there are no redirects in place that are routing the traffic to the root domain. 
{: tsResolve}


Remember that some DNS propagations can take up to 48 hours to complete.