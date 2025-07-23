---

copyright:
  years: 2025
lastupdated: "2025-07-23"

keywords: lists

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About lists
{: #lists}

Use lists to refer to a group of items (such as IP addresses) collectively, by name, in rule expressions. You can create your own custom lists or use lists managed by CIS, such as [managed IP lists](/docs/cis?topic=cis-using-managed-lists&interface=ui#managed-ip-lists).

Lists have the following advantages:

* When creating a rule, using a list is easier and less error-prone than adding a long list of items, such as IP addresses to a rule expression.
* When updating a set of rules that target the same group of IP addresses (or hostnames), using an IP list (or a hostname list) is easier and less error prone than editing multiple rules.
* Lists are easier to read and more informative, particularly when you use descriptive names for your lists.

When you update the content of a list, any rules that use the list are automatically updated, so you can make a single change to your list rather than modify rules individually.

CIS stores your lists at the account level. You can use the same list in rules of different zones in your CIS account.

## Supported lists
{: #supported-lists}

CIS supports the following lists:

* [Custom lists](/docs/cis?topic=cis-custom-lists): Includes custom IP lists, hostname lists, and ASN lists.
* [Managed lists](/docs/cis?topic=cis-managed-lists): Lists managed and updated by CIS. 

## List requirements
{: #list-availability-requirements}

All user-defined lists must follow these formatting and usage rules:

* You can have a maximum number of 10,000 list items across all custom lists.
* For a list name, use only lowercase letters, numbers, and the underscore `(_)` character in the name. A valid name satisfies this regular expression: `^[a-z0-9_]+$.`
* The maximum length of a list name is 50 characters.
* You can only delete a list when there are no rules (enabled or disabled) that reference that list.
   
To learn how to use lists in Ruleset Engine rules, see [Integrating lists in rules](/docs/cis?topic=cis-integrating-lists-in-rules).
{: note}

## Using lists in rules
{: #using-lists-in-rules}

After you’ve created a custom list, you can use it in your rule expressions to match incoming traffic based on the list’s contents. Custom lists are used with the `in` operator as shown:

```bash
<FIELD> in $<LIST_NAME>
```
{: pre}

This rule checks whether the specified field matches any item in the custom list.

The fields that you can use vary according to the list type:

| List type	 | Available fields |
| ------------ | ------------------- |
| IP address | Fields with type `IP address` listed in the [Fields reference](/docs/cis?topic=cis-custom-rules-fields-and-expressions#custom-rule-fields) |
| Hostname | `http.host` |
| ASN | `ip.src.asnum` |
{: caption="Available custom list type" caption-side="bottom"}

You can apply lists in a variety of use cases, such as:

* Blocking or allowing traffic from specific IP ranges
* Filtering requests by known domains
* Prioritizing routing for traffic from specific ISPs or regions

For details on how to build rule expressions with lists, see [Integrating lists in rules](/docs/cis?topic=cis-integrating-lists-in-rules). 
