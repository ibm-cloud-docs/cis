---

copyright:
  years: 2019, 2020
lastupdated: "2020-06-24"

keywords: Cloudant database, CORS, cross-origin resource sharing, host header

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Accessing your Cloudant database through {{site.data.keyword.cis_short_notm}}
{: #access-cloudant-through-cis}

Follow these steps to access your Cloudant database through {{site.data.keyword.cis_full}} ({{site.data.keyword.cis_short_notm}}).
{: shortdesc}

## Before you begin
{: #access-cloudant-through-cis-begin}

These instructions assume you have already added a domain to {{site.data.keyword.cis_short_notm}} as outlined in the [Getting started](/docs/cis?topic=cis-getting-started#getting-started) page.

## Step 1: Add your CIS domain to the Cross-Origin Resource Sharing (CORS)
{: #access-cloudant-through-cis-step1}

* Navigate to your Cloudant database and open the **Account > CORS** page.
* Add your CIS domain to the origin domains input field. For example, `https://cloudant.test.foo.com`.

## Step 2. Configure CIS to point to your Cloudant database
{: #access-cloudant-through-cis-step2}

* Navigate to the CIS dashboard and create a load balancer or DNS record that points to your Cloudant database hostname. For example, `https://cloudant.test.foo.com` -> `111-222-333-444-555-test.cloudant.com`.
* Enable `proxy` for the DNS record or load balancer.

## Step 3. Create a page rule to set the Host Header Override
{: #access-cloudant-through-cis-step3}

* In the CIS dashboard, navigate to **Performance > Page rules**.
* Create a page rule for the URL you want, for example, `https://cloudant.test.foo.com/*`.
* Select the Rule Behavior setting `Host Header Override`.
* Set as the Cloudant database hostname, for example, `111-222-333-444-555-test.cloudant.com`.

To learn more about Cloudant, see the [Cloudant documentation](/docs/Cloudant?topic=Cloudant-getting-started-with-cloudant#getting-started-with-cloudant).
