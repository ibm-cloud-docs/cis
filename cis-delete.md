---

copyright:
  years: 2024
lastupdated: "2024-11-06"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Deleting a {{site.data.keyword.cis_short_notm}} instance
{: #cis-delete-instance}

Removing your domain cancels all active subscriptions, which will not be refunded per our billing policy. If you add this domain back, you must re-purchase all subscriptions. Removing your domain does not change your
domain registration.
{: shortdesc}

## Before you begin
{: #before-you-begin-delete-instance}

Before you delete a CIS instance, make sure that you have satisfied the following requirements:

* If you experience website issues, temporarily pause CIS to evaluate your website's performance.
* If you have to re-add the domain in a different account, make sure to save the current settings. For example, you might import and export DNS records.
* Removing a domain prevents your domain from using DNS resolution. To avoid DNS errors, update your name servers at your domain registrar to use name servers not owned by CIS.
* Confirm that your name servers no longer point to CIS.
* At your registrar, make sure you do not have a DS DNS record. This record enables DNS Security Extensions (DNSSEC) and could prevent your DNS records from being changed.

## Deleting a {{site.data.keyword.cis_short_notm}} instance in the UI
{: #delete-cis-instance-ui}
{: ui}

To delete a CIS instance in the UI, follow these steps:

1. Recommended: Delete all the Logpush jobs for that domain. To do so, go to the **Accounts** page, then scroll to the Logpush list on the Logs tab. Click **Delete** from the Actions menu ![Actions icon](../icons/action-menu-icon.svg "Actions") on the right side of the Logpush name.

   You cannot undo this action.
   {: note}

1. To start the deletion process, go to the **Overview** page and click **Delete** from the domain's Actions menu.

If you are moving your domain to a different provider, be sure to migrate your DNS records and other configuration information to the new provider before you activate the domain there. Activating the domain before you migrate from CIS can cause your domain to change to the [Moved state](/docs/cis?topic=cis-domain-moved-status).
{: important}

## Deleting a {{site.data.keyword.cis_short_notm}} instance from the CLI
{: #delete-cis-instance-cli}
{: cli}

To delete a CIS instance from the CLI, follow these steps:

1. Recommended: Delete all the Logpush jobs for that domain.

   You cannot undo this action.
   {: note}

1. Enter the following command:

   ```bash
   ibmcloud cis instance-delete INSTANCE [-f, --force][-h, --help]
   ```

   Where:

   `INSTANCE`
   :    Is the name or ID of a CIS service instance.

   `-f, --force`
   :    Force the operation without confirmation.

   `-h, --help`
   :    Get help on this command.

If you are moving your domain to a different provider, be sure to migrate your DNS records and other configuration information to the new provider before you activate the domain there. Activating the domain before you migrate from CIS can cause your domain to change to the [Moved state](/docs/cis?topic=cis-domain-moved-status).
{: important}
