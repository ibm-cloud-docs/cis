---

copyright:
  years: 2018, 2020
lastupdated: "2020-10-07"

keywords: 

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

# Configuring rate limiting
{:#cis-rate-limiting}

Rate limiting (Enterprise plan only) protects against denial-of-service attacks, brute-force login attempts, and other types of abusive behavior targeting the application layer.
{: shortdesc}

Select the type of rate limiting rule, either a **Custom rule** or **Protect login**

## Creating a custom rate limiting rule
{:#create-a-custom-rate-limiting-rule}

Enter a rule name that helps you remember what the rule does. This is an optional field.

In the **Traffic matching criteria** section, enter the following information. 
1. Select the criteria type.
1. Enter the URL that you are rate limiting.
1. Select the number of requests to allow before triggering rate limiting.
1. Select the time period (in seconds) over which the requests can occur before triggering rate limiting.

The **Advanced Criteria** option allows you to specify which HTTP methods, header responses, and origin response codes to further restrict the matching criteria.

Select a value form the **Method** list menu (ANY is the default).  

Update **HTTP response header**.  You can also **Add response header** to include headers returned by your origin web server.

If you have more than one header under **HTTP response header**, an _AND_ boolean logic applies.  To exclude a header from being matched, use the _Not Equal_ option. Also, each header must be an exact match. However, case sensitivity doesn't apply.
{:note}

Under **Origin response code**, type the valid numerical value of each HTTP response code to match.  To include two or more response codes, separate each value with a comma. For example, you can enter `401, 403` if you only want those two error codes to count.

### Configuring the response
{:#rate-limiting-configure-response}

Select from the actions listed, and specify the timeout period. In this case, the timeout refers to the ban period that the action takes place. A 60 second timeout means the action is applied for 60 seconds.

|Action| Description|
|------|------------|
|Block | Issues a 429 error when the threshold is exceeded|
|Challenge | User must pass a Google reCaptcha Challenge before proceeding. If successful, we accept the request. Otherwise, the request gets blocked.| 	
|JS Challenge |	User must pass a Javascript Challenge before proceeding. If successful, we accept the request. Otherwise, the request gets blocked.
|Simulate| You can use this option to test your rule before applying any of the other options in your live environment.

**Advanced response**

Specify the response type when a rule's threshold is exceeded.

### Bypassing URLs
{:#rate-limiting-bypass}

Bypass lets you create the equivalent of a allowlist or exception for a set of URLs.  No actions trigger for those URLs, even if the Rate Limiting rule is matched.

## Protecting login
{:#rate-limiting-protect-login}

Protect login creates a standard rule that protects login pages against brute-force attacks. Clients attempting to log in more than 5 times in 5 minutes are blocked for 15 minutes.

Enter a name for the rule, and the login URL.
