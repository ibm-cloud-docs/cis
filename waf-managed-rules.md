---

copyright:
  years: 2024, 2025
lastupdated: "2025-02-20"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Migrating to managed rules
{: #migrating-to-managed-rules}

The CIS web application firewall (WAF) capabilities are moving under the Rulesets Engine feature. This change requires a manual migration and it is recommended that you use the CIS UI migration wizard. To do so, you need to review the configuration, as well as review security events before finishing the update.
{: shortdesc}

After you complete the migration, any automation that uses APIs, CLIs, or Terraform that are related to WAF will stop working and must be updated to use the new managed rulesets.
{: important}

Instances created after June 2024 use the new Ruleset Engine and do not need to be migrated.
{: tip}

To migrate your instance to managed rules, take the following steps:

1. Navigate to the **Security** section.
1. Select the **WAF** tab. If the CIS instance has not been upgraded, you receive the message to **Update to the new WAF**.
1. Click **Review configuration**.
1. In the **Review configuration** panel, the rulesets are listed in the order in which they are applied.
1. Enable or disable the rulesets by using the switches in the **Status** column.
1. From the **Actions** menu beside each  ruleset, you can choose to edit or reorder the  ruleset, or delete it completely. These actions are considered overrides from the default.
1. In the **Managed rulesets** section, you can add or configure rulesets that are not yet added.
   * Click **Add** on the ruleset you want to add, then toggle the switch from **Disabled** to **Enabled** on the new rule.
   * Click **Configure** on the ruleset you want to configure before migrating. In the **Configure deployment** side panel, you can accept all incoming requests or update the scope of execution with the customized filters you make in the expression builder. Then, click **Save**.
1. Click **Deploy** in the side panel to continue.
1. (Enterprise only) Review the security events in the **Security > Events** tab, and select **Ready to update** when you feel the events are correct.
1. Select **Turn off previous version** to finalize the migration (this step cannot be undone), or cancel to continue editing. This transition does not incur any downtime.

## Editing rulesets
{: #edit-rulesets}

From the Action menu, you can select the following actions:

* **Edit**: Opens a panel where you can change ruleset actions and status, as well as perform a batch edit of rules within the ruleset. Edits are considered overrides of the default rules.
* **Delete**: Removes the ruleset from the list.
* **Move up**: Changes the order in which the rulesets are executed by moving one row higher in priority.
* **Move to...**: Changes the priority order in which the rulesets are executed.

## Adding an exception
{: #add-exception}

To add your own exceptions, take the following steps.

1. Click **Add exception**.
1. In the **Add exception** side panel, enter a name for your exception.
1. Select options in the **When incoming requests match...** section, or use the expression builder to fine-tune the exception.
1. If you want to log matching requests, move the switch to the **On** position.
1. Select if you want the exception to skip all remaining rules, or skip specific rules from a managed ruleset.
1. Click **Save**.

## Managed rules FAQs
{: #managed-rules-faqs}

What if I don't migrate?
:   Users who don’t manually migrate are automatically migrated to the Managed Rules on 12 June 2025, with no expected impact to their current WAF policies or security. From this date forward, you must use the [Ruleset Engine API](/apidocs/cis#get-zone-rulesets) to make WAF and Managed Rules configurations.

    Rules and configuration might be slightly different than before, because the new Managed Rules added more robust OWASP security coverage. This ruleset is updated from OWASP v2.x to OWASP v3.x.

What will happen to the previous WAF APIs?
:   After deprecation, the previous WAF APIs will not be available and generate an error, returning a message that indicates to switch to the Managed Rules feature.

How can I confirm that the migration is complete?
:   Run the Migration Status API check. You can also check to see whether the UI shows the wizard on the WAF page. If the wizard appears, you must migrate.

Can I revert to the previous WAF?
:   No. Migration to managed rulesets is final and cannot be undone.

Why can I no longer see the migration wizard?
:   The wizard appears only when the previous WAF is enabled. If you don't see the wizard, you've likely already migrated.

How do I migrate without using the IBM UI or migration wizard?
:   While APIs are available, the wizard is the recommended method.

## Known issues with migration
{: #migration-known-issues}

You can contact IBM Cloud support for help with the following errors:

* If the number of firewall rules you want to migrate exceeds 200.
* If the length of a firewall rule expression is longer than 4 KB.

## Related links
{: #managed-rules-related-links}

To learn more about the available rulesets, see [About rulesets](/docs/cis?topic=cis-about-rule-sets).
