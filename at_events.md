---

copyright:
  years: 2016, 2018

lastupdated: "2018-06-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# CIS {{site.data.keyword.cloudaccesstrailshort}} events
{: #at_events}

Use the {{site.data.keyword.cloudaccesstrailfull}} service to track how users and applications interact with the IBM Cloud Internet Services (CIS) in the {{site.data.keyword.Bluemix}}. 
{:shortdesc}

The {{site.data.keyword.cloudaccesstrailfull_notm}} service records user-initiated activities that change the state of a service in the {{site.data.keyword.Bluemix_notm}}. For more information, see [{{site.data.keyword.cloudaccesstrailfull_notm}}](/docs/services/cloud-activity-tracker/index.html#getting-started-with-cla).




## List of events: DNS domains
{: #events_dns_domain}

The following table lists the actions that are related to DNS domains and generate an event:

<table>
  <caption>List of actions related to DNS domains that genererate an event</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>internet-svcs.zones.create</td>
	  <td>Create a DNS domain.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.update</td>
	  <td>Update a DNS domain.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.delete</td>
	  <td>Delete a DNS domain.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.activation_check.update</td>
	  <td>Perform activation check for a DNS domain.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.dnssec.update</td>
	  <td>Enable / Disable DNSSEC for a DNS domain.</td>
  </tr>
</table>	

## List of events: DNS records
{: #events_dns_record}

The following table lists the actions that are related to DNS records and generate an event:

<table>
  <caption>List of actions that are related to DNS records and genererate an event.</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>internet-svcs.zones.dns_records.create</td>
	  <td>Create a DNS record.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.dns_records.update</td>
	  <td>Update a DNS record.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.dns_records.delete</td>
	  <td>Delete a DNS record.</td>
  </tr>
</table>	


## List of events: Load balancers
{: #events_load_balancers}

The following table lists the actions that are related to load balancers and generate an event:

<table>
  <caption>List of actions that are related to load balancers and genererate an event.</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>internet-svcs.zones.load_balancers.create</td>
	  <td>Create a global load balancer.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.load_balancers.update</td>
	  <td>Update a global load balancer.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.load_balancers.delete</td>
	  <td>Delete a global load balancer.</td>
  </tr>
  <tr>
    <td>internet-svcs.load_balancers.monitors.create</td>
	  <td>Create a health monitor.</td>
  </tr>
  <tr>
    <td>internet-svcs.load_balancers.monitors.update</td>
	  <td>Update a health monitor.</td>
  </tr>
  <tr>
    <td>internet-svcs.load_balancers.monitors.delete</td>
	  <td>Delete a health monitor.</td>
  </tr>
  <tr>
    <td>internet-svcs.load_balancers.pools.create</td>
	  <td>Create a global load balancer pool.</td>
  </tr>
  <tr>
    <td>internet-svcs.load_balancers.pools.update</td>
	  <td>Update a global load balancer pool.</td>
  </tr>
  <tr>
    <td>internet-svcs.load_balancers.pools.delete</td>
	  <td>Delete a global load balancer pool.</td>
  </tr>
</table>



## List of events: Purging the cache
{: #events_cache}

The following table lists the actions that are related to purging the cache and generate an event:

<table>
  <caption>List of actions that are related to purging the cache and genererate an event.</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>internet-svcs.zones.purge_cache.purge_all.update</td>
	  <td>Purge all cached assets of a domain from edge server.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.purge_cache.purge_by_urls.update</td>
	  <td>Purge cached assets by URLs from edge server.</td>
  </tr>
</table>



## List of events: Page rules
{: #events_page_rules}

The following table lists the actions that are related to page rules and generate an event:

<table>
  <caption>List of actions that are related to page rules and genererate an event.</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>internet-svcs.zones.pagerules.create</td>
	  <td>Create a pagerule.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.pagerules.update</td>
	  <td>Update a pagerule.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.pagerules.delete</td>
	  <td>Delete a pagerule.</td>
  </tr>
</table>




## List of events: Firewalls
{: #events_firewalls}

The following table lists the actions that are related to firewalls and generate an event:

<table>
  <caption>List of actions that are related to firewalls and genererate an event.</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>internet-svcs.zones.firewall.waf.packages.groups.update</td>
	  <td>Enable / Disable a group of WAF rulesets.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.firewall.waf.packages.rules.update</td>
	  <td>Enable / Disable a WAF rule.</td>
  </tr>
</table>	



## List of events: Certificate packs
{: #events_certificate_packs}

The following table lists the actions that are related to certificate packs and generate an event:

<table>
  <caption>List of actions that are related to certificate packs and genererate an event.</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>internet-svcs.zones.ssl.certificate_packs.create</td>
	  <td>Order a dedicated certificate.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.ssl.certificate_packs.delete</td>
	  <td>Delete a dedicated certificate.</td>
  </tr>
</table>


## List of events: Custom certificates
{: #events_custom_certificate}

The following table lists the actions that are related to custom certificates and generate an event:

<table>
  <caption>List of actions that are related to custom certificates and genererate an event.</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>internet-svcs.zones.custom_certificates.create</td>
	  <td>Upload a custom certificate.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.custom_certificates.update</td>
	  <td>Update a custom certificate.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.custom_certificates.delete</td>
	  <td>Delete a custom certificate.</td>
  </tr>
</table>







## List of events: Settings
{: #events_settings}

The following table lists the actions that are related to configuring settings and generate an event:

<table>
  <caption>List of actions that are related to configuring settings and generate an event.</caption>
  <tr>
    <th>Action</th>
	  <th>Description</th>
  </tr>
  <tr>
    <td>internet-svcs.zones.settings.cache_level.update</td>
	  <td>Change caching level.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.settings.browser_cache_ttl.update</td>
	  <td>Change browser cache TTL.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.settings.development_mode.update</td>
	  <td>Enable / Disable development mode.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.settings.security_level.update</td>
	  <td>Change security level.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.settings.ssl.update</td>
	  <td>Change SSL setting.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.settings.tls_1_2_only.update</td>
	  <td>Enable / Disable TLS 1.2 support.</td>
  </tr>
  <tr>
    <td>internet-svcs.zones.settings.waf.update</td>
	  <td>Enable / Disable web application firewall.</td>
  </tr>
</table>






## Where to look for the events
{: #ui}

{{site.data.keyword.cloudaccesstrailshort}} events are available in the {{site.data.keyword.cloudaccesstrailshort}} **account domain** that is available in the {{site.data.keyword.Bluemix_notm}} region where the events are generated.



## Additional information
{: #info}

When you monitor {{site.data.keyword.cloudaccesstrailshort}} events that are generated by the IBM Cloud Internet Services (CIS), and you identify an API request for which you need additional information, check the requestData field in the event. Open a support ticket and include the value of the field **X-CORRELATION-ID** that is available in requestData.
