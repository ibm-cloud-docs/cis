---

copyright:
  years: 2019
lastupdated: "2019-03-28"

keywords: Cloudant database, CORS, cross-origin resource sharing, host header

subcollection: cis

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"} 
{:note: .note}


# Access your Cloudant database through IBM Cloud Internet Services
{: #access-cloudant-through-cis}

Follow these steps to access your Cloudant Database through IBM Cloud Internet Services (CIS).

## Before you begin
{: #access-cloudant-through-cis-begin}

These instructions assume you have already added a domain to CIS as outlined in the [Getting Started](/docs/infrastructure/cis?topic=cis-getting-started-with-ibm-cloud-internet-services-cis-) page.

### Step 1: Add your CIS domain to the Cross-Origin Resource Sharing (CORS)
{: #access-cloudant-through-cis-step1}

* Navigate to your Cloudant database and open the `Acccount` -> `CORS` page.
* Add your CIS domain to the origin domains input field. For example, `https://cloudant.test.foo.com`.

### Step 2. Configure CIS to point to your Cloudant database
{: #access-cloudant-through-cis-step2}

* Navigate to the CIS dashboard and create a load balancer or DNS record that points to your Cloudant database hostname. For example, `https://cloudant.test.foo.com` -> `111-222-333-444-555-test.cloudant.com`.
* Enable `proxy` for the DNS record or load balancer.


### Step 3. Create a page rule to set the Host Header Override
{: #access-cloudant-through-cis-step3}

* In the CIS dashboard navigate to `Performance` -> `Page Rules`.
* Create a page rule for the desired URL, for example, `https://cloudant.test.foo.com/*`.
* Select the Rule Behavior setting `Host Header Override`.
* Set as the Cloudant database hostname, for example, `111-222-333-444-555-test.cloudant.com`.

For more information on Cloudant, see the [Coudant documentation](/docs/services/Cloudant?topic=cloudant-getting-started-with-cloudant).
