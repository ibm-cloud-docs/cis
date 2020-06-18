---

copyright:
  years: 2019, 2020
lastupdated: "2020-06-08"

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:term: .term}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:external: target="_blank" .external}
{:generic: data-hd-programlang="generic"}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"}

# Firewall rules
{: #firewall-rules}

{{site.data.keyword.cis_full}} firewall rules offer power and flexibility by targeting HTTP traffic and applying custom criteria to block, challenge, log, or allow certain requests.
{: shortdesc}

## Plan entitlements

You can create many types of firewall rules. However, the number of active rules on your site is limited by your customer plan. See the [Plan comparison](/docs/cis?topic=cis-cis-plan-comparison) page for more information on entitlements.

The number of active rules per plan is fixed. You cannot purchase additional active rules at this time.

## Create, edit, and delete rules
{: #create-edit-delete-rules}

Before getting started, it's a good idea to become familiar with [Fields and Expressions](/docs/cis?topic=cis-fields-and-expressions).
{: note}

### Create a Firewall Rule
To configure a basic Firewall Rule, perform the following procedure:

1. Navigate to **Security > Firewall Rules**.
2. Click the **Create Firewall Rule** button.
3. Enter your rule name or description.
4. Optionally, input a priority, if necessary. Note that a priority of zero is a null priority and will be evaluated last.
5. Use the UI builder in the **Incoming requests** section to add a condition.
 To build an expression with multiple conditions, click either:

 * **And** - to evaluate conditions using _and_ logic
 * **Or** - to evaluate conditions or groups of previously _and_'ed conditions using _or_ logic

 You can see that as you build a condition, the Expression Preview shows the expression in plain text.

 In the Expression Preview, you can click to edit your expression manually instead of using the Visual Expression Builder, or switch between the two. However, depending on the complexity of a manually constructed expression, the Visual Expression Builder may be unable to render it.
{: note}

6. Pick an action from the **Response** list menu.
7. To save your rule, choose the most appropriate option by clicking either:

 * **Save as draft** - to save your rule but leave it disabled
 * **Save and deploy** - to save your rule and activate it

### Edit a Firewall Rule
To edit an existing rule, perform the following procedure:

1. Navigate to **Security > Firewall Rules**.
2. In the Firewall Rules table, locate the rule you want to modify, then click the overflow menu on the far right of the row.
3. Select **Edit**.
4. Make the desired changes to the rule.
7. To save your rule, choose the most appropriate option by clicking either:

 * **Save as draft** - to save your rule but leave it disabled
 * **Save and deploy** - to save your rule and activate it

To pause or activate any rule in the list of existing rules, click the **Enabled** toggle, accordingly.
{: note}

### Delete a Firewall Rule
To delete an existing rule, perform the following procedure:

1. Navigate to **Security > Firewall Rules**.
2. In the Firewall Rules table, locate the rule to modify and click the overflow menu on the far right of the row.
3. Select **Delete**.
4. A confirmation dialog appears. Confirm the rule deletion.

