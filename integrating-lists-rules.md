---

copyright:
  years: 2018, 2025
lastupdated: "2025-07-15"

keywords: integrating lists
subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Integrating lists in rules
{: #integrating-lists-in-rules}

CIS allows you to use lists in firewall expressions for more efficient rule management. Lists allow you to create a group of items and refer to them collectively, by name, in your expressions. Each list type supports items of a specific data type. All items in a list must have the same data type. Learn how to use these lists within the CIS dashboard and API to enhance security and streamline rule creation.
{: shortdesc}

## Expression Builder
{: #expression-builder}

The Expression Editor allows users to create custom firewall rules by defining conditions based on attributes like IP addresses, HTTP headers, and URL paths. It helps filter traffic with greater precision using logical operators (AND, OR, NOT) for more granular security control.

To use a list in the Expression Builder, follow these steps:

1. Select **is in list** or **is not in list** from the **Operator** menu.
1. Select a list from the **Value** menu. Depending on your plan, you might be able to select a [managed IP list](/docs/cis?topic=cis-managed-lists#managed-ip-lists).
1. To commit your changes and enable the rule, select **Deploy**. If you are not ready to enable the rule, select **Save as Draft**.

## Expression Editor
{: #expression-editor}

The Expression Editor allows you to write and modify logical expressions used in security rules. It enables the combination of various conditions, such as IP address, request headers, and URL paths, to create tailored rules for traffic filtering and security enforcement.

To refer to a list in a rule expression, use `$<list_name>` and specify the `in` operator. Only one value in the list has to match the left-hand side of the expression (before the `in` operator) for the simple expression to evaluate to `true`. If there is no match, the expression evaluates to `false`.

Examples:

* Expression matching requests from IP addresses that are in an IP list named `office_network`:

   ```sh
   ip.src in $office_network
   ```
   {: pre}

* Expression matching requests with a source IP address different from IP addresses in the `office_network` IP list:

   ```sh
   not ip.src in $office_network
   ```
   {: pre}

* Expression matching requests from IP addresses in the CIS Open Proxies [managed IP list](/docs/cis?topic=cis-using-managed-lists&interface=ui#managed-ip-lists).

   ```sh
   ip.src in $cf.open_proxies
   ```
   {: pre}
