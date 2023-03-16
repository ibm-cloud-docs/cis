---

copyright:
  years: 2018, 2023
lastupdated: "2023-03-08"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Managing your {{site.data.keyword.cis_short_notm}} deployment
{: #manage-your-cis-deployment}

You'll begin by using the Overview screen as your working base of operations. It shows all of the current parameters for your deployment.
{: shortdesc}

Once you've set up your DNS and configured it, you are ready to go!

## Using the Overview screen
{: #using-overview-screen}

Using the Overview screen, you can see the status of all your selections. Each setting links to the section of the user interface where the setting is configured. To modify any selection, you can navigate by clicking the link for the setting. For example, to change the load balancer configuration or add a new load balancer, click the `Load Balancer` field.

On the Overview screen, you might see that your domain name configuration is in **Pending** status, or in **Active** status. **Pending** status indicates that your domain is not fully set up, yet. You have to update your DNS provider or registrar with the name servers that are provided as part of the setup process.

**Enterprise only**: The **Service Details** section of the Overview also allows you to add additional domains to your instance of {{site.data.keyword.cis_short_notm}}, and to switch between multiple domains.

## Changing the Service mode
{: #changing-the-service-mode}

In the Service Mode section of the Overview page is a list menu to select one of two modes:

* **Defense Mode** helps protect against existing or predicted DNS attacks. This mode prevents all traffic from reaching your origin servers through your domain.
* **Pause Service** disables all security and performance benefits to your domain. DNS functions still resolve for your website, but traffic is sent directly to configured origins.

### Setting up Service mode
{: #steps-to-set-service-mode}

1. Select the mode you want from the list menu.
1. Click **Activate mode**.
1. Confirm or cancel the selection in the confirmation pop-up.

A notification appears on all pages to show that either Pause Service or Defense Mode is active.
To return to normal operation, click **Deactivate mode** in the notification banner.

## Configuring and managing your DNS
{: #configure-and-manage-your-dns}

Go to the **Reliability** section, click the **DNS** tab and add a record. Type in the information about your DNS record and then click **Add record** to implement your changes.

After creating your records, consider turning on the `Proxy` setting. Most of the features of {{site.data.keyword.cis_short_notm}} require that the internet traffic to your site flow through {{site.data.keyword.cis_short_notm}} infrastructure. In other words, it only applies to proxied records and load balancers. To really reap the benefit of {{site.data.keyword.cis_short_notm}}, make sure that your DNS records and load balancers have the proxy setting enabled.

## Setting up and manage your caching
{: #set-up-and-manage-your-caching}

Next, you can set up caching. You have the option of three types of caching, available from the caching screen list menu.

* **No query string**: Only delivers resources from cache when there is no query string.
* **Query string independent**: Delivers the same resource to everyone independent of the query string.
   The **Ignore Query String** setting applies only to static file extensions. This setting removes the query string when generating the cache key, so that a request for `style.css?something` is normalized to `style.css` when serving from the cache.
   {: note}

* **Query string dependent**: Delivers a different resource each time the query string changes.

## Purge cache
{: #purge-cache-overview}

You can purge your cache to prepare for updates at any time by entering the URL into the purge cache field. You can purge a single file or multiple files (up to 30 at a time).

## Browser expiration
{: #browser-expiration}

You can use the list menu to select the time of browser expiration that you require; for example, 8 hours, or 1 day.

Enterprise only: You can also instruct {{site.data.keyword.cis_short_notm}} not to override browser cache control by setting this to **Respect Existing Headers**.

## Using Development mode
{: #using-development-mode}

**Development mode** is intended for use when major updates or new file uploads are required, or any time you do not want the end users to work from the cache at all, but to retrieve files directly from the origin servers. To begin using **Development Mode**, toggle the switch to `Enabled` position. To stop using **Development Mode**, toggle the switch to `Disabled` position. **Development mode** expires automatically after 3 hours.

## Managing page rules
{: #managing-your-page-rules}

You can use page rules to specify particular settings that only apply to certain URLs, for example to have different cache control settings for certain URL paths. Use the list menus to configure the page rule. The rule settings are divided into three categories: **Security**, **Performance**, and **Reliability**.

Notice that when certain rules are enabled, other options become grayed out, if those options are in conflict with the other rules you've just selected. After you've selected the page rules that you want, click **Provision** to enable them. The new rules take effect immediately, and they can be viewed immediately on the Page Rules screen.

You also can enable or disable your page rules from the table displayed in the Page Rules screen. See [Using page rules](/docs/cis?topic=cis-use-page-rules) for details.

## Security settings
{: #security-settings-overview}

By default, DDoS protection is enabled for any DNS records or load balancers with proxy on.

**Only** proxied records result in traffic being routed through {{site.data.keyword.cis_short_notm}} cloud edge for edge processing.
{: note}

Security settings are:

* Turn on WAF using the toggle on the **Web Application Firewall** page. When you toggle the rules on or off, the changes are applied immediately.
* **Enterprise only** - The **Rate limiting** page allows you to configure rate limiting rules to avoid noisy-neighbor problems and ward off DDoS.
* On the **IP Firewall** page, you can configure access rules based on IP, country code, or ASN. You can also configure rules to block user agents. The domain lockdown section of this page allows you to limit access to your domain to certain IP addresses.
* You can review firewall-related events on the **Events** page.

## Certificates
{: #certificates-overview}

When you configure a domain, IBM {{site.data.keyword.cis_short_notm}} automatically deploys a universal certificate for that domain. Thus, you don't need to do anything to have certificate-based protection in that domain. If you want, you can upload your own self-managed certificate. You'll need a separate certificate for each domain, and you'll see an error message if the certificate you are uploading does not match your domain. You can also order custom certificates on this page. 

If you want to upload your own certificate, you must ensure that you replace expiring certificates before they expire, otherwise your visitors might not be able to connect. Enterprise plan users can set up an expiration notice using the [Alerts feature](/docs/cis?topic=cis-configuring-policies&interface=ui).
{: important}
