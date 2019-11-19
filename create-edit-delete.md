---

copyright:
  years: 2019
lastupdated: "2019-04-23"

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:important: .important}
{:tip: .tip}

# Create, edit, and delete rules
{: #create-edit-delete-rules}

You can create, edit, and delete Firewall Rules using the information in this topic.
{:shortdesc}

Before getting started, it's a good idea to become familiar with [Fields and Expressions](/docs/infrastructure/cis?topic=cis-fields-and-expressions).
{: note}

## Create a Firewall Rule
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

6. For **Response**, pick an action from the dropdown.
7. To save your rule, choose the most appropriate option by clicking either:

 * **Save as draft** - to save your rule but leave it disabled
 * **Save and deploy** - to save your rule and activate it

## Edit a Firewall Rule
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

## Delete a Firewall Rule
To delete an existing rule, perform the following procedure:

1. Navigate to **Security > Firewall Rules**.
2. In the Firewall Rules table, locate the rule to modify and click the overflow menu on the far right of the row.
3. Select **Delete**.
4. A confirmation dialog appears. Confirm the rule deletion.
