---

copyright:
  years: 2023
lastupdated: "2023-08-24"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I delete my {{site.data.keyword.cis_short_notm}} instance?
{: #delete-instance}

When you want to delete an instance of {{site.data.keyword.cis_short_notm}}, sometimes the delete operation doesn't work.
{: shortdesc}

You attempted to delete your {{site.data.keyword.cis_short_notm}} instance, but it failed.
{: tsSymptoms}

Instances that have domains attached can't be deleted. 
{: tsCauses}

If any global load balancers are attached, they can also cause the delete operation to fail. 

Before deleting an instance, all of the domains in the instance must be removed.
{: Resolve}

Additionally, make sure that all global load balancers have been removed.
