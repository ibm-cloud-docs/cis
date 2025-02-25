---

copyright:
  years: 2019, 2025
lastupdated: "2025-02-24"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Creating, editing, and deleting firewall rules
{: #about-firewall-rules}



{{site.data.keyword.cis_full}} firewall rules offer power and flexibility by targeting HTTP traffic and applying custom criteria to block, challenge, log, or allow certain requests.
{: shortdesc}

You can create many types of firewall rules. However, the number of active rules on your site is limited by your customer plan. See [Comparing CIS plans](/docs/cis?topic=cis-cis-plan-comparison) for more information on entitlements.

The number of active rules per plan is fixed. You can't purchase additional active rules at this time.

Before getting started, it's a good idea to become familiar with [Using fields, functions, and expressions](/docs/cis?topic=cis-fields-and-expressions).
{: important}

## Creating a firewall rule
{: #create-firewall-rule}

Follow these steps to configure a basic firewall rule:

1. Navigate to **Security > Firewall Rules**.
2. Click **Create Firewall Rule**.
3. Enter a rule name and optional description.
4. Optionally, input a priority, if necessary. Note that a priority of zero is a null priority and is evaluated last.
5. Use the UI builder in the **Incoming requests** section to add a condition.
    To build an expression with multiple conditions, click either:
    * **And** - to evaluate conditions using _and_ logic
    * **Or** - to evaluate conditions or groups of previously _and_'ed conditions using _or_ logic

    You can see that as you build a condition, the Expression Preview shows the expression in plain text.

    In the Expression Preview, you can click to edit your expression manually instead of using the Visual Expression Builder, or switch between the two. However, depending on the complexity of a manually constructed expression, the Visual Expression Builder might be unable to render it.
    {: note}

6. Pick an action from the **Response** list menu.
7. To save your rule, choose the most appropriate option by clicking either:
    * **Save as draft** to save your rule, but leave it disabled.
    * **Save and deploy** to save your rule and activate it.

## Editing a firewall rule
{: #edit-firewall-rule}

Follow these steps to edit an existing rule:

1. Navigate to **Security > Firewall Rules**.
1. In the Firewall Rules table, locate the rule you want to modify, then click the Actions menu on the right of the row.
1. Select **Edit**.
1. Make your changes to the rule.
1. To save your rule, choose the most appropriate option by clicking either:
    * **Save as draft** to save your rule, but leave it disabled.
    * **Save and deploy** to save your rule and activate it.

To pause or activate any rule in the list of existing rules, click the **Enabled** toggle.
{: note}

## Deleting a firewall rule
{: #delete-firewall-rule}

Follow these steps to delete an existing rule:

1. Navigate to **Security > Firewall Rules**.
1. In the Firewall Rules table, locate the rule to modify and click the Actions menu on the right of the row.
1. Select **Delete**.
1. Confirm the rule deletion.
