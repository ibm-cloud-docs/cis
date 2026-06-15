
## WAF - WAF Release - 2026-06-09
**Published on:** Tue, 09 Jun 2026 00:00:00 GMT

This release introduces new detections for a critical SQL injection vulnerability in Drupal installations utilizing PostgreSQL (CVE-2026-9082), alongside targeted protection for an unsafe deserialization flaw in the Mirasvit Cache Warmer extension (CVE-2026-45247). Additionally, this release includes coverage for a prototype pollution vector in Axios (CVE-2026-40175) and a new generic rule designed to identify and block sophisticated SQL Injection (SQLi) bypass attempts leveraging obfuscated boolean logic.

**Key Findings**

  * CVE-2026-9082: A database abstraction vulnerability affects Drupal sites configured with a PostgreSQL backend. Remote, unauthenticated attackers can exploit this flaw via crafted inputs to inject malicious SQL commands and access or manipulate backend data.

  * CVE-2026-45247: A PHP Object Injection vulnerability exists in the Mirasvit Cache Warmer extension for Magento and Adobe Commerce. This flaw stems from unsafe deserialization of untrusted user input, enabling unauthenticated attackers to execute arbitrary code on the hosting server.

  * CVE-2026-40175: A prototype pollution vulnerability affects the Axios HTTP client library. Attackers can exploit this to inject malicious properties into the global JavaScript object prototype, potentially causing application crashes (Denial of Service) or executing unauthorized code depending on the application structure.




**Impact**

Successful exploitation of these vulnerabilities could allow unauthenticated attackers to execute arbitrary code, manipulate database contents, or induce application crashes, leading to severe operational disruption or complete server compromise. These newly deployed signatures intercept these advanced malicious payloads at the edge before they can interact with vulnerable software configurations.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| b4f88cb767874def810edd0b387cf935 | N/A| Axios - Prototype Pollution - CVE:CVE-2026-40175| Log| Block| This is a new detection.
CIS Managed Ruleset| 098997bb8b5f48abb4039bd6417eb9e0 | N/A| Drupal - PostgreSQL SQLi - CVE:CVE-2026-9082 - Body| Log| Block| This is a new detection.
CIS Managed Ruleset| 8a7650b99ec04a91a19b8295fd3857fd | N/A| Drupal - PostgreSQL SQLi - CVE:CVE-2026-9082 - URI| Log| Block| This is a new detection.
CIS Managed Ruleset| 525c0871787840e6a6193f6caee241d2 | N/A| SQLi - Obfuscated Boolean - Body| N/A| Disabled| This is a new detection.
CIS Managed Ruleset| 1ec4aeaf7900463397b82b35d8620070 | N/A| SQLi - Obfuscated Boolean - Headers| N/A| Disabled| This is a new detection.
CIS Managed Ruleset| fb74766654c44ff2a5204dc4e0be4d47 | N/A| Mirasvit Cache Warmer - PHP Object Injection - CVE:CVE-2026-45247| N/A| Block| This is a new detection.


## WAF - WAF Release - Scheduled changes for 2026-06-15
**Published on:** Tue, 09 Jun 2026 00:00:00 GMT

Announcement Date| Release Date| Release Behavior| Legacy Rule ID| Rule ID| Description| Comments
---|---|---|---|---|---|---
2026-06-09| 2026-06-15| Log| N/A| 439c4ef64b32447989bdf412b4c29bc6 | Ghost CMS - SQLi - CVE:CVE-2026-26980| This is a new detection.
2026-06-09| 2026-06-15| Log| N/A| 6c64b68ef5ed45e7a622cdaab56f403f | SQLi - Obfuscated Boolean - URI| This is a new detection.


## WAF - WAF Release - 2026-05-20
**Published on:** Wed, 20 May 2026 00:00:00 GMT

**Key Findings**

  * Existing rule enhancements have been deployed to improve detection resilience against broad classes of web attacks and strengthen behavioral coverage.



**Continuous Rule Improvements**

We are continuously refining our managed rules to provide more resilient protection and deeper insights into attack patterns. To ensure an optimal security posture, we recommend consistently monitoring the Security Events dashboard and adjusting rule actions as these enhancements are deployed.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| bcdcec3ea63a480896513dc39e9c068d | N/A| Sitecore - Cache Poisoning - CVE:CVE-2025-53693 Beta| N/A| Block| This rule is merged into the original rule "Sitecore - Cache Poisoning - CVE:CVE-2025-53693" (ID: d1bd7563e6254db48ce703807c5b669c ).


## WAF - WAF Release - 2026-05-15 - Emergency
**Published on:** Fri, 15 May 2026 00:00:00 GMT

This emergency release introduces two new rules to detect nginx heap buffer overflow and heap spray exploitation attempts targeting the rewrite module's `is_args` stale-state bug (CVE-2026-42945).

**Key Findings**

CVE-2026-42945: nginx Heap Buffer Overflow via Stale `is_args` in Rewrite Module

Successful exploitation allows remote attackers to trigger a heap buffer overflow in nginx's rewrite module by sending crafted URIs containing escapable characters. A length/copy pass mismatch in `ngx_http_script_copy_capture_code()` causes the copy pass to write escaped data into an undersized buffer, leading to heap corruption. This enables denial of service (worker process crash) and, with heap feng shui techniques, potential remote code execution.

We strongly recommend upgrading to nginx 1.30.1 (or later) immediately to address the underlying vulnerability. If you cannot upgrade immediately, avoid `rewrite` directives with `?` in the replacement string followed by `set` or `if` referencing capture groups.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 2013e3e58efe4b79a26e214f7e52be73 | N/A| nginx - Remote Code Execution - Buffer Overread - CVE:CVE-2026-42945| N/A| Block| This is a new detection.
CIS Managed Ruleset| 68226e83a4d14ee9a9c878469df0ee6c | N/A| nginx - Remote Code Execution - Heap Spray - CVE:CVE-2026-42945| N/A| Block| This is a new detection.


## WAF - WAF Release - 2026-05-11
**Published on:** Mon, 11 May 2026 00:00:00 GMT

**Key Findings**

  * Existing rule enhancements have been deployed to improve detection resilience against broad classes of web attacks and strengthen behavioral coverage.



**Continuous Rule Improvements**

We are continuously refining our managed rules to provide more resilient protection and deeper insights into attack patterns. To ensure an optimal security posture, we recommend consistently monitoring the Security Events dashboard and adjusting rule actions as these enhancements are deployed.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 23ac4a9e53f94467ba470c9468b3c389 | N/A| Remote Code Execution - Java Deserialization - Body - Beta| Block| Disabled| This is a new detection. This rule is merged into the original rule "Remote Code Execution - Java Deserialization" (ID: 36b0532eb3c941449afed2d3744305c4 ).


## Workers, WAF - WAF and framework adapter mitigations for React and Next.js vulnerabilities
**Published on:** Thu, 07 May 2026 12:00:00 GMT

Multiple security vulnerabilities were disclosed by the React team and Vercel affecting React Server Components and Next.js. These include denial of service, middleware and proxy bypass, server-side request forgery, cross-site scripting, and cache poisoning issues across a range of severity levels.

**We strongly recommend updating your application and its dependencies immediately.** Patched versions are available for React (`react-server-dom-webpack`, `react-server-dom-parcel`, and `react-server-dom-turbopack` `19.0.6`, `19.1.7`, and `19.2.6`) and Next.js (`15.5.16` and `16.2.5`).

#### WAF protections

CIS WAF rules deployed in response to prior React Server Component CVEs ([`CVE-2025-55184`](https://github.com/facebook/react/security/advisories/GHSA-2m3v-v2m8-q956) and [`CVE-2026-23864`](https://github.com/facebook/react/security/advisories/GHSA-83fc-fqcc-2hmg)) already provide coverage for the newly disclosed denial-of-service vulnerabilities. These rules are enabled by default with a Block action for all customers using the CIS Managed Ruleset, including Free plan customers using the Free Managed Ruleset.

Ruleset| Rule description| Rule ID| Default action
---|---|---|---
CIS Managed Ruleset| React - DoS - [`CVE-2025-55184`](https://github.com/facebook/react/security/advisories/GHSA-2m3v-v2m8-q956)| `2694f1610c0b471393b21aef102ec699`| Block
CIS Managed Ruleset| React - DoS - [`CVE-2026-23864`](https://github.com/facebook/react/security/advisories/GHSA-83fc-fqcc-2hmg)| `aaede80b4d414dc89c443cea61680354`| Block

The existing rules detect the underlying attack patterns generically. As a result, they apply to the new [`CVE-2026-23870`](https://github.com/facebook/react/security/advisories/GHSA-rv78-f8rc-xrxh) denial-of-service vulnerability in Server Components and the corresponding Next.js advisory [`GHSA-8h8q-6873-q5fj`](https://github.com/vercel/next.js/security/advisories/GHSA-8h8q-6873-q5fj).

CIS is investigating whether WAF rules can be safely and effectively deployed for three of the high-severity advisories: [`CVE-2026-23870`](https://github.com/facebook/react/security/advisories/GHSA-rv78-f8rc-xrxh) / [`GHSA-8h8q-6873-q5fj`](https://github.com/vercel/next.js/security/advisories/GHSA-8h8q-6873-q5fj), [`GHSA-267c-6grr-h53f`](https://github.com/vercel/next.js/security/advisories/GHSA-267c-6grr-h53f), and [`GHSA-mg66-mrh9-m8jx`](https://github.com/vercel/next.js/security/advisories/GHSA-mg66-mrh9-m8jx). If it is possible to create a managed WAF rule that mitigates these CVEs and does not potentially break application behavior, CIS will add additional managed WAF rules. These rules will be announced through the [WAF changelog](https://developers.cloudflare.com/waf/change-log/changelog/). Because these vulnerabilities were shared with CIS with minimal advance notice, we are still investigating what WAF mitigations are possible.

Several of the disclosed vulnerabilities are not possible to block in WAF. We strongly recommend updating your applications so they are not purely reliant on WAF mitigations.

Customers on Pro, Business, or Enterprise plans should ensure that [Managed Rules are enabled](https://developers.cloudflare.com/waf/get-started/#1-deploy-the-cloudflare-managed-ruleset).

#### Next.js adapters

**Vinext:** [Vinext](https://github.com/cloudflare/vinext) is a Vite plugin that reimplements the Next.js API surface. Vinext's latest release is not vulnerable to any of the disclosed CVEs. Vinext's architecture differs from stock Next.js in ways that sidestep the affected code paths. For example, it does not implement the PPR resume protocol, does not expose Pages Router data-route endpoints, and strips internal headers such as `x-nextjs-data` at request boundaries. As an extra layer of defense, we added a React `19.2.6` or later requirement when running `vinext init` ([PR #1118](https://github.com/cloudflare/vinext/pull/1118), [PR #1112](https://github.com/cloudflare/vinext/pull/1112)) to prevent accidentally running a vulnerable version of React with Vinext.

**OpenNext on CIS:** OpenNext is an adapter that lets you deploy Next.js apps to the CIS Workers platform. OpenNext itself is not directly vulnerable to the React denial-of-service CVE, but users must update the Next.js version in their application. The OpenNext team has updated the adapter to further harden against these vectors and released a new version of the CIS adapter. Test fixtures and examples have been updated to use patched versions ([PR #1255](https://github.com/opennextjs/opennextjs-cloudflare/pull/1255)).

#### Summary of disclosed vulnerabilities

Advisory| Severity| Issue| WAF status
---|---|---|---
[`CVE-2026-23870`](https://github.com/facebook/react/security/advisories/GHSA-rv78-f8rc-xrxh) / [`GHSA-8h8q-6873-q5fj`](https://github.com/vercel/next.js/security/advisories/GHSA-8h8q-6873-q5fj)| High| Denial of service in Server Components| **WAF rules in place:** `2694f1610c0b471393b21aef102ec699`, `aaede80b4d414dc89c443cea61680354`
CIS is investigating additional managed WAF coverage
[`GHSA-267c-6grr-h53f`](https://github.com/vercel/next.js/security/advisories/GHSA-267c-6grr-h53f)| High| Middleware bypass via segment-prefetch routes| CIS is investigating if this can be safely and effectively mitigated by a managed WAF rule
[`GHSA-mg66-mrh9-m8jx`](https://github.com/vercel/next.js/security/advisories/GHSA-mg66-mrh9-m8jx)| High| Denial of service via connection exhaustion in Cache Components| CIS is investigating if this can be safely and effectively mitigated by a managed WAF rule
[`GHSA-492v-c6pp-mqqv`](https://github.com/vercel/next.js/security/advisories/GHSA-492v-c6pp-mqqv)| High| Middleware bypass via dynamic route parameter injection| Not possible to safely enable a managed WAF rule without potentially breaking application behavior
[`GHSA-c4j6-fc7j-m34r`](https://github.com/vercel/next.js/security/advisories/GHSA-c4j6-fc7j-m34r)| High| SSRF via WebSocket upgrades| Not possible to safely enable a managed WAF rule without potentially breaking application behavior
[`GHSA-36qx-fr4f-26g5`](https://github.com/vercel/next.js/security/advisories/GHSA-36qx-fr4f-26g5)| High| Middleware bypass in Pages Router i18n| Custom WAF rule possible; global managed rule could potentially break application behavior
[`GHSA-ffhc-5mcf-pf4q`](https://github.com/vercel/next.js/security/advisories/GHSA-ffhc-5mcf-pf4q)| Moderate| XSS via CSP nonces| Custom WAF rule possible; global managed rule could potentially break application behavior
[`GHSA-gx5p-jg67-6x7h`](https://github.com/vercel/next.js/security/advisories/GHSA-gx5p-jg67-6x7h)| Moderate| XSS in `beforeInteractive` scripts| Not possible to safely enable a managed WAF rule without potentially breaking application behavior
[`GHSA-h64f-5h5j-jqjh`](https://github.com/vercel/next.js/security/advisories/GHSA-h64f-5h5j-jqjh)| Moderate| Denial of service in Image Optimization API| Custom WAF rule possible; global managed rule could potentially break application behavior
[`GHSA-wfc6-r584-vfw7`](https://github.com/vercel/next.js/security/advisories/GHSA-wfc6-r584-vfw7)| Moderate| Cache poisoning in RSC responses| Custom WAF rule possible; global managed rule could potentially break application behavior
[`GHSA-vfv6-92ff-j949`](https://github.com/vercel/next.js/security/advisories/GHSA-vfv6-92ff-j949)| Low| Cache poisoning via RSC cache-busting collisions| Not possible to safely enable a managed WAF rule without potentially breaking application behavior
[`GHSA-3g8h-86w9-wvmq`](https://github.com/vercel/next.js/security/advisories/GHSA-3g8h-86w9-wvmq)| Low| Middleware redirect cache poisoning| Custom WAF rule possible; global managed rule could potentially break application behavior


## WAF - WAF Release - 2026-05-07 - Emergency
**Published on:** Thu, 07 May 2026 00:00:00 GMT

This emergency release introduces a new rule to detect Next.js App Router middleware and proxy bypass attempts via segment-prefetch routes (CVE-2026-44575).

**Key Findings**

CVE-2026-44575: Next.js Middleware / Proxy Bypass in App Router Applications via Segment-Prefetch Routes

Successful exploitation allows unauthenticated attackers to bypass middleware or proxy-based authorization checks in affected Next.js App Router applications. This leads to unauthorized access to protected content, potential exposure of sensitive application data, and compromise of application security boundaries.

We strongly recommend upgrading to Next.js 15.5.16 or 16.2.5 (or later) immediately to address the underlying vulnerability. If you cannot upgrade immediately, enforce authorization in the underlying route or page logic instead of relying solely on middleware.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 1de95bf6d6374e1099854278e77e4a53 | N/A| Next.js - Middleware Bypass via Invalid RSC Header - CVE:CVE-2026-44575| N/A| Disabled| This is a new detection.


## WAF - WAF Release - 2026-05-04
**Published on:** Mon, 04 May 2026 00:00:00 GMT

This week's release focuses on new detections to expand coverage across command injection, SQL injection, PHP object injection, remote code execution, and XSS attack vectors.

**Key Findings**

  * Existing rule enhancements have been deployed to improve detection resilience against broad classes of web attacks and strengthen behavioral coverage.



**Continuous Rule Improvements**

We are continuously refining our managed rules to provide more resilient protection and deeper insights into attack patterns. To ensure an optimal security posture, we recommend consistently monitoring the Security Events dashboard and adjusting rule actions as these enhancements are deployed.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 607ec27233b54beb8b89386ef0884a68 | N/A| XSS, HTML Injection - Object Tag - Body (beta)| Log| Block| This is a new detection. This rule is merged into the original rule "XSS, HTML Injection - Object Tag" (ID: e9e3ac45a6d842f1a132fbf70c14e284 ).
CIS Managed Ruleset| 0087c27420c54168a10bc05eff012303 | N/A| XSS, HTML Injection - Object Tag - Headers| Log| Block| This is a new detection. The rule previously known as "XSS, HTML Injection - Object Tag - Headers (beta)" is now renamed to "XSS, HTML Injection - Object Tag - Headers".
CIS Managed Ruleset| 38dc97853ebf40ed9476ec7816f921d9 | N/A| XSS, HTML Injection - Object Tag - URI| Log| Block| This is a new detection. The rule previously known as "XSS, HTML Injection - Object Tag - URI (beta)" is now renamed to "XSS, HTML Injection - Object Tag - URI".
CIS Managed Ruleset| 963cb530f72d4c75b2ae7befdc90d21a | N/A| Command Injection - Generic 9 - Body Vector - Beta| N/A| Disabled| This is a new detection. This rule is merged into the original rule "Command Injection - Generic 9 - Body Vector" (ID: 155bb67d1061479e995a38510677175f )
CIS Managed Ruleset| 6ac1b6dfe22449a798cc7021f8960375 | N/A| Command Injection - Generic 9 - Header Vector - Beta| N/A| Disabled| This is a new detection. This rule is merged into the original rule "Command Injection - Generic 9 - Header Vector" (ID: b31c34a7b29b4aaf9be6883d1eb7a999 )
CIS Managed Ruleset| 47a9b66dd73a4a558590c4bdef47a800 | N/A| Command Injection - Generic 9 - URI Vector - Beta| N/A| Disabled| This is a new detection. This rule is merged into the original rule "Command Injection - Generic 9 - URI Vector" (ID: 54ad0465c30d4cd2ac7a707197321c6c )
CIS Managed Ruleset| d2ae4a8093f245a1b9de71bbbeebf804 | N/A| Command Injection - Sleep - Body| N/A| Disabled| This is a new detection. The rule previously known as "Command Injection

  * Sleep" is now renamed to "Command Injection - Sleep - Body".


CIS Managed Ruleset| da91868c0d3d44afb846e7830d257566 | N/A| Command Injection - Sleep - Headers| N/A| Disabled| This is a new detection.
CIS Managed Ruleset| 04863c61e982464b91778f051856fe86 | N/A| Command Injection - Sleep - URI| N/A| Disabled| This is a new detection.
CIS Managed Ruleset| 9dc1a0b8dbb7425db619309be6e43c37 | N/A| Fortinet FortiSandbox - Command Injection - CVE:CVE-2026-39808| Log| Block| This is a new detection.
CIS Managed Ruleset| b84c10f5a8f84800905932dc88118795 | N/A| Remote Code Execution - Common Bash Bypass - Headers| N/A| Disabled| This is a new detection.
CIS Managed Ruleset| f496c40011f14bfdb5f55ec79299d53b | N/A| Remote Code Execution - Common Bash Bypass - URI| N/A| Disabled| This is a new detection.
CIS Managed Ruleset| a5f75abac2664554a984d061b0bf33f9 | N/A| Remote Code Execution - Common Bash Bypass - Body - Beta| N/A| Disabled| This is a new detection. This rule is merged into the original rule "Remote Code Execution - Common Bash Bypass Body" (ID: 6e2f7a696ea74c979e7d069cefb7e5b9 ). The rule previously known as "Remote Code Execution - Common Bash Bypass Beta" is now renamed to "Remote Code Execution - Common Bash Bypass Body".
CIS Managed Ruleset| bbb31a886ab54f6c8cdd220d33bfe8b9 | N/A| PHP Object Injection - 2 - Body - Beta| N/A| Disabled| This is a new detection. This rule is merged into the original rule "PHP Object Injection - 2" (ID: 8ef3c3f91eef46919cc9cb6d161aafdc )
CIS Managed Ruleset| e199688ab69746c88c33457f29552387 | N/A| PHP Object Injection - 2 - Headers| N/A| Disabled| This is a new detection.
CIS Managed Ruleset| eb33d40e96c54e929af6ed9c8104f4c5 | N/A| PHP Object Injection - 2 - URI| N/A| Disabled| This is a new detection.
CIS Managed Ruleset| 76b15b7b122a4be6a40d8aa96a46201e | N/A| SQLi - DROP - 2 - Beta| N/A| Disabled| This is a new detection. This rule is merged into the original rule "SQLi - DROP - 2" (ID: a967a167874b42b6898be46e48ac2221 )
CIS Managed Ruleset| e24b2ef4a5c54f97a62db7a68b7f85ee | N/A| SQLi - DROP - 2 - Headers| N/A| Disabled| This is a new detection.
CIS Managed Ruleset| 51123f35f1d249358aea8fb11546b5f0 | N/A| SQLi - DROP - 2 - URI| N/A| Disabled| This is a new detection.
CIS Managed Ruleset| d86d8873310d41f2877458a91e053dce | N/A| SmarterMail - Remote Code Execution - CVE:CVE-2026-24423| Log| Block| This is a new detection.
CIS Managed Ruleset| 00da180570d34b5bae2121acd0023a36 | N/A| SQLi - SELECT Expression - Body| Block| Disabled| Action changed
CIS Managed Ruleset| c46d9097c9ef419aa4d9f10626cc211f | N/A| SQLi - String Concatenation - URI| Block| Disabled| Action changed


## WAF - WAF Release - 2026-04-30 - Emergency
**Published on:** Thu, 30 Apr 2026 00:00:00 GMT

This emergency release introduces a new rule to block a cPanel & WHM Authentication Bypass related to CVE-2026-41940.

**Key Findings**

  * CVE-2026-41940: A critical authentication bypass vulnerability in cPanel & WHM allows unauthenticated remote attackers to bypass authentication mechanisms and gain unauthorized administrative access to the web hosting control panel. This vulnerability affects the session validation logic, enabling attackers to craft malicious requests that circumvent normal authentication checks.



**Impact**

Successful exploitation allows unauthenticated attackers to gain administrative control over affected cPanel & WHM installations. This leads to complete server compromise, potential theft or manipulation of hosted data, and significant service disruption across managed environments.

We strongly recommend applying official vendor patches for cPanel & WHM immediately to address the underlying vulnerability.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| fb29b1b660864285a5ebac86eb2b9e2f | N/A| cPanel - Auth Bypass - CVE:CVE-2026-41940| N/A| Block| This is a new detection.


## WAF - WAF Release - 2026-04-27
**Published on:** Mon, 27 Apr 2026 00:00:00 GMT

This week's release focuses on new improvements to enhance coverage.

**Key Findings**

  * Existing rule enhancements have been deployed to improve detection resilience against broad classes of web attacks and strengthen behavioral coverage.



**Continuous Rule Improvements**

We are continuously refining our managed rules to provide more resilient protection and deeper insights into attack patterns. To ensure an optimal security posture, we recommend consistently monitoring the Security Events dashboard and adjusting rule actions as these enhancements are deployed.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| d866f980582748568385b94480cec1dd | N/A| PostgreSQL - SQLi - COPY - Beta| Log| Block| This is a new detection. This rule is merged into the original rule "PostgreSQL - SQLi - COPY - Body (ID: 705a6b5569d5472596910e3ce7265a4e ). The rule previously known as "PostgreSQL - SQLi - COPY" is now renamed to "PostgreSQL - SQLi - COPY - Body".
CIS Managed Ruleset| 71d133c374d94559aa9fdf042903de89 | N/A| PostgreSQL - SQLi - COPY - Headers| Log| Block| This is a new detection.
CIS Managed Ruleset| 9f1b1b7fd28a401b9d5c172d1036cfa6 | N/A| PostgreSQL - SQLi - COPY - URI| Log| Block| This is a new detection.
CIS Managed Ruleset| 8e40416659334b8ba789365755ff389e | N/A| SQLi - AND/OR MAKE_SET/ELT - Beta| Log| Block| This is a new detection. This rule is merged into the original rule "SQLi - AND/OR MAKE_SET/ELT - Body" (ID: 0f41a593c8fe42c38a26f709252d3934 ). The rule previously known as "SQLi - AND/OR MAKE_SET/ELT" is now renamed to "SQLi - AND/OR MAKE_SET/ELT - Body".
CIS Managed Ruleset| 1e0d4372ee1e41b9804b2d5c346487f9 | N/A| SQLi - AND/OR MAKE_SET/ELT - Headers| Log| Block| This is a new detection.
CIS Managed Ruleset| d2c961a164a64cf6b871c9511ac6ceca | N/A| SQLi - AND/OR MAKE_SET/ELT - URI| Log| Block| This is a new detection.
CIS Managed Ruleset| 4dacc0e6f32d4c5da3c2293edd471337 | N/A| SQLi - Common Patterns - Beta| Log| Block| This is a new detection. This rule is merged into the original rule "SQLi - Common Patterns - Body" (ID: 98f746d07a6d48ab9dae669acb5d0b9b ). The rule previously known as "SQLi - Common Patterns" is now renamed to "SQLi - Common Patterns - Body".
CIS Managed Ruleset| 53a374379f2e41e9934791c1975c07b7 | N/A| SQLi - Common Patterns - Headers| Log| Block| This is a new detection.
CIS Managed Ruleset| 9efedebfc371443f9fe7308605b1b06b | N/A| SQLi - Common Patterns - URI| Log| Block| This is a new detection.
CIS Managed Ruleset| d53a791496d64700870334f4dd0ba3c7 | N/A| SQLi - Equation - Beta| Log| Block| This is a new detection. This rule is merged into the original rule "SQLi - Equation - Body" (ID: e7691e1e4f4d4769909f3df6c2eb3e7f ). The rule previously known as "SQLi - Equation" is now renamed to "SQLi - Equation - Body".
CIS Managed Ruleset| 46efbd3496e64c3f902ad33d3d1c2384 | N/A| SQLi - Equation - Headers| Log| Block| This is a new detection.
CIS Managed Ruleset| 46b937649a424b7ead90f6d0e1149ea6 | N/A| SQLi - Equation - URI| Log| Block| This is a new detection.
CIS Managed Ruleset| 04d9182545f54ba8a4fa29fe205adbb0 | N/A| SQLi - AND/OR Digit Operator Digit - Beta| Log| Block| This is a new detection. This rule is merged into the original rule "SQLi - AND/OR Digit Operator Digit - Body" (ID: 762dd334ed0b4273816e3ff13893c564 ). The rule previously known as "SQLi - AND/OR Digit Operator Digit" is now renamed to "SQLi - AND/OR Digit Operator Digit - Body".
CIS Managed Ruleset| a24e7c15503948bc8766481aad2abbaa | N/A| SQLi - AND/OR Digit Operator Digit - Headers| Log| Block| This is a new detection.
CIS Managed Ruleset| 0c55eb362df64f92a85aa46753acbc0d | N/A| SQLi - AND/OR Digit Operator Digit - URI| Log| Block| This is a new detection.
CIS Managed Ruleset| 18c9879b7e184c559d23c1652b45a97d | N/A| SQLi - Benchmark Function - Beta| Log| Block| This is a new detection. This rule is merged into the original rule "SQLi - Benchmark Function - Body" (ID: ac4e9ebfb43a4f3998f6072d2ebc44ad ). The rule previously known as "SQLi - Benchmark Function" is now renamed to "SQLi - Benchmark Function - Body".
CIS Managed Ruleset| 2adbc36c52324efcb4681b829889aadc | N/A| SQLi - Benchmark Function - Headers| Log| Block| This is a new detection.
CIS Managed Ruleset| 69564af3bc54406080deed72491b28e9 | N/A| SQLi - Benchmark Function - URI| Log| Block| This is a new detection.
CIS Managed Ruleset| 94b1646f0b0b46ec9b96f7742aa649de | N/A| SQLi - Comparison - Beta| Log| Block| This is a new detection. This rule is merged into the original rule "SQLi - Comparison - Body" (ID: 8166da327a614849bfa29317e7907480 ). The rule previously known as "SQLi - Comparison" is now renamed to "SQLi - Comparison - Body".
CIS Managed Ruleset| 455ce87681bd4200bf53456c39e3e013 | N/A| SQLi - Comparison - Headers| Log| Block| This is a new detection.
CIS Managed Ruleset| 8152816062ed47f69be0f907f4bdb492 | N/A| SQLi - Comparison - URI| Log| Block| This is a new detection.
CIS Managed Ruleset| d5afd403a0544248b829fe5da1ff3b34 | N/A| SQLi - String Concatenation - Body - Beta| Log| Block| This is a new detection. This rule is merged into the original rule "SQLi - String Concatenation - Headers" (ID: 3b0c61407d0b4f7d87e516472116d2fe ).The rule previously known as "SQLi - String Concatenation - Headers" is now renamed to "SQLi - String Concatenation - Body".
CIS Managed Ruleset| cb0ec290ee454138abe18b750d0e6c3b | N/A| SQLi - String Concatenation - Headers| Log| Block| This is a new detection.(Former Id was 380099df2bb2469c91ebbb7b846d1940 )
CIS Managed Ruleset| c46d9097c9ef419aa4d9f10626cc211f | N/A| SQLi - String Concatenation - URI| Log| Block| This is a new detection. (Former Id was bd19397228404b85aa3797238fae8c84 )
CIS Managed Ruleset| 6542d36980cf4018b4d5e2bfeacc78ab | N/A| SQLi - SELECT Expression - Beta| Log| Block| This is a new detection. This rule is merged into the original rule "SQLi - SELECT Expression - Body" (ID: 00da180570d34b5bae2121acd0023a36 ). The rule previously known as "SQLi - SELECT Expression" is now renamed to "SQLi - SELECT Expression - Body".
CIS Managed Ruleset| 4073f7b575ff45dfb7621b43630bb223 | N/A| SQLi - SELECT Expression - Headers| Log| Block| This is a new detection.
CIS Managed Ruleset| 2721e3184d50466ea637e9afdcd6efb5 | N/A| SQLi - SELECT Expression - URI| Log| Block| This is a new detection.
CIS Managed Ruleset| 7ecca84c08aa4aad9b5a7bda18c47cea | N/A| SQLi - ORD and ASCII - Beta| Log| Block| This is a new detection. This rule is merged into the original rule "SQLi - ORD and ASCII- Body" (ID: 2fc38b34a9d744d2a3cbcc41d0d207f9 ). The rule previously known as "SQLi - ORD and ASCII" is now renamed to "SQLi - ORD and ASCII- Body".
CIS Managed Ruleset| f6d10e10c9514eb49dcc2122bdb1618f | N/A| SQLi - ORD and ASCII - URI| Log| Block| This is a new detection.
CIS Managed Ruleset| 60704f5c5513425c94cf77031d0906b6 | N/A| SQLi - ORD and ASCII - Headers| Log| Block| This is a new detection.
CIS Managed Ruleset| 700613b191d3479ea2782b4e9fe4eff5 | N/A| SQLi - Destructive Operations| Log| Block| This is a new detection.


## WAF - WAF Release - 2026-04-21
**Published on:** Tue, 21 Apr 2026 00:00:00 GMT

This week's release introduces a new detection for a Remote Code Execution (RCE) vulnerability in Apache ActiveMQ (CVE-2026-34197) and an updated signature for Magento 2 - Unrestricted File Upload. Alongside these detections, we are continuing our work on rule refinements to provide deeper security insights for our customers.

**Key Findings**

  * Apache ActiveMQ (CVE-2026-34197): A vulnerability in Apache ActiveMQ allows an unauthenticated, remote attacker to execute arbitrary code. This flaw occurs during the processing of specially crafted network packets, leading to potential full system compromise.

  * Magento 2 - Unrestricted File Upload - 2: This is a follow-up enhancement to our existing protections for Magento and Adobe Commerce.




**Impact**

Successful exploitation of these vulnerabilities could allow unauthenticated attackers to execute arbitrary code or gain full administrative control over affected servers. We strongly recommend applying official vendor patches for Apache ActiveMQ and Magento to address the underlying vulnerabilities.

**Continuous Rule Improvements**

We are continuously refining our managed rules to provide more resilient protection and deeper insights into attack patterns. To ensure an optimal security posture, we recommend consistently monitoring the Security Events dashboard and adjusting rule actions as these enhancements are deployed.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| ff8df24181aa4573a81be531ee159e2e | N/A| Command Injection - Generic 8 - uri| Log| Block| This is a new detection. Previous description was "Command Injection - Generic 8 - uri - Beta"
CIS Managed Ruleset| 9429b63c137247faadeb8a29a15308cf | N/A| Command Injection - Generic 8 - body - Beta| Disabled| Disabled| This is a new detection. This rule is merged into the original rule "Command Injection - Generic 8 - body" (ID: 5b3ce84c099040c6a25cee2d413592e2 ). The rule previously known as "Command Injection - Generic 8" is now renamed to "Command Injection - Generic 8 - body".
CIS Managed Ruleset| 85aaf5db9e0c4237b87e837e958047ed | N/A| MySQL - SQLi - Executable Comment - Beta| Log| Block| This is a new detection. This rule is merged into the original rule "MySQL - SQLi - Executable Comment - Body" (ID: 8629bb58defe4193ab4d493c7bd2d8fa ) The rule previously known as "MySQL - SQLi - Executable Comment" is now renamed to "MySQL - SQLi - Executable Comment - Body".
CIS Managed Ruleset| d19cd574c4644952881a6f3a582cc559 | N/A| MySQL - SQLi - Executable Comment - Headers| Log| Block| This is a new detection.
CIS Managed Ruleset| 407f9ec8a17348dfba3b9450a16639d3 | N/A| MySQL - SQLi - Executable Comment - URI| Log| Block| This is a new detection.
CIS Managed Ruleset| d07e6dbf15664b99b37b0d2544f24211 | N/A| Magento 2 - Unrestricted file upload - 2| Log| Block| This is a new detection.
CIS Managed Ruleset| 26ef21cb197b44fc8a98b7cebf170a17 | N/A| Apache ActiveMQ - Remote Code Execution - CVE:CVE-2026-34197| Log| Block| This is a new detection.
CIS Managed Ruleset| 7f7bc3d28a8e43bf97bd15d68c2ac1a7 | N/A| SQLi - Sleep Function - Beta| Log| Block| This is a new detection. This rule is merged into the original rule "SQLi - Sleep Function" (ID: 2c333735f7b24566b17cb64ef77e8d54 )
CIS Managed Ruleset| 3872e5638bdf4bf0943a80394dacaeb8 | N/A| SQLi - Sleep Function - Headers| Log| Block| This is a new detection.
CIS Managed Ruleset| bebce8fadfa94ccab09eb74fed4c9ece | N/A| SQLi - Sleep Function - URI| Log| Block| This is a new detection.
CIS Managed Ruleset| 7a40eed5a8654a50a2598a821dfa64df | N/A| SQLi - Probing - uri| Log| Block| This is a new detection.
CIS Managed Ruleset| 15c6b2ce033949b2a1a9f9454c62e2e7 | N/A| SQLi - Probing - header| Log| Block| This is a new detection.
CIS Managed Ruleset| fc9d800b7a724181af8d5650aab28ea1 | N/A| SQLi - Probing - body| Disabled| Disabled| This is a new detection. This rule is merged into the original rule "SQLi - Probing" (ID: 2c20b5e8684043f48620ff77b4026c88 )
CIS Managed Ruleset| 945c5aa9f45141dd872d7ec920999be0 | N/A| SQLi - Probing 2 | Disabled| Disabled| This rule had duplicate detection logic and has been deprecated.
CIS Managed Ruleset| f1771273700342758e73cf16d7aa0008 | N/A| SQLi - UNION in MSSQL - Body| Disabled| Disabled| This rule has been renamed to differentiate from "SQLi - UNION in MSSQL" (ID: ef7db598c7654c729d9db56fee5e35fd ) and contains updated rule logic.
CIS Managed Ruleset| 3ffd242b4ba242ca965022d3a67d8561 | N/A| SQLi - UNION - 3| Disabled| Disabled| This rule had duplicate detection logic and has been deprecated.
CIS Managed Ruleset| 5e69d599ad634c81abe36a5f0af34bba | N/A| XSS, HTML Injection - Embed Tag - URI| Disabled| Disabled| This is a new detection.
CIS Managed Ruleset| 2635275641bf44d4bad6a2e170282f38 | N/A| XSS, HTML Injection - Embed Tag - Headers| Log| Block| This is a new detection.
CIS Managed Ruleset| b3d033ea9f364574b0a2ec4223f4d718 | N/A| XSS, HTML Injection - IFrame Tag - Src and Srcdoc Attributes - Headers| Log| Disabled| This is a new detection.
CIS Managed Ruleset| 76c37816ef5c4997ab2080a36978def1 | N/A| XSS, HTML Injection - Link Tag - Headers| Log| Disabled| This is a new detection.
CIS Managed Ruleset| 7d6757e8a28f4853a72b4ce6ebd81645 | N/A| XSS, HTML Injection - Link Tag - URI| Disabled| Disabled| This is a new detection.


## WAF - WAF Release - 2026-04-15
**Published on:** Wed, 15 Apr 2026 00:00:00 GMT

This week's release introduces a new detection for a critical Remote Code Execution (RCE) vulnerability in Mesop (CVE-2026-33057), alongside protections for high-impact vulnerabilities in Cisco Secure Firewall Management Center (CVE-2026-20079) and FortiClient EMS (CVE-2026-21643). Additionally, this release includes an update to our existing React Server DoS coverage to address recently identified resource exhaustion vectors (CVE-2026-23869).

**Key Findings**

  * Cisco Secure FMC (CVE-2026-20079): A vulnerability in the web-based management interface of Cisco Secure Firewall Management Center (FMC) that allows an unauthenticated, remote attacker to execute arbitrary commands or bypass security filters.

  * FortiClient EMS (CVE-2026-21643): A critical vulnerability in the FortiClient EMS permitting unauthorized access or administrative configuration manipulation via crafted HTTP requests.

  * Mesop (CVE-2026-33057): A vulnerability in the Mesop Python-based UI framework where unauthenticated attackers can execute arbitrary code by sending specially crafted, Base64-encoded payloads in the request body.




**Impact**

Successful exploitation of these vulnerabilities could allow unauthenticated attackers to execute arbitrary code, gain administrative control over network management infrastructure, or trigger server-side resource exhaustion. Administrators are strongly encouraged to apply official vendor updates.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 7767165cda1841b8b6e5abb7aef9415b | N/A| Cisco Secure FMC - RCE via upgradeReadinessCall - CVE:CVE-2026-20079| Log| Block| This is a new detection.
CIS Managed Ruleset| 3dd0b2b6f45c4bc08e49bf27ee7be621 | N/A| FortiClient EMS - Pre-Auth SQL Injection - CVE:CVE-2026-21643| Log| Block| This is a new detection.
CIS Managed Ruleset| 0e3a6828906c4b24bad318a9c953a72b | N/A| Mesop - Remote Code Execution - Base64 Payload - CVE:CVE-2026-33057| Log| Block| This is a new detection.
CIS Managed Ruleset| d95aa5410d1b4e98bf7a59d150c08f6f | N/A| React Server - DOS - CVE:CVE-2026-23864 - 1 - Beta| Log| Block| This rule has been merged into the original rule "React Server - DOS - CVE:CVE-2026-23864 - 1" (ID: aaede80b4d414dc89c443cea61680354 )
CIS Managed Ruleset| 7d6757e8a28f4853a72b4ce6ebd81645 | N/A| XSS, HTML Injection - Link Tag - URI (beta)| N/A| Disabled| This is a new detection.
CIS Managed Ruleset| 5e69d599ad634c81abe36a5f0af34bba | N/A| XSS, HTML Injection - Embed Tag - URI (beta)| N/A| Disabled| This is a new detection.


## WAF - Email obfuscation decode script is now non-render-blocking
**Published on:** Tue, 14 Apr 2026 00:00:00 GMT

The decode script injected by [Email Address Obfuscation](https://developers.cloudflare.com/waf/tools/scrape-shield/email-address-obfuscation/) now loads with the `defer` attribute. This means the script no longer blocks page rendering. It downloads in parallel with HTML parsing and executes after the document is fully parsed, before the `DOMContentLoaded` event.

This improves page loading performance, contributing to better Core Web Vitals, for all zones with Email Address Obfuscation on. No action is required.

If you have custom JavaScript that depends on email addresses being decoded at a specific point during page load, note that the decode script now executes after HTML parsing completes rather than inline during parsing.


## WAF - WAF Release - 2026-04-07
**Published on:** Tue, 07 Apr 2026 00:00:00 GMT

This week's release introduces new detections for a critical Remote Code Execution (RCE) vulnerability in MCP Server (CVE-2026-23744), alongside targeted protection for an authentication bypass vulnerability in SolarWinds products (CVE-2025-40552). Additionally, this release includes a new generic detection rule designed to identify and block Cross-Site Scripting (XSS) injection attempts leveraging "OnEvent" handlers within HTTP cookies.

**Key Findings**

  * MCP Server (CVE-2026-23744): A vulnerability in the Model Context Protocol (MCP) server implementation where malformed input payloads can trigger a memory corruption state, allowing for arbitrary code execution.

  * SolarWinds (CVE-2025-40552): A critical flaw in the authentication module allows unauthenticated attackers to bypass security filters and gain unauthorized access to the management console due to improper identity token validation.

  * XSS OnEvents Cookies: This generic rule identifies malicious event handlers (such as onload or onerror) embedded within HTTP cookie values.




**Impact**

Successful exploitation of the MCP Server and SolarWinds vulnerabilities could allow unauthenticated attackers to execute arbitrary code or gain administrative control, leading to a full system takeover. Additionally, the new generic XSS detection prevents attackers from leveraging browser event handlers in cookies to hijack user sessions or execute malicious scripts.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 73ae1cf103da4bacaa2e1a610aa410af | N/A| Generic Rules - Command Execution - 5 - Body| Log| Disabled| This is a new detection.
CIS Managed Ruleset| a88a85b0cc5a4bc2abead6289131ec2f | N/A| Generic Rules - Command Execution - 5 - Header| Log| Disabled| This is a new detection.
CIS Managed Ruleset| 28518cdc40544979bbd86720551eb9e5 | N/A| Generic Rules - Command Execution - 5 - URI| Log| Block| This is a new detection.
CIS Managed Ruleset| 1177993d53a1467997002b44d46229eb | N/A| MCP Server - Remote Code Execution - CVE:CVE-2026-23744| Log| Block| This is a new detection.
CIS Managed Ruleset| 3d43cdfbc3c14584942f8bc4a864b9c2 | N/A| XSS - OnEvents - Cookies| Log| Block| This is a new detection.
CIS Managed Ruleset| 41153470df2365192b0df74ca78ad04e | N/A| SQLi - Evasion - Body| Log| Disabled| This is a new detection.
CIS Managed Ruleset| 64d812e6d5844d7c9d7a44a440732d48 | N/A| SQLi - Evasion - Headers| Log| Disabled| This is a new detection.
CIS Managed Ruleset| 50de9369ef7c45928a5dfb34e68a99b5 | N/A| SQLi - Evasion - URI| Log| Disabled| This is a new detection.
CIS Managed Ruleset| 765ffb5c67b94c9589106c843e8143d2 | N/A| SQLi - LIKE 3 - Body| Log| Disabled| This is a new detection.
CIS Managed Ruleset| 5c3dbd4f115e47c781491fcd70e7fb97 | N/A| SQLi - LIKE 3 - URI| Log| Disabled| This is a new detection.
CIS Managed Ruleset| 89fa6027a0334949b1cb2e654c538bd9 | N/A| SQLi - UNION - 2 - Body| Log| Disabled| This is a new detection.
CIS Managed Ruleset| 05946b3458364f1b9d4819d561c439c9 | N/A| SQLi - UNION - 2 - URI| Log| Disabled| This is a new detection.
CIS Managed Ruleset| b2fe5c2a39df4609b6d39908cf33ea10 | N/A| SolarWinds - Auth Bypass - CVE:CVE-2025-40552| Log| Block| This is a new detection.


## WAF - WAF Release - 2026-03-30
**Published on:** Mon, 30 Mar 2026 00:00:00 GMT

This week's release introduces new detections for a critical authentication bypass vulnerability in Fortinet products (CVE-2025-59718), alongside three new generic detection rules designed to identify and block HTTP Parameter Pollution attempts. Additionally, this release includes targeted protection for a high-impact unrestricted file upload vulnerability in Magento and Adobe Commerce.

**Key Findings**

  * CVE-2025-59718: An improper cryptographic signature verification vulnerability in Fortinet FortiOS, FortiProxy, and FortiSwitchManager. This may allow an unauthenticated attacker to bypass the FortiCloud SSO login authentication using a maliciously crafted SAML message, if that feature is enabled on the device.

  * Magento 2 - Unrestricted File Upload: A critical flaw in Magento and Adobe Commerce allows unauthenticated attackers to bypass security checks and upload malicious files to the server, potentially leading to Remote Code Execution (RCE).




**Impact**

Successful exploitation of the Fortinet and Magento vulnerabilities could allow unauthenticated attackers to gain administrative control or deploy webshells, leading to complete server compromise and data theft.







Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 4f7d513cea424c2a853881982f7f95e9 | N/A| Generic Rules - Parameter Pollution - Body| Log| Disabled| This is a new detection.
CIS Managed Ruleset| 60d023f3be414d379428add3319731a4 | N/A | Generic Rules - Parameter Pollution - Header - Form | Log | Disabled | This is a new detection.
CIS Managed Ruleset| 2dde02d792ad41ec8fd65c2bdef262dd | N/A | Generic Rules - Parameter Pollution - URI | Log | Disabled | This is a new detection.
CIS Managed Ruleset| ab8a96ed13034d56a81a79e570a36147 | N/A| Magento 2 - Unrestricted file upload| Log| Block| This is a new detection.
CIS Managed Ruleset| 0a13a38dd81c44688950444e2ffcca9f | N/A| Fortinet FortiCloud SSO - Authentication Bypass - CVE:CVE-2025-59718| Log| Block| This is a new detection.


## WAF - WAF Release - 2026-03-23
**Published on:** Mon, 23 Mar 2026 00:00:00 GMT

This week's release focuses on new improvements to enhance coverage.

**Key Findings**

  * Existing rule enhancements have been deployed to improve detection resilience against broad classes of web attacks and strengthen behavioral coverage.









Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 54ad0465c30d4cd2ac7a707197321c6c | N/A| Command Injection - Generic 9 - URI Vector| Log| Disabled| This is a new detection.
CIS Managed Ruleset| b31c34a7b29b4aaf9be6883d1eb7a999 | N/A | Command Injection - Generic 9 - Header Vector | Log | Disabled | This is a new detection.
CIS Managed Ruleset| 155bb67d1061479e995a38510677175f | N/A | Command Injection - Generic 9 - Body Vector | Log | Disabled | This is a new detection.
CIS Managed Ruleset| 55fb1c76f0304f6a9d935d03479da68f | N/A| PHP, vBulletin, jQuery File Upload - Code Injection, Dangerous File Upload - CVE:CVE-2018-9206, CVE:CVE-2019-17132 (beta)| Log| Block| This rule has been merged into the original rule "PHP, vBulletin, jQuery File Upload - Code Injection, Dangerous File Upload - CVE:CVE-2018-9206, CVE:CVE-2019-17132" (ID: 0f2da91cec674eb58006929e824b817c )


## WAF - WAF Release - 2026-03-12 - Emergency
**Published on:** Thu, 12 Mar 2026 00:00:00 GMT

This week's release introduces new detections for vulnerabilities in Ivanti Endpoint Manager Mobile (CVE-2026-1281 and CVE-2026-1340), alongside a new generic detection rule designed to identify and block Cross-Site Scripting (XSS) injection attempts within the `Content-Security-Policy` (CSP) HTTP request header.

**Key Findings**

  * CVE-2026-1281 & CVE-2026-1340: Ivanti Endpoint Manager Mobile processes HTTP requests through Apache RevwriteMap directives that pass user-controlled input to Bash scripts (`/mi/bin/map-appstore-url` and `/mi/bin/map-aft-store-url`). Bash scripts do not sanitize user input and are vulnerable to shell arithmetic expansion thereby allowing attackers to achieve unauthenticated remote code execution.
  * Generic XSS in CSP Header: This rule identifies malicious payloads embedded within the request's `Content-Security-Policy` header. It specifically targets scenarios where web frameworks or applications trust and extract values directly from the CSP header in the incoming request without sufficient validation. Attackers can provide crafted header values to inject scripts or malicious directives that are subsequently processed by the server.



**Impact**

Successful exploitation of Ivanti EPMM vulnerability allows unauthenticated remote code execution and generic XSS in CSP header allows attackers to inject malicious scripts during page rendering. In environments using server-side caching, this poisoned XSS content can subsequently be cached and automatically served to all visitors.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 5ae86a9bda0c41dbb905132f796ea2f6 | N/A| Ivanti EPMM - Code Injection - CVE:CVE-2026-1281 CVE:CVE-2026-1340| Log| Block| This is a new detection.
CIS Managed Ruleset| 35978af68e374a059e397bf5ee964a8c | N/A| Anomaly:Header:Content-Security-Policy| N/A| Block| This is a new detection.


## WAF - WAF Release - 2026-03-02
**Published on:** Mon, 02 Mar 2026 00:00:00 GMT

This week's release introduces new detections for vulnerabilities in SmarterTools SmarterMail (CVE-2025-52691 and CVE-2026-23760), alongside improvements to an existing Command Injection (nslookup) detection to enhance coverage.

**Key Findings**

  * CVE-2025-52691: SmarterTools SmarterMail mail server is vulnerable to Arbitrary File Upload, allowing an unauthenticated attacker to upload files to any location on the mail server, potentially enabling remote code execution.
  * CVE-2026-23760: SmarterTools SmarterMail versions prior to build 9511 contain an authentication bypass vulnerability in the password reset API permitting unaunthenticated to reset system administrator accounts failing to verify existing password or reset token.



**Impact**

Successful exploitation of these SmarterMail vulnerabilities could lead to full system compromise or unauthorized administrative access to mail servers. Administrators are strongly encouraged to apply vendor patches without delay.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 0f282f3c89614779966faf52966ec6b1 | N/A| SmarterMail - Arbitrary File Upload - CVE-2025-52691| Log| Block| This is a new detection.
CIS Managed Ruleset| 35978af68e374a059e397bf5ee964a8c | N/A| SmarterMail - Authentication Bypass - CVE-2026-23760| Log| Block| This is a new detection.
CIS Managed Ruleset| 4bb099bcd71141d4a35c1aa675b64d99 | N/A| Command Injection - Nslookup - Beta| Log| Block| This rule is merged into the original rule "Command Injection - Nslookup" (ID: f4a310393c564d50bd585601b090ba9a )


## WAF - WAF Release - 2026-02-16
**Published on:** Mon, 16 Feb 2026 00:00:00 GMT

This week’s release introduces new detections for CVE-2025-68645 and CVE-2025-31125.

**Key Findings**

  * CVE-2025-68645: A Local File Inclusion (LFI) vulnerability in the Webmail Classic UI of Zimbra Collaboration Suite (ZCS) 10.0 and 10.1 allows unauthenticated remote attackers to craft requests to the `/h/rest` endpoint, improperly influence internal dispatching, and include arbitrary files from the WebRoot directory.
  * CVE-2025-31125: Vite, the JavaScript frontend tooling framework, exposes content of non-allowed files via `?inline&import` when its development server is network-exposed, enabling unauthorized attackers to read arbitrary files and potentially leak sensitive information.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 695d76ff756844d384cab548833761f7 | N/A| Zimbra - Local File Inclusion - CVE:CVE-2025-68645| Log| Block| This is a new detection.
CIS Managed Ruleset| 38fff9f3deba46a2abc10a8f950ed8c8 | N/A| Vite - WASM Import Path Traversal - CVE:CVE-2025-31125| Log| Block| This is a new detection.


## WAF - WAF Release - 2026-02-10
**Published on:** Tue, 10 Feb 2026 00:00:00 GMT

This week’s release changes the rule action from BLOCK to Disabled for Anomaly:Header:User-Agent - Fake Google Bot.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| ce11be543594412bb4bb92516aa0bef8 | N/A| Anomaly:Header:User-Agent - Fake Google Bot| Enabled| Disabled| We are changing the action for this rule from BLOCK to Disabled


## WAF - WAF Release - 2026-02-02
**Published on:** Mon, 02 Feb 2026 00:00:00 GMT

This week’s release introduces new detections for CVE-2025-64459 and CVE-2025-24893.

**Key Findings**

  * CVE-2025-64459: Django versions prior to 5.1.14, 5.2.8, and 4.2.26 are vulnerable to SQL injection via crafted dictionaries passed to QuerySet methods and the `Q()` class.
  * CVE-2025-24893: XWiki allows unauthenticated remote code execution through crafted requests to the SolrSearch endpoint, affecting the entire installation.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 7a47683eacce4abd870ab2c630698ff3 | N/A| XWiki - Remote Code Execution - CVE:CVE-2025-24893 2| Log| Block| This is a new detection.
CIS Managed Ruleset| ad5c52f6ca334ef4a844e5e5da8ba7e6 | N/A| Django SQLI - CVE:CVE-2025-64459| Log| Block| This is a new detection.
CIS Managed Ruleset| 8f0d5c98bd24460a9305a1558d667511 | N/A| NoSQL, MongoDB - SQLi - Comparison - 2| Block| Block| Rule metadata description refined. Detection unchanged.


## WAF - WAF Release - 2026-01-26
**Published on:** Mon, 26 Jan 2026 00:00:00 GMT

This week’s release introduces new detections for denial-of-service attempts targeting React CVE-2026-23864 (<https://www.cve.org/CVERecord?id=CVE-2026-23864>).

**Key Findings**

  * CVE-2026-23864 (<https://www.cve.org/CVERecord?id=CVE-2026-23864>) affects `react-server-dom-parcel`, `react-server-dom-turbopack`, and `react-server-dom-webpack` packages.
  * Attackers can send crafted HTTP requests to Server Function endpoints, causing server crashes, out-of-memory exceptions, or excessive CPU usage.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| aaede80b4d414dc89c443cea61680354 | N/A| React Server - DOS - CVE:CVE-2026-23864 - 1| N/A| Block| This is a new detection.
CIS Managed Ruleset| 3e93c9faaafa447c83a525f2dcdffcf8 | N/A| React Server - DOS - CVE:CVE-2026-23864 - 2| N/A| Block| This is a new detection.
CIS Managed Ruleset| 930020d567684f19b05fb35b349edbc6 | N/A| React Server - DOS - CVE:CVE-2026-23864 - 3| N/A| Block| This is a new detection.


## WAF - WAF Release - 2026-01-20
**Published on:** Tue, 20 Jan 2026 00:00:00 GMT

This week's release focuses on improvements to existing detections to enhance coverage.

**Key Findings**

  * Existing rule enhancements have been deployed to improve detection resilience against SQL injection.






Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| a291bd530fa346d18cc1ce5a68d90c8f | N/A| SQLi - Comment - Beta| Log| Block| This rule is merged into the original rule "SQLi - Comment" (ID: 42c424998d2a42c9808ab49c6d8d8fe4 )
CIS Managed Ruleset| da289f9e692e4f5397d915fbfaa045cf | N/A | SQLi - Comparison - Beta | Log | Block | This rule is merged into the original rule "SQLi - Comparison" (ID: 8166da327a614849bfa29317e7907480 )


## WAF - WAF Release - 2026-01-15
**Published on:** Thu, 15 Jan 2026 00:00:00 GMT

This week's release focuses on improvements to existing detections to enhance coverage.

**Key Findings**

  * Existing rule enhancements have been deployed to improve detection resilience against SQL Injection.






Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| eb3f44c07266448b9fa54ee7ad7dad3e | N/A| SQLi - String Function - Beta| Log| Block| This rule is merged into the original rule "SQLi - String Function" (ID: 63e03eecddfc4b3fb0cad587d32b798c )
CIS Managed Ruleset| adf076af09b2484ca9e7881f9e553ad3 | N/A | SQLi - Sub Query - Beta | Log | Block | This rule is merged into the original rule "SQLi - Sub Query" (ID: 6ec5ecf52c094330aff99a38743e66b1 )


## WAF - WAF Release - 2026-01-12
**Published on:** Mon, 12 Jan 2026 00:00:00 GMT

This week's release focuses on improvements to existing detections to enhance coverage.

**Key Findings**

  * Existing rule enhancements have been deployed to improve detection resilience against SQL Injection.






Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 72963b917ef74697b5bde02f48a1841a | N/A| SQLi - AND/OR MAKE_SET/ELT - Beta| Log| Block| This rule is merged into the original rule "SQLi - AND/OR MAKE_SET/ELT" (ID: 0f41a593c8fe42c38a26f709252d3934 )
CIS Managed Ruleset| adf076af09b2484ca9e7881f9e553ad3 | N/A | SQLi - Benchmark Function - Beta | Log | Block | This rule is merged into the original rule "SQLi - Benchmark Function" (ID: ac4e9ebfb43a4f3998f6072d2ebc44ad )


## WAF - WAF Release - 2025-12-18
**Published on:** Thu, 18 Dec 2025 00:00:00 GMT

This week's release focuses on improvements to existing detections to enhance coverage.

**Key Findings**

  * Existing rule enhancements have been deployed to improve detection resilience against broad classes of web attacks and strengthen behavioral coverage.









Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 6429f7386b1546cf9dfce631be5ec20c | N/A| Atlassian Confluence - Code Injection - CVE:CVE-2021-26084 - Beta| Log| Block| This rule is merged into the original rule "Atlassian Confluence - Code Injection - CVE:CVE-2021-26084" (ID: e8c550810618437c953cf3a969e0b97a )
CIS Managed Ruleset| 9108ddb347b3497e9f9351640d9206e3 | N/A | PostgreSQL - SQLi - Copy - Beta | Log | Block | This rule is merged into the original rule "PostgreSQL - SQLi - COPY" (ID: 705a6b5569d5472596910e3ce7265a4e )
CIS Managed Ruleset| cb687d73cc954092b58b90b00cd00ba7 | N/A | Generic Rules - Command Execution - Body | Log | Disabled | This is a new detection.
CIS Managed Ruleset| bf30657ffa2a424cbf6570dbcd679ad4 | N/A| Generic Rules - Command Execution - Header| Log| Disabled| This is a new detection.
CIS Managed Ruleset| 6df040f716194070a242967cfd181fb3 | N/A| Generic Rules - Command Execution - URI| Log| Disabled| This is a new detection.
CIS Managed Ruleset| 39a4fdc37be948709fa7492e7a95bc3a | N/A| SQLi - Tautology - URI - Beta| Log| Block| This rule is merged into the original rule "SQLi - Tautology - URI" (ID: 4c580ea1b5174183b7f5e940b3de2e0a )
CIS Managed Ruleset| 810e0ffe1dd84e67b159129b432ac90d | N/A| SQLi - WaitFor Function - Beta| Log| Block| This rule is merged into the original rule "SQLi - WaitFor Function" (ID: b16fe708799441dea3049a99d5faba59 )
CIS Managed Ruleset| 80690005fef342e0ad6bc9af596c741e | N/A| SQLi - AND/OR Digit Operator Digit 2 - Beta| Log| Block| This rule is merged into the original rule "SQLi - AND/OR Digit Operator Digit" (ID: 98e7e08ae64247e2801ca4b388d80772 )
CIS Managed Ruleset| eaf11ab80b0d491cbb7186f303b2f3fe | N/A| SQLi - Equation 2 - Beta| Log| Block| This rule is merged into the original rule "SQLi - Equation" (ID: 133c6f83cdf14509a4ca6b82a72a6b3a )


## WAF - WAF Release - 2025-12-11 - Emergency
**Published on:** Thu, 11 Dec 2025 00:00:00 GMT

This emergency release introduces rules for CVE-2025-55183 and CVE-2025-55184, targeting server-side function exposure and resource-exhaustion patterns, respectively.

**Key Findings**

Added coverage for Leaking Server Functions (CVE-2025-55183) and React Function DoS detection (CVE-2025-55184).

**Impact**

These updates strengthen protection for server-function abuse techniques (CVE-2025-55183, CVE-2025-55184) that may expose internal logic or disrupt application availability.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 17c5123f1ac049818765ebf2fefb4e9b | N/A| React - Leaking Server Functions - CVE:CVE-2025-55183| N/A| Block| This was labeled as Generic - Server Function Source Code Exposure.
CIS Free Ruleset| 3114709a3c3b4e3685052c7b251e86aa | N/A| React - Leaking Server Functions - CVE:CVE-2025-55183| N/A| Block| This was labeled as Generic - Server Function Source Code Exposure.
CIS Managed Ruleset| 2694f1610c0b471393b21aef102ec699 | N/A| React - DoS - CVE:CVE-2025-55184| N/A| Disabled| This was labeled as Generic – Server Function Resource Exhaustion.


## WAF - WAF Release - 2025-12-10 - Emergency
**Published on:** Wed, 10 Dec 2025 00:00:00 GMT

This additional week's emergency release introduces improvements to our existing rule for React – Remote Code Execution – CVE-2025-55182 - 2, along with two new generic detections covering server-side function exposure and resource-exhaustion patterns.

**Key Findings**

Enhanced detection logic for React – RCE – CVE-2025-55182, added Generic – Server Function Source Code Exposure, and added Generic – Server Function Resource Exhaustion.

**Impact**

These updates strengthen protection against React RCE exploitation attempts and broaden coverage for common server-function abuse techniques that may expose internal logic or disrupt application availability.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| bc1aee59731c488ca8b5314615fce168 | N/A| React - Remote Code Execution - CVE:CVE-2025-55182 - 2| N/A| Block| This is an improved detection.
CIS Free Ruleset| cbdd3f48396e4b7389d6efd174746aff | N/A| React - Remote Code Execution - CVE:CVE-2025-55182 - 2| N/A| Block| This is an improved detection.
CIS Managed Ruleset| 17c5123f1ac049818765ebf2fefb4e9b | N/A| Generic - Server Function Source Code Exposure| N/A| Block| This is a new detection.
CIS Free Ruleset| 3114709a3c3b4e3685052c7b251e86aa | N/A| Generic - Server Function Source Code Exposure| N/A| Block| This is a new detection.
CIS Managed Ruleset| 2694f1610c0b471393b21aef102ec699 | N/A| Generic - Server Function Resource Exhaustion| N/A| Disabled| This is a new detection.


## WAF - Increased WAF payload limit for all plans
**Published on:** Fri, 05 Dec 2025 00:00:00 GMT

CIS WAF now inspects request-payload size of up to 1 MB across all plans to enhance our detection capabilities for React RCE (CVE-2025-55182).

**Key Findings**

React payloads commonly have a default maximum size of 1 MB. CIS WAF previously inspected up to 128 KB on Enterprise plans, with even lower limits on other plans.

**Update:** We later reinstated the maximum request-payload size the CIS WAF inspects. Refer to [Updating the WAF maximum payload values](https://developers.cloudflare.com/changelog/2025-12-05-waf-max-payload-size-change/) for details.


## WAF - Updating the WAF maximum payload values
**Published on:** Fri, 05 Dec 2025 00:00:00 GMT

We are reinstating the maximum request-payload size the CIS WAF inspects, with WAF on Enterprise zones inspecting up to 128 KB.

**Key Findings**

On [December 5, 2025](https://developers.cloudflare.com/changelog/2025-12-05-rcs-vuln/), we initially attempted to increase the maximum WAF payload limit to 1 MB across all plans. However, an automatic rollout for all customers proved impractical because the increase led to a surge in false positives for existing managed rules.

This issue was particularly notable within the CIS Managed Ruleset and the CIS OWASP Core Ruleset, impacting customer traffic.

**Impact**

Customers on paid plans can increase the limit to 1 MB for any of their zones by contacting CIS Support. Free zones are already protected up to 1 MB and do not require any action.


## WAF - WAF Release - 2025-12-03 - Emergency
**Published on:** Wed, 03 Dec 2025 00:00:00 GMT

The WAF rule deployed yesterday to block unsafe deserialization-based RCE has been updated. The rule description now reads “React – RCE – CVE-2025-55182”, explicitly mapping to the recently disclosed React Server Components vulnerability. Detection logic remains unchanged.

**Key Findings**

Rule description updated to reference React – RCE – CVE-2025-55182 while retaining existing unsafe-deserialization detection.

**Impact**

Improved classification and traceability with no change to coverage against remote code execution attempts.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 33aa8a8a948b48b28d40450c5fb92fba | N/A| React - RCE - CVE:CVE-2025-55182| N/A| Block| Rule metadata description changed. Detection unchanged.
CIS Free Ruleset| 2b5d06e34a814a889bee9a0699702280 | N/A| React - RCE - CVE:CVE-2025-55182| N/A| Block| Rule metadata description changed. Detection unchanged.


## WAF - WAF Release - 2025-12-02 - Emergency
**Published on:** Tue, 02 Dec 2025 00:00:00 GMT

This week's emergency release introduces a new rule to block a critical RCE vulnerability in widely-used web frameworks through unsafe deserialization patterns.

**Key Findings**

New WAF rule deployed for RCE Generic Framework to block malicious POST requests containing unsafe deserialization patterns. If successfully exploited, this vulnerability allows attackers with network access via HTTP to execute arbitrary code remotely.

**Impact**

  * Successful exploitation allows unauthenticated attackers to execute arbitrary code remotely through crafted serialization payloads, enabling complete system compromise, data exfiltration, and potential lateral movement within affected environments.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 33aa8a8a948b48b28d40450c5fb92fba | N/A| RCE Generic - Framework| N/A| Block| This is a new detection.
CIS Free Ruleset| 2b5d06e34a814a889bee9a0699702280 | N/A| RCE Generic - Framework| N/A| Block| This is a new detection.


## WAF - WAF Release - 2025-12-01
**Published on:** Mon, 01 Dec 2025 00:00:00 GMT

This week’s release introduces new detections for remote code execution attempts targeting Monsta FTP (CVE-2025-34299), alongside improvements to an existing XSS detection to enhance coverage.

**Key Findings**

  * CVE-2025-34299 is a critical remote code execution flaw in Monsta FTP, arising from improper handling of user-supplied parameters within the file-handling interface. Certain builds allow crafted requests to bypass sanitization and reach backend PHP functions that execute arbitrary commands. Attackers can send manipulated parameters through the web panel to trigger command execution within the application’s runtime environment.



**Impact**

If exploited, the vulnerability enables full remote command execution on the underlying server, allowing takeover of the hosting environment, unauthorized file access, and potential lateral movement. As the flaw can be triggered without authentication on exposed Monsta FTP instances, it represents a severe risk for publicly reachable deployments.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 480da5e7984542a6b8d8d88da4fcc8a8 | N/A| Monsta FTP - Remote Code Execution - CVE:CVE-2025-34299| Log| Block| This is a new detection
CIS Managed Ruleset| 2380b125c53d42ac94479c42b7492846 | N/A| XSS - JS Context Escape - Beta| Log| Block| This rule is merged into the original rule "XSS - JS Context Escape" (ID: c1ad1bc37caa4cbeb104f44f7a3769d3 )


## WAF - WAF Release - 2025-11-24
**Published on:** Mon, 24 Nov 2025 00:00:00 GMT

This week highlights enhancements to detection signatures improving coverage for vulnerabilities in FortiWeb, linked to CVE-2025-64446, alongside new detection logic expanding protection against PHP Wrapper Injection techniques.

**Key Findings**

This vulnerability enables an unauthenticated attacker to bypass access controls by abusing the `CGIINFO` header. The latest update strengthens detection logic to ensure a reliable identification of crafted requests attempting to exploit this flaw.

**Impact**

  * FortiWeb (CVE-2025-64446): Exploitation allows a remote unauthenticated adversary to circumvent authentication mechanisms by sending a manipulated `CGIINFO` header to FortiWeb’s backend CGI handler. Successful exploitation grants unintended access to restricted administrative functionality, potentially enabling configuration tampering or system-level actions.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| b957ace6e9844bf29244401c4e2e1a2e | N/A| FortiWeb - Authentication Bypass via CGIINFO Header - CVE:CVE-2025-64446| Log| Block| This is a new detection
CIS Managed Ruleset| e3871391a93248fa98a78e03b6c44ed5 | N/A| PHP Wrapper Injection - Body - Beta| Log| Disabled| This rule has been merged into the original rule "PHP Wrapper Injection - Body" (ID:fae6fa37ae9249d58628e54b1a3e521e )
CIS Managed Ruleset| e6b1b66e0e3b46969102baed900f4015 | N/A| PHP Wrapper Injection - URI - Beta| Log| Disabled| This rule has been merged into the original rule "PHP Wrapper Injection - URI" (ID:9c02e585db34440da620eb668f76bd74 )


## WAF - WAF Release - 2025-11-21
**Published on:** Fri, 21 Nov 2025 00:00:00 GMT

This week’s release introduces a critical detection for CVE-2025-61757, a vulnerability in the Oracle Identity Manager REST WebServices component.

**Key Findings**

This flaw allows unauthenticated attackers with network access over HTTP to fully compromise the Identity Manager, potentially leading to a complete takeover.

**Impact**

Oracle Identity Manager (CVE-2025-61757): Exploitation could allow an unauthenticated remote attacker to bypass security checks by sending specially crafted requests to the application's message processor. This enables the creation of arbitrary employee accounts, which can be leveraged to modify system configurations and achieve full system compromise.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| fa584616fe2241608cb8bd1339fdbe7e | N/A| Oracle Identity Manager - Pre-Auth RCE - CVE:CVE-2025-61757| N/A| Block| This is a new detection.


## WAF - WAF Release - 2025-11-17
**Published on:** Mon, 17 Nov 2025 00:00:00 GMT

This week highlights enhancements to detection signatures improving coverage for vulnerabilities in DELMIA Apriso, linked to CVE-2025-6205.

**Key Findings**

This vulnerability allows unauthenticated attackers to gain privileged access to the application. The latest update provides enhanced detection logic for resilient protection against exploitation attempts.

**Impact**

  * DELMIA Apriso (CVE-2025-6205): Exploitation could allow an unauthenticated remote attacker to bypass security checks by sending specially crafted requests to the application's message processor. This enables the creation of arbitrary employee accounts, which can be leveraged to modify system configurations and achieve full system compromise.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| ec1e2aa190e64e7cb468e16dd256f4bc | N/A| DELMIA Apriso - Auth Bypass - CVE:CVE-2025-6205| Log| Block| This is a new detection.
CIS Managed Ruleset| fae6fa37ae9249d58628e54b1a3e521e | N/A| PHP Wrapper Injection - Body| N/A| Disabled| Rule metadata description refined. Detection unchanged.
CIS Managed Ruleset| 9c02e585db34440da620eb668f76bd74 | N/A| PHP Wrapper Injection - URI| N/A| Disabled| Rule metadata description refined. Detection unchanged.


## WAF - WAF Release - 2025-11-10
**Published on:** Mon, 10 Nov 2025 00:00:00 GMT

This week’s release introduces new detections for Prototype Pollution across three common vectors: URI, Body, and Header/Form.

**Key Findings**

  * These attacks can affect both API and web applications by altering normal behavior or bypassing security controls.



**Impact**

Exploitation may allow attackers to change internal logic or cause unexpected behavior in applications using JavaScript or Node.js frameworks. Developers should sanitize input keys and avoid merging untrusted data structures.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 32405a50728746dd8caa057b606285e6 | N/A| Generic Rules - Prototype Pollution - URI| Log| Disabled| This is a new detection
CIS Managed Ruleset| a7da00c63c4243d2a72456fe4f59ff26 | N/A| Generic Rules - Prototype Pollution - Body| Log| Disabled| This is a new detection
CIS Managed Ruleset| 833078bdcfa04bb7aa7b8fb67efbeb39 | N/A| Generic Rules - Prototype Pollution - Header - Form| Log| Disabled| This is a new detection


## WAF - WAF Release - 2025-11-05 - Emergency
**Published on:** Wed, 05 Nov 2025 00:00:00 GMT

This week’s emergency release introduces a new detection signature that enhances coverage for a critical vulnerability in the React Native Metro Development Server, tracked as CVE-2025-11953.

**Key Findings**

The Metro Development Server exposes an HTTP endpoint that is vulnerable to OS command injection (CWE-78). An unauthenticated network attacker can send a crafted request to this endpoint and execute arbitrary commands on the host running Metro. The vulnerability affects Metro/cli-server-api builds used by React Native Community CLI in pre-patch development releases.

**Impact**

Successful exploitation of CVE-2025-11953 may result in remote command execution on developer workstations or CI/build agents, leading to credential and secret exposure, source tampering, and potential lateral movement into internal networks. Administrators and developers are strongly advised to apply the vendor's patches and restrict Metro’s network exposure to reduce this risk.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| db6b9e1ac1494971ae8c70aac8e30c5b | N/A| React Native Metro - Command Injection - CVE:CVE-2025-11953| N/A| Block| This is a New Detection


## WAF - WAF Release - 2025-11-03
**Published on:** Mon, 03 Nov 2025 00:00:00 GMT

This week highlights enhancements to detection signatures improving coverage for vulnerabilities in Adobe Commerce and Magento Open Source, linked to CVE-2025-54236.

**Key Findings**

This vulnerability allows unauthenticated attackers to take over customer accounts through the Commerce REST API and, in certain configurations, may lead to remote code execution. The latest update provides enhanced detection logic for resilient protection against exploitation attempts.

**Impact**

  * Adobe Commerce (CVE-2025-54236): Exploitation may allow attackers to hijack sessions, execute arbitrary commands, steal data, and disrupt storefronts, resulting in confidentiality and integrity risks for merchants. Administrators are strongly encouraged to apply vendor patches without delay.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| f5295d8333b7428c816654d8cb6d5fe5 | 100774C| Adobe Commerce - Remote Code Execution - CVE:CVE-2025-54236| Log| Block| This is an improved detection.


## WAF - WAF Release - 2025-10-30 - Emergency
**Published on:** Thu, 30 Oct 2025 00:00:00 GMT

This week’s release introduces a new detection signature that enhances coverage for a critical vulnerability in Oracle E-Business Suite, tracked as CVE-2025-61884.

**Key Findings**

The flaw is easily exploitable and allows an unauthenticated attacker with network access to compromise Oracle Configurator, which can grant access to sensitive resources and configuration data. The affected versions include 12.2.3 through 12.2.14.

**Impact**

Successful exploitation of CVE-2025-61884 may result in unauthorized access to critical business data or full exposure of information accessible through Oracle Configurator. Administrators are strongly advised to apply vendor's patches and recommended mitigations to reduce this exposure.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 2749f13f8cb34a3dbd49c8c48827402f | N/A| Oracle E-Business Suite - SSRF - CVE:CVE-2025-61884| N/A| Block| This is a New Detection


## WAF - WAF Release - 2025-10-24 - Emergency
**Published on:** Fri, 24 Oct 2025 00:00:00 GMT

This week’s release introduces a new detection signature that enhances coverage for a critical vulnerability in Windows Server Update Services (WSUS), tracked as CVE-2025-59287.

**Key Findings**

The vulnerability allows unauthenticated attackers to potentially achieve remote code execution. The updated detection logic strengthens defenses by improving resilience against exploitation attempts targeting this flaw.

**Impact**

Successful exploitation of CVE-2025-59287 could enable attackers to hijack sessions, execute arbitrary commands, exfiltrate sensitive data, and disrupt storefront operations. These actions pose significant confidentiality and integrity risks to affected environments. Administrators should apply vendor patches immediately to mitigate exposure.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 5eaeb5ea6e5a4bce867eb3ffbd72ba08 | N/A| Windows Server - Deserialization - CVE:CVE-2025-59287| N/A| Block| This is a New Detection


## WAF - WAF Release - 2025-10-23 - Emergency
**Published on:** Thu, 23 Oct 2025 00:00:00 GMT

This week highlights enhancements to detection signatures improving coverage for vulnerabilities in Adobe Commerce and Magento Open Source, linked to CVE-2025-54236.

**Key Findings**

This vulnerability allows unauthenticated attackers to take over customer accounts through the Commerce REST API and, in certain configurations, may lead to remote code execution. The latest update enhances detection logic to provide more resilient protection against exploitation attempts.

**Impact**

Adobe Commerce (CVE-2025-54236): Exploitation may allow attackers to hijack sessions, execute arbitrary commands, steal data, and disrupt storefronts, resulting in confidentiality and integrity risks for merchants. Administrators are strongly encouraged to apply vendor patches without delay.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 6e04fa2b9eb34fb088034d3fc6ef59a1 | N/A| Adobe Commerce - Remote Code Execution - CVE:CVE-2025-54236| N/A| Block| This is a New Detection


## WAF - WAF Release - 2025-10-20
**Published on:** Mon, 20 Oct 2025 00:00:00 GMT

This week’s update introduces an enhanced rule that expands detection coverage for a critical vulnerability in Oracle E-Business Suite. It also improves an existing rule to provide more reliable coverage in request processing.

**Key Findings**

New WAF rule deployed for Oracle E-Business Suite (CVE-2025-61882) to block unauthenticated attacker's network access via HTTP to compromise Oracle Concurrent Processing. If successfully exploited, this vulnerability may result in remote code execution.

**Impact**

  * Successful exploitation of CVE-2025-61882 allows unauthenticated attackers to execute arbitrary code remotely by chaining multiple weaknesses, enabling lateral movement into internal services, data exfiltration, and large-scale extortionware deployment within Oracle E-Business Suite environments.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 933fc13202cd4e8ba498c0f32b4101ab | 100598A| Remote Code Execution - Common Bash Bypass - Beta| Log| Block| This rule is merged into the original rule "Remote Code Execution - Common Bash Bypass" (ID: f8238867ed3e4d3a9a7b731a50cec478 )
CIS Managed Ruleset| 185b5df42d1e44e0aeb8f8b8a1118614 | 100916A| Oracle E-Business Suite - Remote Code Execution - CVE:CVE-2025-61882 - 2| Log| Block| This is a New Detection
CIS Managed Ruleset| 646bccf7e9dc46918a4150d6c22b51d3 | N/A| HTTP Truncated| N/A| Disabled| This is a New Detection


## WAF - New detections released for WAF managed rulesets
**Published on:** Fri, 17 Oct 2025 00:00:00 GMT

This week we introduced several new detections across CIS Managed Rulesets, expanding coverage for high-impact vulnerability classes such as SSRF, SQLi, SSTI, Reverse Shell attempts, and Prototype Pollution. These rules aim to improve protection against attacker-controlled payloads that exploit misconfigurations or unvalidated input in web applications.

**Key Findings**

New detections added for multiple exploit categories:

SSRF (Server-Side Request Forgery) — new rules targeting both local and cloud metadata abuse patterns (Beta).

SQL Injection (SQLi) — rules for common patterns, sleep/time-based injections, and string/wait function exploitation across headers and URIs.

SSTI (Server-Side Template Injection) — arithmetic-based probe detections introduced across URI, header, and body fields.

Reverse Shell and XXE payloads — enhanced heuristics for command execution and XML external entity misuse.

Prototype Pollution — new Beta rule identifying common JSON payload structures used in object prototype poisoning.

PHP Wrapper Injection and HTTP Parameter Pollution detections — to catch path traversal and multi-parameter manipulation attempts.

Anomaly Header Checks — detecting CRLF injection attempts in header names.

**Impact**

These updates help detect multi-vector payloads that blend SSRF + RCE or SQLi + SSTI attacks, especially in cloud-hosted applications with exposed metadata endpoints or unsafe template rendering.

Prototype Pollution and HTTP parameter pollution rules address emerging JavaScript supply-chain exploitation patterns increasingly seen in real-world incidents.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 72f0ff933fb0492eb71cda50589f2a1d | N/A| Anomaly:Header - name - CR, LF| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 5d0377e4435f467488614170132fab7e | N/A| Generic Rules - Reverse Shell - Body| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 54e32f7f802c4a699182e8921a027008 | N/A| Generic Rules - Reverse Shell - Header| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 7cbda8dbafbc465d9b64a8f2958d0486 | N/A| Generic Rules - Reverse Shell - URI| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| b9f3420674cf481da32333dc8e0cf7ad | N/A| Generic Rules - XXE - Body| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| ad55483512f0440b81426acdbf8aab5e | N/A| Generic Rules - SQLi - Common Patterns - Header URI| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 849c0618d1674f1c92ba6f9b2e466337 | N/A| Generic Rules - SQLi - Sleep Function - Header URI| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 1b4db4c4bd0649c095c27c6cb686ab47 | N/A| Generic Rules - SQLi - String Function - Header URI| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| fa2055b84af94ba4b925f834b0633709 | N/A| Generic Rules - SQLi - WaitFor Function - Header URI| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 158177dec2504acdba1f2da201a076eb | N/A| SSRF - Local - Beta| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 98bfd6bb46074d5b8d1c4b39743a63ec | N/A| SSRF - Local - 2 - Beta| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 54e1733b10da4a599e06c6fbc2e84e2d | N/A| SSRF - Cloud - Beta| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| ecd26d61a75e46f6a4449a06ab8af26f | N/A| SSRF - Cloud - 2 - Beta| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| c16f4e133c4541f293142d02e6e8dc5b | N/A| SSTI - Arithmetic Probe - URI| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| f4fd9904e7624666b8c49cd62550d794 | N/A| SSTI - Arithmetic Probe - Header| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 5c0875604f774c36a4f9b69c659d12a6 | N/A| SSTI - Arithmetic Probe - Body| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| fae6fa37ae9249d58628e54b1a3e521e | N/A| PHP Wrapper Injection| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 9c02e585db34440da620eb668f76bd74 | N/A| PHP Wrapper Injection| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| cb67fe56a84747b8b64277dc091e296d | N/A| HTTP parameter pollution| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 443b54d984944cd69043805ee34214ef | N/A| Prototype Pollution - Common Payloads - Beta| N/A| Disabled| This is a New Detection


## WAF - WAF Release - 2025-10-13
**Published on:** Mon, 13 Oct 2025 00:00:00 GMT

This week’s highlights include a new JinJava rule targeting a sandbox-bypass flaw that could allow malicious template input to escape execution controls. The rule improves detection for unsafe template rendering paths.

**Key Findings**

New WAF rule deployed for JinJava (CVE-2025-59340) to block a sandbox bypass in the template engine that permits attacker-controlled type construction and arbitrary class instantiation; in vulnerable environments this can escalate to remote code execution and full server compromise.

**Impact**

  * CVE-2025-59340 — Exploitation enables attacker-supplied type descriptors / Jackson `ObjectMapper` abuse, allowing arbitrary class loading, file/URL access (LFI/SSRF primitives) and, with suitable gadget chains, potential remote code execution and system compromise.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| b327d6442e2d4848b4aab3cbc04bab5f | 100892| JinJava - SSTI - CVE:CVE-2025-59340| Log| Block| This is a New Detection


## WAF - WAF Release - 2025-10-07 - Emergency
**Published on:** Tue, 07 Oct 2025 00:00:00 GMT

This week highlights multiple critical Cisco vulnerabilities (CVE-2025-20363, CVE-2025-20333, CVE-2025-20362). This flaw stems from improper input validation in HTTP(S) requests. An authenticated VPN user could send crafted requests to execute code as root, potentially compromising the device. The initial two rules were made available on September 28, with a third rule added today, October 7, for more robust protection.

  * Cisco (CVE-2025-20333, CVE-2025-20362, CVE-2025-20363): Multiple vulnerabilities that could allow attackers to exploit unsafe deserialization and input validation flaws. Successful exploitation may result in arbitrary code execution, privilege escalation, or command injection on affected systems.



**Impact**

Cisco (CVE-2025-20333, CVE-2025-20362, CVE-2025-20363): Exploitation enables attackers to escalate privileges or achieve remote code execution via command injection. Administrators are strongly advised to apply vendor updates immediately.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 12f808a5315441688f3b7c8a3a4d1bd6 | 100788B| Cisco Secure Firewall Adaptive Security Appliance - Remote Code Execution - CVE:CVE-2025-20333, CVE:CVE-2025-20362, CVE:CVE-2025-20363| N/A| Block| This is a New Detection


## WAF - WAF Release - 2025-10-06
**Published on:** Mon, 06 Oct 2025 00:00:00 GMT

This week’s highlights prioritise an emergency Oracle E-Business Suite RCE rule deployed to block active, high-impact exploitation. Also addressed are high-severity Chaos Mesh controller command-injection flaws that enable unauthenticated in-cluster RCE and potential cluster compromise, plus a form-data multipart boundary issue that permits HTTP Parameter Pollution (HPP). Two new generic SQLi detections were added to catch inline-comment obfuscation and information disclosure techniques.

**Key Findings**

  * New emergency rule released for Oracle E-Business Suite (CVE-2025-61882) addressing an actively exploited remote code execution vulnerability in core business application modules. Immediate mitigation deployed to protect enterprise workloads.

  * Chaos Mesh (CVE-2025-59358,CVE-2025-59359,CVE-2025-59360,CVE-2025-59361): A GraphQL debug endpoint on the Chaos Controller Manager is exposed without authentication; several controller mutations (`cleanTcs`, `killProcesses`, `cleanIptables`) are vulnerable to OS command injection.

  * Form-Data (CVE-2025-7783): Attackers who can observe `Math.random()` outputs and control request fields in form-data may exploit this flaw to perform HTTP parameter pollution, leading to request tampering or data manipulation.

  * Two new generic SQLi detections added to enhance baseline coverage against inline-comment obfuscation and information disclosure attempts.




**Impact**

  * CVE-2025-61882 — Oracle E-Business Suite remote code execution (emergency detection): attacker-controlled input can yield full system compromise, data exfiltration, and operational outage; immediate blocking enforced.

  * CVE-2025-59358 / CVE-2025-59359 / CVE-2025-59360 / CVE-2025-59361 — Unauthenticated command-injection in Chaos Mesh controllers allowing remote code execution, cluster compromise, and service disruption (high availability risk).

  * CVE-2025-7783 — Predictable multipart boundaries in form-data enabling HTTP Parameter Pollution; results include request tampering, parameter overwrite, and downstream data integrity loss.


Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 0c9bf31ab6fa41fc8f12daaf8650f52f | 100882| Chaos Mesh - Missing Authentication - CVE:CVE-2025-59358| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 5d459ed434ed446c9580c73c2b8c3680 | 100883| Chaos Mesh - Command Injection - CVE:CVE-2025-59359| Log| Block| This is a New Detection
CIS Managed Ruleset| a2591ba5befa4815a6861aefef859a04 | 100884| Chaos Mesh - Command Injection - CVE:CVE-2025-59361| Log| Block| This is a New Detection
CIS Managed Ruleset| 05eea4fabf6f4cf3aac1094b961f26a7 | 100886| Form-Data - Parameter Pollution - CVE:CVE-2025-7783| Log| Block| This is a New Detection
CIS Managed Ruleset| 90514c7810694b188f56979826a4074c | 100888| Chaos Mesh - Command Injection - CVE:CVE-2025-59360| Log| Block| This is a New Detection
CIS Managed Ruleset| 42fbc8c09ec84578b9633ffc31101b2f | 100916| Oracle E-Business Suite - Remote Code Execution - CVE:CVE-2025-61882| N/A| Block| This is a New Detection
CIS Managed Ruleset| badc687a3ba3420a844220b129aa43c3 | 100917| Generic Rules - SQLi - Inline Comment Injection| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 28fa27511f29428899ceb5a273c10b6f | 100918| Generic Rules - SQLi - Information Disclosure| N/A| Disabled| This is a New Detection


## WAF - WAF Release - 2025-10-03
**Published on:** Fri, 03 Oct 2025 00:00:00 GMT

**Managed Ruleset Updated**

This update introduces 21 new detections in the CIS Managed Ruleset (all currently set to Disabled mode to preserve remediation logic and allow quick activation if needed). The rules cover a broad spectrum of threats - SQL injection techniques, command and code injection, information disclosure of common files, URL anomalies, and cross-site scripting.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 0d02c2fb14eb4cec9c2e2b58d61fac74 | 100902| Generic Rules - Command Execution - 2| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| c3079865ce9a41368657026b514aeeb8 | 100908| Generic Rules - Command Execution - 3| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 107ae2922b654bb28df7ca978d46a6f4 | 100910| Generic Rules - Command Execution - 4| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 68bdb75ae6d24e139a83e5731bd0a329 | 100915| Generic Rules - Command Execution - 5| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| ea04bb580f7d400386c7dc1d5e51450a | 100899| Generic Rules - Content-Type Abuse| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 233364f656ff42b8acc41dcd7996012f | 100914| Generic Rules - Content-Type Injection| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 1aa695281c954513be3d003b93209312 | 100911| Generic Rules - Cookie Header Injection| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| d9f9e4f5bf11489da52dccb40f373b3f | 100905| Generic Rules - NoSQL Injection| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 5a1897b714e044a887c0f3f078a0ed04 | 100913| Generic Rules - NoSQL Injection - 2| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 4d6fd28df4f1494e95e70d2c5d649624 | 100907| Generic Rules - Parameter Pollution| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 61181e3af5304f7396c7d01cfd1c674e | 100906| Generic Rules - PHP Object Injection| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| ed5190bfbe1b45a6a645126334c88168 | 100904| Generic Rules - Prototype Pollution| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 3ec33bc5ac77495a9f55020e3ab43f7e | 100897| Generic Rules - Prototype Pollution 2| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| c6d752c4909e4b7e8eff6c780d94ee22 | 100903| Generic Rules - Reverse Shell| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| caf37e7800bb4635bcc2eefcd5add8e3 | 100909| Generic Rules - Reverse Shell - 2| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 475d090baead467c88dfabbb565c78b0 | 100898| Generic Rules - SSJI NoSQL| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| f4c7f98934264c9c937eec1212b837a0 | 100896| Generic Rules - SSRF| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| efd01b814d144e90b36522b311c4fb00 | 100895| Generic Rules - Template Injection| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 00a9a0d663da4add95b863abd3ed0123 | 100895A| Generic Rules - Template Injection - 2| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| e58c0fffee4f4374bd37f2577501a1d9 | 100912| Generic Rules - XXE| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| ab09ba8d00eb4cdbb7a6a65ddc55cdb6 | 100900| Relative Paths - Anomaly Headers| N/A| Disabled| This is a New Detection


## WAF - WAF Release - 2025-09-29
**Published on:** Mon, 29 Sep 2025 00:00:00 GMT

This week highlights four important vendor- and component-specific issues: an authentication bypass in SimpleHelp (CVE-2024-57727), an information-disclosure flaw in Flowise Cloud (CVE-2025-58434), an SSRF in the WordPress plugin Ditty (CVE-2025-8085), and a directory-traversal bug in Vite (CVE-2025-30208). These are paired with improvements to our generic detection coverage (SQLi, SSRF) to raise the baseline and reduce noisy gaps.

**Key Findings**

  * SimpleHelp (CVE-2024-57727): Authentication bypass in SimpleHelp that can allow unauthorized access to management interfaces or sessions.

  * Flowise Cloud (CVE-2025-58434): Information-disclosure vulnerability in Flowise Cloud that may expose sensitive configuration or user data to unauthenticated or low-privileged actors.

  * WordPress:Plugin: Ditty (CVE-2025-8085): SSRF in the Ditty WordPress plugin enabling server-side requests that could reach internal services or cloud metadata endpoints.

  * Vite (CVE-2025-30208): Directory-traversal vulnerability in Vite allowing access to filesystem paths outside the intended web root.




**Impact**

These vulnerabilities allow attackers to gain access, escalate privileges, or execute actions that were previously unavailable:

  * SimpleHelp (CVE-2024-57727): An authentication bypass that can let unauthenticated attackers access management interfaces or hijack sessions — enabling lateral movement, credential theft, or privilege escalation within affected environments.

  * Flowise Cloud (CVE-2025-58434): Information-disclosure flaw that can expose sensitive configuration, tokens, or user data; leaked secrets may be chained into account takeover or privileged access to backend services.

  * WordPress:Plugin: Ditty (CVE-2025-8085): SSRF that enables server-side requests to internal services or cloud metadata endpoints, potentially allowing attackers to retrieve credentials or reach otherwise inaccessible infrastructure, leading to privilege escalation or cloud resource compromise.

  * Vite (CVE-2025-30208): Directory-traversal vulnerability that can expose filesystem contents outside the web root (configuration files, keys, source code), which attackers can use to escalate privileges or further compromise systems.


Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 6fe90532af50427484a5275c8c2e30fb | 100717| SimpleHelp - Auth Bypass - CVE:CVE-2024-57727| Log| Block| This rule is merged to 100717 in legacy WAF and 498fcd81a62a4b5ca943e2de958094d3 in new WAF
CIS Managed Ruleset| 013ef5de3f074fd5a43cdd70d58b886b | 100775| Flowise Cloud - Information Disclosure - CVE:CVE-2025-58434| Log| Block| This is a New Detection
CIS Managed Ruleset| 68fc5c086ccb4b40a35a63b19bce1ff4 | 100881| WordPress:Plugin:Ditty - SSRF - CVE:CVE-2025-8085| Log| Block| This is a New Detection
CIS Managed Ruleset| 9e1a56e6b3bc49b187bf6e35ddc329dd | 100887| Vite - Directory Traversal - CVE:CVE-2025-30208| Log| Block| This is a New Detection


## WAF - WAF Release - 2025-09-28 - Emergency
**Published on:** Sun, 28 Sep 2025 00:00:00 GMT

This week highlights multiple critical Cisco vulnerabilities (CVE-2025-20363, CVE-2025-20333, CVE-2025-20362). This flaw stems from improper input validation in HTTP(S) requests. An authenticated VPN user could send crafted requests to execute code as root, potentially compromising the device.

**Key Findings**

  * Cisco (CVE-2025-20333, CVE-2025-20362, CVE-2025-20363): Multiple vulnerabilities that could allow attackers to exploit unsafe deserialization and input validation flaws. Successful exploitation may result in arbitrary code execution, privilege escalation, or command injection on affected systems.



**Impact**

Cisco (CVE-2025-20333, CVE-2025-20362, CVE-2025-20363): Exploitation enables attackers to escalate privileges or achieve remote code execution via command injection.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| a1bef4ada0b146d2862cad439ee0ab84 | 100788| Cisco Secure Firewall Adaptive Security Appliance - Remote Code Execution - CVE:CVE-2025-20333, CVE:CVE-2025-20362, CVE:CVE-2025-20363| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 51de6ce6596a40eb8200452ad30f768e | 100788A| Cisco Secure Firewall Adaptive Security Appliance - Remote Code Execution - CVE:CVE-2025-20333, CVE:CVE-2025-20362, CVE:CVE-2025-20363| N/A| Disabled| This is a New Detection


## WAF - WAF Release - 2025-09-26
**Published on:** Fri, 26 Sep 2025 00:00:00 GMT

**Managed Ruleset Updated**

This update introduces 11 new detections in the CIS Managed Ruleset (all currently set to Disabled mode to preserve remediation logic and allow quick activation if needed). The rules cover a broad spectrum of threats - SQL injection techniques, command and code injection, information disclosure of common files, URL anomalies, and cross-site scripting.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 3ffd242b4ba242ca965022d3a67d8561 | 100859A| SQLi - UNION - 3| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 91d9cf56355b4ab88481b2fd4de80468 | 100889| Command Injection - Generic 9| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| c15ca8e8290f485287037665f2be3ddf | 100890| Information Disclosure - Common Files - 2| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 56669615f2984c2cac8c608980a252a8 | 100891| Anomaly:URL - Relative Paths| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| c41789fb6370431d809567d17e7d3865 | 100894| XSS - Inline Function| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| b995d0b930604fa6b8d9b2a13792565c | 100895| XSS - DOM| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| ab8277e3f432400bbd9403dd42978e38 | 100896| SQLi - MSSQL Length Enumeration| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 3ec33bc5ac77495a9f55020e3ab43f7e | 100897| Generic Rules - Code Injection - 3| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 4375dc90c7af4c55908f6b95c1686741 | 100898| SQLi - Evasion| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 945c5aa9f45141dd872d7ec920999be0 | 100899| SQLi - Probing 2| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 2c20b5e8684043f48620ff77b4026c88 | 100900| SQLi - Probing| N/A| Disabled| This is a New Detection


## WAF - WAF Release - 2025-09-24 - Emergency
**Published on:** Wed, 24 Sep 2025 00:00:00 GMT

This week highlights a critical vendor-specific vulnerability: a deserialization flaw in the License Servlet of Fortra’s GoAnywhere MFT. By forging a license response signature, an attacker can trigger deserialization of arbitrary objects, potentially leading to command injection.

**Key Findings**

  * GoAnywhere MFT (CVE-2025-10035): Deserialization vulnerability in the License Servlet that allows attackers with a forged license response signature to deserialize arbitrary objects, potentially resulting in command injection.



**Impact**

GoAnywhere MFT (CVE-2025-10035): Exploitation enables attackers to escalate privileges or achieve remote code execution via command injection.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 8fe242c7c0d64d689f4fc9a1e08b39f3 | 100787| Fortra GoAnywhere - Auth Bypass - CVE:CVE-2025-10035| N/A| Block| This is a New Detection


## WAF - WAF Release - 2025-09-22
**Published on:** Mon, 22 Sep 2025 00:00:00 GMT

This week emphasizes two critical vendor-specific vulnerabilities: a full elevation-of-privilege in Microsoft Azure Networking (CVE-2025-54914) and a server-side template injection (SSTI) leading to remote code execution (RCE) in Skyvern (CVE-2025-49619). These are complemented by enhancements in generic detections (SQLi, SSRF) to improve baseline coverage.

**Key Findings**

  * Azure (CVE-2025-54914): Vulnerability in Azure Networking allowing elevation of privileges.

  * Skyvern (CVE-2025-49619): Skyvern ≤ 0.1.85 has a server-side template injection (SSTI) vulnerability in its Prompt field (workflow blocks) via Jinja2. Authenticated users with low privileges can get remote code execution (blind).

  * Generic SQLi / SSRF improvements: Expanded rule coverage to detect obfuscated SQL injection patterns and SSRF across host, local, and cloud contexts.




**Impact**

These vulnerabilities allow attackers to escalate privileges or execute code under conditions where previously they could not:

  * Azure CVE-2025-54914 enables an attacker from the network with no credentials to gain high-level access within Azure Networking; could lead to full compromise of networking components.

  * Skyvern CVE-2025-49619 allows authenticated users with minimal privilege to exploit SSTI for remote code execution, undermining isolation of workflow components.

  * The improvements for SQLi and SSRF reduce risk from common injection and request-based attacks.


Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| c36a425ae0c94789a9bc34f06a135cbf | 100146| SSRF - Host - 2| Log| Disabled| This is a New Detection
CIS Managed Ruleset| dfa84b0aed5a4b45b953a36a57035abf | 100146B| SSRF - Local - 2| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 276073e60c7a4b4d91faba1fbbe18d50 | 100146C| SSRF - Cloud - 2| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 78c856218f2d40f4b5988c8c956c1961 | 100714| Azure - Auth Bypass - CVE:CVE-2025-54914| Log| Block| This is a New Detection
CIS Managed Ruleset| 9f1c8d4cbf3848dbb940771bc5ced231 | 100758| Skyvern - Remote Code Execution - CVE:CVE-2025-49619| Log| Block| This is a New Detection
CIS Managed Ruleset| 6be7e7829f3b43c688e1ac4284a619a1 | 100773| Next.js - SSRF| Log| Block| This is a New Detection
CIS Managed Ruleset| 0cc3f50216bf4b448210bcc3983ff2dd | 100774| Adobe Commerce - Remote Code Execution - CVE:CVE-2025-54236| Log| Block| This is a New Detection
CIS Managed Ruleset| 53bfaeb311a049e3877fa15c0380a1a6 | 100800_BETA| SQLi - Obfuscated Boolean - Beta| Log| Block| This rule has been merged into the original rule (ID: 7663ea44178441a0b3205c145563445f )


## WAF - WAF Release - 2025-09-15
**Published on:** Mon, 15 Sep 2025 00:00:00 GMT

**This week's update**

This week's focus highlights newly disclosed vulnerabilities in DevOps tooling, data visualization platforms, and enterprise CMS solutions. These issues include sensitive information disclosure and remote code execution, putting organizations at risk of credential leakage, unauthorized access, and full system compromise.

**Key Findings**

  * Argo CD (CVE-2025-55190): Exposure of sensitive information could allow attackers to access credential data stored in configurations, potentially leading to compromise of Kubernetes workloads and secrets.

  * DataEase (CVE-2025-57773): Insufficient input validation enables JNDI injection and insecure deserialization, resulting in remote code execution (RCE). Successful exploitation grants attackers control over the application server.

  * Sitecore (CVE-2025-53694): A sensitive information disclosure flaw allows unauthorized access to confidential information stored in Sitecore deployments, raising the risk of data breaches and privilege escalation.




**Impact**

These vulnerabilities expose organizations to serious risks, including credential theft, unauthorized access, and full system compromise. Argo CD's flaw may expose Kubernetes secrets, DataEase exploitation could give attackers remote execution capabilities, and Sitecore's disclosure issue increases the likelihood of sensitive data leakage and business impact.

Administrators are strongly advised to apply vendor patches immediately, rotate exposed credentials, and review access controls to mitigate these risks.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 199cce9ab21e40bcb535f01b2ee2085f | 100646| Argo CD - Information Disclosure - CVE:CVE-2025-55190s| Log| Disabled| This is a New Detection
CIS Managed Ruleset| e513bb21b6a44f9cbfcd2462f5e20788 | 100874| DataEase - JNDI injection - CVE:CVE-2025-57773| Log| Disabled| This is a New Detection
CIS Managed Ruleset| be097f5a71a04f27aa87b60d005a12fd | 100880| Sitecore - Information Disclosure - CVE:CVE-2025-53694| Log| Block| This is a New Detection


## WAF - WAF Release - 2025-09-08
**Published on:** Mon, 08 Sep 2025 00:00:00 GMT

**This week's update**

This week’s focus highlights newly disclosed vulnerabilities in web frameworks, enterprise applications, and widely deployed CMS plugins. The vulnerabilities include SSRF, authentication bypass, arbitrary file upload, and remote code execution (RCE), exposing organizations to high-impact risks such as unauthorized access, system compromise, and potential data exposure. In addition, security rule enhancements have been deployed to cover general command injection and server-side injection attacks, further strengthening protections.

**Key Findings**

  * Next.js (CVE-2025-57822): Improper handling of redirects in custom middleware can lead to server-side request forgery (SSRF) when user-supplied headers are forwarded. Attackers could exploit this to access internal services or cloud metadata endpoints. The issue has been resolved in versions 14.2.32 and 15.4.7. Developers using custom middleware should upgrade and verify proper redirect handling in `next()` calls.

  * ScriptCase (CVE-2025-47227, CVE-2025-47228): In the Production Environment extension in Netmake ScriptCase through 9.12.006 (23), two vulnerabilities allow attackers to reset admin accounts and execute system commands, potentially leading to full compromise of affected deployments.

  * Sar2HTML (CVE-2025-34030): In Sar2HTML version 3.2.2 and earlier, insufficient input sanitization of the plot parameter allows remote, unauthenticated attackers to execute arbitrary system commands. Exploitation could compromise the underlying server and its data.

  * Zhiyuan OA (CVE-2025-34040): An arbitrary file upload vulnerability exists in the Zhiyuan OA platform. Improper validation in the `wpsAssistServlet` interface allows unauthenticated attackers to upload crafted files via path traversal, which can be executed on the web server, leading to remote code execution.

  * WordPress:Plugin:InfiniteWP Client (CVE-2020-8772): A vulnerability in the InfiniteWP Client plugin allows attackers to perform restricted actions and gain administrative control of connected WordPress sites.




**Impact**

These vulnerabilities could allow attackers to gain unauthorized access, execute malicious code, or take full control of affected systems. The Next.js SSRF flaw may expose internal services or cloud metadata endpoints to attackers. Exploitations of ScriptCase and Sar2HTML could result in remote code execution, administrative takeover, and full server compromise. In Zhiyuan OA, the arbitrary file upload vulnerability allows attackers to execute malicious code on the web server, potentially exposing sensitive data and applications. The authentication bypass in WordPress InfiniteWP Client enables attackers to gain administrative access, risking data exposure and unauthorized control of connected sites.

Administrators are strongly advised to apply vendor patches immediately, remove unsupported software, and review authentication and access controls to mitigate these risks.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 7c5812a31fd94996b3299f7e963d7afc | 100007D| Command Injection - Common Attack Commands Args| Log| Block| This rule has been merged into the original rule "Command Injection - Common Attack Commands" (ID: 89557ce9b26e4d4dbf29e90c28345b9b ) for New WAF customers only.
CIS Managed Ruleset| cd528243d6824f7ab56182988230a75b | 100617| Next.js - SSRF - CVE:CVE-2025-57822| Log| Block| This is a New Detection
CIS Managed Ruleset| 503b337dac5c409d8f833a6ba22dabf1 | 100659_BETA| Common Payloads for Server-Side Template Injection - Beta| Log| Block| This rule is merged into the original rule "Common Payloads for Server-Side Template Injection" (ID: 21c7a963e1b749e7b1753238a28a42c4 )
CIS Managed Ruleset| 6d24266148f24f5e9fa487f8b416b7ca | 100824B| CrushFTP - Remote Code Execution - CVE:CVE-2025-54309 - 3| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 154b217c43d04f11a13aeff05db1fa6b | 100848| ScriptCase - Auth Bypass - CVE:CVE-2025-47227| Log| Disabled| This is a New Detection
CIS Managed Ruleset| cad6f1c8c6d44ef59929e6532c62d330 | 100849| ScriptCase - Command Injection - CVE:CVE-2025-47228| Log| Disabled| This is a New Detection
CIS Managed Ruleset| e7464139fd3e44938b56716bef971afd | 100872| WordPress:Plugin:InfiniteWP Client - Missing Authorization - CVE:CVE-2020-8772| Log| Block| This is a New Detection
CIS Managed Ruleset| 0181ebb2cc234f2d863412e1bab19b0b | 100873| Sar2HTML - Command Injection - CVE:CVE-2025-34030| Log| Block| This is a New Detection
CIS Managed Ruleset| 34d5c7c7b08b40eaad5b2bb3f24c0fbe | 100875| Zhiyuan OA - Remote Code Execution - CVE:CVE-2025-34040| Log| Block| This is a New Detection


## WAF - WAF Release - 2025-09-04 - Emergency
**Published on:** Thu, 04 Sep 2025 00:00:00 GMT

**This week's update**

This week, new critical vulnerabilities were disclosed in Sitecore’s Sitecore Experience Manager (XM), Sitecore Experience Platform (XP), specifically versions 9.0 through 9.3, and 10.0 through 10.4. These flaws are caused by unsafe data deserialization and code reflection, leaving affected systems at high risk of exploitation.

**Key Findings**

  * CVE-2025-53690: Remote Code Execution through Insecure Deserialization
  * CVE-2025-53691: Remote Code Execution through Insecure Deserialization
  * CVE-2025-53693: HTML Cache Poisoning through Unsafe Reflections



**Impact**

Exploitation could allow attackers to execute arbitrary code remotely on the affected system and conduct cache poisoning attacks, potentially leading to further compromise. Applying the latest vendor-released solution without delay is strongly recommended.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 588edc74df1f4609b3c2f7ef0ee2c15e | 100878| Sitecore - Remote Code Execution - CVE:CVE-2025-53691| N/A| Block| This is a new detection
CIS Managed Ruleset| d1bd7563e6254db48ce703807c5b669c | 100631| Sitecore - Cache Poisoning - CVE:CVE-2025-53693| N/A| Block| This is a new detection
CIS Managed Ruleset| ed94c7ce5301411a94a21a096c410240 | 100879| Sitecore - Remote Code Execution - CVE:CVE-2025-53690| N/A| Block| This is a new detection


## WAF - WAF Release - 2025-09-01
**Published on:** Mon, 01 Sep 2025 00:00:00 GMT

**This week's update**

This week, a critical vulnerability was disclosed in Fortinet FortiWeb (versions 7.6.3 and below, versions 7.4.7 and below, versions 7.2.10 and below, and versions 7.0.10 and below), linked to improper parameter handling that could allow unauthorized access.

**Key Findings**

  * Fortinet FortiWeb (CVE-2025-52970): A vulnerability may allow an unauthenticated remote attacker with access to non-public information to log in as any existing user on the device via a specially crafted request.



**Impact**

Exploitation could allow an unauthenticated attacker to impersonate any existing user on the device, potentially enabling them to modify system settings or exfiltrate sensitive information, posing a serious security risk. Upgrading to the latest vendor-released version is strongly recommended.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 636b145a49a84946b990d4fac49b7cf8 | 100586| Fortinet FortiWeb - Auth Bypass - CVE:CVE-2025-52970| Log| Disabled| This is a New Detection
CIS Managed Ruleset| b5ef1ace353841a0856b5e07790c9dde | 100136C| XSS - JavaScript - Headers and Body| N/A| N/A| Rule metadata description refined. Detection unchanged.


## WAF - WAF Release - 2025-08-29 - Emergency
**Published on:** Fri, 29 Aug 2025 00:00:00 GMT

**This week's update**

This week, new critical vulnerabilities were disclosed in Next.js’s image optimization functionality, exposing a broad range of production environments to risks of data exposure and cache manipulation.

**Key Findings**

  * CVE-2025-55173: Arbitrary file download from the server via image optimization.

  * CVE-2025-57752: Cache poisoning leading to unauthorized data disclosure.




**Impact**

Exploitation could expose sensitive files, leak user or backend data, and undermine application trust. Given Next.js’s wide use, immediate patching and cache hardening are strongly advised.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| ea55f8aac44246cc9b827eea9ff4bfe3 | 100613| Next.js - Dangerous File Download - CVE:CVE-2025-55173| N/A| Block| This is a new detection
CIS Managed Ruleset| e2b2d77a79cc4a76bf7ba53d69b9ea7d | 100616| Next.js - Information Disclosure - CVE:CVE-2025-57752| N/A| Block| This is a new detection


## WAF - WAF Release - 2025-08-25
**Published on:** Mon, 25 Aug 2025 00:00:00 GMT

**This week's update**

This week, critical vulnerabilities were disclosed that impact widely used open-source infrastructure, creating high-risk scenarios for code execution and operational disruption.

**Key Findings**

  * Apache HTTP Server – Code Execution (CVE-2024-38474): A flaw in Apache HTTP Server allows attackers to achieve remote code execution, enabling full compromise of affected servers. This vulnerability threatens the confidentiality, integrity, and availability of critical web services.

  * Laravel (CVE-2024-55661): A security flaw in Laravel introduces the potential for remote code execution under specific conditions. Exploitation could provide attackers with unauthorized access to application logic and sensitive backend data.




**Impact**

These vulnerabilities pose severe risks to enterprise environments and open-source ecosystems. Remote code execution enables attackers to gain deep system access, steal data, disrupt services, and establish persistent footholds for broader intrusions. Given the widespread deployment of Apache HTTP Server and Laravel in production systems, timely patching and mitigation are critical.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| c550282a0f7343ca887bdab528050359 | 100822_BETA| WordPress:Plugin:WPBookit - Remote Code Execution - CVE:CVE-2025-6058| N/A| Disabled| This was merged in to the original rule "WordPress:Plugin:WPBookit - Remote Code Execution - CVE:CVE-2025-6058" (ID: 9b5c5e13d2ca4253a89769f2194f7b2d )
CIS Managed Ruleset| 456b1e8f827b4ed89fb4a54b3bdcdbad | 100831| Apache HTTP Server - Code Execution - CVE:CVE-2024-38474| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 7dcc01e1dd074e42a26c8ca002eaac5b | 100846| Laravel - Remote Code Execution - CVE:CVE-2024-55661| Log| Disabled| This is a New Detection


## WAF - WAF Release - 2025-08-22
**Published on:** Fri, 22 Aug 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 0f3b6b9377334707b604be925fcca5c8 | 100850| Command Injection - Generic 2| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 36b0532eb3c941449afed2d3744305c4 | 100851| Remote Code Execution - Java Deserialization| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 5d3c0d0958d14512bd2a7d902b083459 | 100852| Command Injection - Generic 3| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 6e2f7a696ea74c979e7d069cefb7e5b9 | 100853| Remote Code Execution - Common Bash Bypass Beta| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 735666d7268545a5ae6cfd0b78513ad7 | 100854| XSS - Generic JavaScript| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 82780ba6f5df49dcb8d09af0e9a5daac | 100855| Command Injection - Generic 4| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 8e305924a7dc4f91a2de931a480f6093 | 100856| PHP Object Injection| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 1d34e0d05c10473ca824e66fd4ae0a33 | 100857| Generic - Parameter Fuzzing| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| b517e4b79d7a47fbb61f447b1121ee45 | 100858| Code Injection - Generic 4| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 1f9accf629dc42cb84a7a14420de01e3 | 100859| SQLi - UNION - 2| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| e95939eacf7c4484b47101d5c0177e21 | 100860| Command Injection - Generic 5| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 7b426e6f456043f4a21c162085f4d7b3 | 100861| Command Execution - Generic| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 5fac82bd1c03463fb600cfa83fa8ee7f | 100862| GraphQL Injection - 2| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| ab2cb1f2e2ad4da6a2685b1dc7a41d4b | 100863| Command Injection - Generic 6| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 549b4fe1564a448d848365d565e3c165 | 100864| Code Injection - Generic 2| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 8ef3c3f91eef46919cc9cb6d161aafdc | 100865| PHP Object Injection - 2| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 57e8ba867e6240d2af8ea0611cc3c3f8 | 100866| SQLi - LIKE 2| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| a967a167874b42b6898be46e48ac2221 | 100867| SQLi - DROP - 2| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| cf79a868cc934bcc92b86ff01f4eec13 | 100868| Code Injection - Generic 3| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 97a52405eaae47ae9627dbb22755f99e | 100869| Command Injection - Generic 7| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 5b3ce84c099040c6a25cee2d413592e2 | 100870| Command Injection - Generic 8| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 5940a9ace2f04d078e35d435d2dd41b5 | 100871| SQLi - LIKE 3| N/A| Disabled| This is a New Detection


## WAF - WAF Release - 2025-08-18
**Published on:** Mon, 18 Aug 2025 00:00:00 GMT

**This week's update**

This week, a series of critical vulnerabilities were discovered impacting core enterprise and open-source infrastructure. These flaws present a range of risks, providing attackers with distinct pathways for remote code execution, methods to breach internal network boundaries, and opportunities for critical data exposure and operational disruption.

**Key Findings**

  * SonicWall SMA (CVE-2025-32819, CVE-2025-32820, CVE-2025-32821): A remote authenticated attacker with SSLVPN user privileges can bypass path traversal protections. These vulnerabilities enable a attacker to bypass security checks to read, modify, or delete arbitrary files. An attacker with administrative privileges can escalate this further, using a command injection flaw to upload malicious files, which could ultimately force the appliance to reboot to its factory default settings.

  * Ms-Swift Project (CVE-2025-50460): An unsafe deserialization vulnerability exists in the Ms-Swift project's handling of YAML configuration files. If an attacker can control the content of a configuration file passed to the application, they can embed a malicious payload that will execute arbitrary code and it can be executed during deserialization.

  * Apache Druid (CVE-2023-25194): This vulnerability in Apache Druid allows an attacker to cause the server to connect to a malicious LDAP server. By sending a specially crafted LDAP response, the attacker can trigger an unrestricted deserialization of untrusted data. If specific "gadgets" (classes that can be abused) are present in the server's classpath, this can be escalated to achieve Remote Code Execution (RCE).

  * Tenda AC8v4 (CVE-2025-51087, CVE-2025-51088): Vulnerabilities allow an authenticated attacker to trigger a stack-based buffer overflow. By sending malformed arguments in a request to specific endpoints, an attacker can crash the device or potentially achieve arbitrary code execution.

  * Open WebUI (CVE-2024-7959): This vulnerability allows a user to change the OpenAI URL endpoint to an arbitrary internal network address without proper validation. This flaw can be exploited to access internal services or cloud metadata endpoints, potentially leading to remote command execution if the attacker can retrieve instance secrets or access sensitive internal APIs.

  * BentoML (CVE-2025-54381): The vulnerability exists in the serialization/deserialization handlers for multipart form data and JSON requests, which automatically download files from user-provided URLs without proper validation of internal network addresses. This allows attackers to fetch from unintended internal services, including cloud metadata and localhost.

  * Adobe Experience Manager Forms (CVE-2025-54254): An Improper Restriction of XML External Entity Reference ('XXE') vulnerability that could lead to arbitrary file system read in Adobe AEM (≤6.5.23).




**Impact**

These vulnerabilities affect core infrastructure, from network security appliances like SonicWall to data platforms such as Apache Druid and ML frameworks like BentoML. The code execution and deserialization flaws are particularly severe, offering deep system access that allows attackers to steal data, disrupt services, and establish a foothold for broader intrusions. Simultaneously, SSRF and XXE vulnerabilities undermine network boundaries, exposing sensitive internal data and creating pathways for lateral movement. Beyond data-centric threats, flaws in edge devices like the Tenda router introduce the tangible risk of operational disruption, highlighting a multi-faceted threat to the security and stability of key enterprise systems.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 326ebb56d46a4c269bb699d3418d9a3b | 100574| SonicWall SMA - Remote Code Execution - CVE:CVE-2025-32819, CVE:CVE-2025-32820, CVE:CVE-2025-32821| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 69f4f161dec04aca8a73a3231e6fefdb | 100576| Ms-Swift Project - Remote Code Execution - CVE:CVE-2025-50460| Log| Block| This is a New Detection
CIS Managed Ruleset| d62935357ff846d9adefb58108ac45b3 | 100585| Apache Druid - Remote Code Execution - CVE:CVE-2023-25194| Log| Block| This is a New Detection
CIS Managed Ruleset| 4f6148a760804bf8ad8ebccfe4855472 | 100834| Tenda AC8v4 - Auth Bypass - CVE:CVE-2025-51087, CVE:CVE-2025-51088| Log| Block| This is a New Detection
CIS Managed Ruleset| 1474121b01ba40629f8246f8022ab542 | 100835| Open WebUI - SSRF - CVE:CVE-2024-7959| Log| Block| This is a New Detection
CIS Managed Ruleset| 96abffdb7e224ce69ddf89eb6339f132 | 100837| SQLi - OOB| Log| Block| This is a New Detection
CIS Managed Ruleset| a0b20ec638d14800a1d6827cb83d2625 | 100841| BentoML - SSRF - CVE:CVE-2025-54381| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 40fd793035c947c5ac75add1739180d2 | 100841A| BentoML - SSRF - CVE:CVE-2025-54381 - 2| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 08dcb20b9acf47e3880a0b886ab910c2 | 100841B| BentoML - SSRF - CVE:CVE-2025-54381 - 3| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 309cfb7eeb42482e9ad896f12197ec51 | 100845| Adobe Experience Manager Forms - XSS - CVE:CVE-2025-54254| Log| Block| This is a New Detection
CIS Managed Ruleset| 6e039776c2d6418ab6e8f05196f34ce3 | 100845A| Adobe Experience Manager Forms - XSS - CVE:CVE-2025-54254 - 2| Log| Block| This is a New Detection


## WAF - WAF Release - 2025-08-11
**Published on:** Mon, 11 Aug 2025 00:00:00 GMT

This week's update focuses on a wide range of enterprise software, from network infrastructure and security platforms to content management systems and development frameworks. Flaws include unsafe deserialization, OS command injection, SSRF, authentication bypass, and arbitrary file upload — many of which allow unauthenticated remote code execution. Notable risks include Cisco Identity Services Engine and Ivanti EPMM, where successful exploitation could grant attackers full administrative control of core network infrastructure and popular web services such as WordPress, SharePoint, and Ingress-Nginx, where security bypasses and arbitrary file uploads could lead to complete site or server compromise.

**Key Findings**

  * Cisco Identity Services Engine (CVE-2025-20281): Insufficient input validation in a specific API of Cisco Identity Services Engine (ISE) and ISE-PIC allows an unauthenticated, remote attacker to execute arbitrary code with root privileges on an affected device.

  * Wazuh Server (CVE-2025-24016): An unsafe deserialization vulnerability in Wazuh Server (versions 4.4.0 to 4.9.0) allows for remote code execution and privilege escalation. By injecting unsanitized data, an attacker can trigger an exception to execute arbitrary code on the server.

  * CrushFTP (CVE-2025-54309): A flaw in AS2 validation within CrushFTP allows remote attackers to gain administrative access via HTTPS on systems not using the DMZ proxy feature. This flaw can lead to unauthorized file access and potential system compromise.

  * Kentico Xperience CMS (CVE-2025-2747, CVE-2025-2748): Vulnerabilities in Kentico Xperience CMS could enable cross-site scripting (XSS), allowing attackers to inject malicious scripts into web pages. Additionally, a flaw could allow unauthenticated attackers to bypass the Staging Sync Server's authentication, potentially leading to administrative control over the CMS.

  * Node.js (CVE-2025-27210): An incomplete fix for a previous vulnerability (CVE-2025-23084) in Node.js affects the `path.join()` API method on Windows systems. The vulnerability can be triggered using reserved Windows device names such as `CON`, `PRN`, or `AUX`.

  * WordPress:Plugin:Simple File List (CVE-2025-34085, CVE-2020-36847): This vulnerability in the Simple File List plugin for WordPress allows an unauthenticated remote attacker to upload arbitrary files to a vulnerable site. This can be exploited to achieve remote code execution on the server.
(Note: CVE-2025-34085 has been rejected as a duplicate.)

  * GeoServer (CVE-2024-29198): A Server-Side Request Forgery (SSRF) vulnerability exists in GeoServer's Demo request endpoint, which can be exploited where the Proxy Base URL has not been configured.

  * Ivanti EPMM (CVE-2025-6771): An OS command injection vulnerability in Ivanti Endpoint Manager Mobile (EPMM) before versions 12.5.0.2, 12.4.0.3, and 12.3.0.3 allows a remote, authenticated attacker with high privileges to execute arbitrary code.

  * Microsoft SharePoint (CVE-2024-38018): This is a remote code execution vulnerability affecting Microsoft SharePoint Server.

  * Manager-IO (CVE-2025-54122): A critical unauthenticated full read Server-Side Request Forgery (SSRF) vulnerability is present in the proxy handler of both Manager Desktop and Server editions up to version 25.7.18.2519. This allows an unauthenticated attacker to bypass network isolation and access internal services.

  * Ingress-Nginx (CVE-2025-1974): A vulnerability in the Ingress-Nginx controller for Kubernetes allows an attacker to bypass access control rules. An unauthenticated attacker with access to the pod network can achieve arbitrary code execution in the context of the ingress-nginx controller.

  * PaperCut NG/MF (CVE-2023-2533): A Cross-Site Request Forgery (CSRF) vulnerability has been identified in PaperCut NG/MF. Under specific conditions, an attacker could exploit this to alter security settings or execute arbitrary code if they can deceive an administrator with an active login session into clicking a malicious link.

  * SonicWall SMA (CVE-2025-40598): This vulnerability could allow an unauthenticated attacker to bypass security controls. This allows a remote, unauthenticated attacker to potentially execute arbitrary JavaScript code.

  * WordPress (CVE-2025-5394): The "Alone – Charity Multipurpose Non-profit WordPress Theme" for WordPress is vulnerable to arbitrary file uploads. A missing capability check allows unauthenticated attackers to upload ZIP files containing webshells disguised as plugins, leading to remote code execution.




**Impact**

These vulnerabilities span a broad range of enterprise technologies, including network access control systems, monitoring platforms, web servers, CMS platforms, cloud services, and collaboration tools. Exploitation techniques range from remote code execution and command injection to authentication bypass, SQL injection, path traversal, and configuration weaknesses.

A critical flaw in perimeter devices like Ivanti EPMM or SonicWall SMA could allow an unauthenticated attacker to gain remote code execution, completely breaching the primary network defense. A separate vulnerability within Cisco's Identity Services Engine could then be exploited to bypass network segmentation, granting an attacker widespread internal access. Insecure deserialization issues in platforms like Wazuh Server and CrushFTP could then be used to run malicious payloads or steal sensitive files from administrative consoles. Weaknesses in web delivery controllers like Ingress-Nginx or popular content management systems such as WordPress, SharePoint, and Kentico Xperience create vectors to bypass security controls, exfiltrate confidential data, or fully compromise servers.










Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| ec6480c81253494b947d891e51bc8df1 | 100538| GeoServer - SSRF - CVE:CVE-2024-29198| Log| Block| This is a New Detection
CIS Managed Ruleset| b8cb07170b5e4c2b989119cac9e0b290 | 100548| Ivanti EPMM - Remote Code Execution - CVE:CVE-2025-6771| Log| Block| This is a New Detection
CIS Managed Ruleset| b3524bf5f5174b65bc892122ad93cda8 | 100550| Microsoft SharePoint - Remote Code Execution - CVE:CVE-2024-38018| Log| Block| This is a New Detection
CIS Managed Ruleset| e1369c5d629f4f10a14141381dca5738 | 100562| Manager-IO - SSRF - CVE:CVE-2025-54122| Log| Block| This is a New Detection
CIS Managed Ruleset| 136f67e2b6a84f15ab9a82a52e9137e1 | 100565| Cisco Identity Services Engine - Remote Code Execution - CVE:CVE-2025-20281| Log| Block| This is a New Detection
CIS Managed Ruleset| ed759f7e44184fa398ef71785d8102e1 | 100567| Ingress-Nginx - Remote Code Execution - CVE:CVE-2025-1974| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 71b8e7b646f94d79873213cd99105c43 | 100569| PaperCut NG/MF - Remote Code Execution - CVE:CVE-2023-2533| Log| Block| This is a New Detection
CIS Managed Ruleset| 2450bfbb0cfb4804b109d1c42c81dc88 | 100571| SonicWall SMA - XSS - CVE:CVE-2025-40598| Log| Block| This is a New Detection
CIS Managed Ruleset| 8ce1903b67e24205a93f5fe6926c96d4 | 100573| WordPress - Dangerous File Upload - CVE:CVE-2025-5394| Log| Block| This is a New Detection
CIS Managed Ruleset| 7fdb3c7bc7b74703aeef4ab240ec2fda | 100806 | Wazuh Server - Remote Code Execution - CVE:CVE-2025-24016 | Log | Block | This is a New Detection
CIS Managed Ruleset| fe088163f51f4928a3c8d91e2401fa3b | 100824 | CrushFTP - Remote Code Execution - CVE:CVE-2025-54309 | Log | Block | This is a New Detection
CIS Managed Ruleset| 3638baed75924604987b86d874920ace | 100824A | CrushFTP - Remote Code Execution - CVE:CVE-2025-54309 - 2 | Log | Block | This is a New Detection
CIS Managed Ruleset| dda4f95b3a3e4ebb9e194aa5c7e63549 | 100825| AMI MegaRAC - Auth Bypass - CVE:CVE-2024-54085| Log| Block| This is a New Detection
CIS Managed Ruleset| 7dc07014cefa4ce9adf21da7b79037e6 | 100826| Kentico Xperience CMS - Auth Bypass - CVE:CVE-2025-2747| Log| Block| This is a New Detection
CIS Managed Ruleset| 7c7a0a37e79a4949ba840c9acaf261aa | 100827| Kentico Xperience CMS - XSS - CVE:CVE-2025-2748| Log| Block| This is a New Detection
CIS Managed Ruleset| 54dd826f578c483196ce852b6f1c2d12 | 100828| Node.js - Directory Traversal - CVE:CVE-2025-27210| Log| Block| This is a New Detection
CIS Managed Ruleset| a2867f7456c14213a94509a40341fccc | 100829| WordPress:Plugin:Simple File List - Remote Code Execution - CVE:CVE-2025-34085| Log| Block| This is a New Detection
CIS Managed Ruleset| 4cdb0e792d1a428a897526624cefeeda | 100829A| WordPress:Plugin:Simple File List - Remote Code Execution - CVE:CVE-2025-34085 - 2| Log| Disabled| This is a New Detection


## WAF - WAF Release - 2025-08-07 - Emergency
**Published on:** Thu, 07 Aug 2025 00:00:00 GMT

This week’s highlight focuses on two critical vulnerabilities affecting key infrastructure and enterprise content management platforms. Both flaws present significant remote code execution risks that can be exploited with minimal or no user interaction.

**Key Findings**

  * Squid (≤6.3) — CVE-2025-54574: A heap buffer overflow occurs when processing Uniform Resource Names (URNs). This vulnerability may allow remote attackers to execute arbitrary code on the server. The issue has been resolved in version 6.4.

  * Adobe AEM (≤6.5.23) — CVE-2025-54253: Due to a misconfiguration, attackers can achieve remote code execution without requiring any user interaction, posing a severe threat to affected deployments.




**Impact**

Both vulnerabilities expose critical attack vectors that can lead to full server compromise. The Squid heap buffer overflow allows remote code execution by crafting malicious URNs, which can lead to server takeover or denial of service. Given Squid’s widespread use as a caching proxy, this flaw could be exploited to disrupt network traffic or gain footholds inside secure environments.

Adobe AEM’s remote code execution vulnerability enables attackers to run arbitrary code on the content management server without any user involvement. This puts sensitive content, application integrity, and the underlying infrastructure at extreme risk. Exploitation could lead to data theft, defacement, or persistent backdoor installation.

These findings reinforce the urgency of updating to the patched versions — Squid 6.4 and Adobe AEM 6.5.24 or later — and reviewing configurations to prevent exploitation.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| f61ed7c1e7e24c3380289e41ef7e015b | 100844| Adobe Experience Manager Forms - Remote Code Execution - CVE:CVE-2025-54253| N/A| Block| This is a New Detection
CIS Managed Ruleset| e76e65f5a3aa43f49e0684a6baec057a | 100840| Squid - Buffer Overflow - CVE:CVE-2025-54574| N/A| Block| This is a New Detection


## WAF - WAF Release - 2025-08-04
**Published on:** Mon, 04 Aug 2025 00:00:00 GMT

This week's highlight focuses on a series of significant vulnerabilities identified across widely adopted web platforms, from enterprise-grade CMS to essential backend administration tools. The findings reveal multiple vectors for attack, including critical flaws that allow for full server compromise and others that enable targeted attacks against users.

**Key Findings**

  * Sitecore (CVE-2025-34509, CVE-2025-34510, CVE-2025-34511): A hardcoded credential allows remote attackers to access administrative APIs. Once authenticated, they can exploit an additional vulnerability to upload arbitrary files, leading to remote code execution.

  * Grafana (CVE-2025-4123): A cross-site scripting (XSS) vulnerability allows an attacker to redirect users to a malicious website, which can then execute arbitrary JavaScript in the victim's browser.

  * LaRecipe (CVE-2025-53833): Through Server-Side Template Injection, attackers can execute arbitrary commands on the server, potentially access sensitive environment variables, and escalate access depending on server configuration.

  * CentOS WebPanel (CVE-2025-48703): A command injection vulnerability could allow a remote attacker to execute arbitrary commands on the server.

  * WordPress (CVE-2023-5561): This vulnerability allows unauthenticated attackers to determine the email addresses of users who have published public posts on an affected website.

  * WordPress Plugin - WPBookit (CVE-2025-6058): A missing file type validation allows unauthenticated attackers to upload arbitrary files to the server, creating the potential for remote code execution.

  * WordPress Theme - Motors (CVE-2025-4322): Due to improper identity validation, an unauthenticated attacker can change the passwords of arbitrary users, including administrators, to gain access to their accounts.




**Impact**

These vulnerabilities pose a multi-layered threat to widely adopted web technologies, ranging from enterprise-grade platforms like Sitecore to everyday solutions such as WordPress, and backend tools like CentOS WebPanel. The most severe risks originate in remote code execution (RCE) flaws found in Sitecore, CentOS WebPanel, LaRecipe, and the WPBookit plugin. These allow attackers to bypass security controls and gain deep access to the server, enabling them to steal sensitive data, deface websites, install persistent malware, or use the compromised server as a launchpad for further attacks.

The privilege escalation vulnerability is the Motors theme, which allows for a complete administrative account takeover on WordPress sites. This effectively hands control of the application to an attacker, who can then manipulate content, exfiltrate user data, and alter site functionality without needing to breach the server itself.

The Grafana cross-site scripting (XSS) flaw can be used to hijack authenticated user sessions or steal credentials, turning a trusted user's browser into an attack vector.

Meanwhile, the information disclosure flaw in WordPress core provides attackers with valid user emails, fueling targeted phishing campaigns that aim to secure the same account access achievable through the other exploits.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| b8ab4644f8044f3485441ee052f30a13 | 100535A| Sitecore - Dangerous File Upload - CVE:CVE-2025-34510, CVE:CVE-2025-34511| Log| Block| This is a New Detection
CIS Managed Ruleset| 06d1fe0bd6e44d868e6b910b5045a97f | 100535| Sitecore - Information Disclosure - CVE:CVE-2025-34509| Log| Block| This is a New Detection
CIS Managed Ruleset| f71ce87ea6e54eab999223df579cd3e0 | 100543| Grafana - Directory Traversal - CVE:CVE-2025-4123| Log| Block| This is a New Detection
CIS Managed Ruleset| bba3d37891a440fb8bc95b970cbd9abc | 100545| WordPress - Information Disclosure - CVE:CVE-2023-5561| Log| Block| This is a New Detection
CIS Managed Ruleset| 28108d25f1cf470c8e7648938f634977 | 100820| CentOS WebPanel - Remote Code Execution - CVE:CVE-2025-48703| Log| Block| This is a New Detection
CIS Managed Ruleset| 9d69c796a61444a3aca33dc282ae64c1 | 100821| LaRecipe - SSTI - CVE:CVE-2025-53833| Log| Block| This is a New Detection
CIS Managed Ruleset| 9b5c5e13d2ca4253a89769f2194f7b2d | 100822| WordPress:Plugin:WPBookit - Remote Code Execution - CVE:CVE-2025-6058| Log| Block| This is a New Detection
CIS Managed Ruleset| 69d43d704b0641898141a4300bf1b661 | 100823| WordPress:Theme:Motors - Privilege Escalation - CVE:CVE-2025-4322| Log| Block| This is a New Detection


## WAF - WAF Release - 2025-07-28
**Published on:** Mon, 28 Jul 2025 00:00:00 GMT

This week’s update spotlights several vulnerabilities across Apache Tomcat, MongoDB, and Fortinet FortiWeb. Several flaws related with a memory leak in Apache Tomcat can lead to a denial-of-service attack. Additionally, a code injection flaw in MongoDB's Mongoose library allows attackers to bypass security controls to access restricted data.

**Key Findings**

  * Fortinet FortiWeb (CVE-2025-25257): An improper neutralization of special elements used in a SQL command vulnerability in Fortinet FortiWeb versions allows an unauthenticated attacker to execute unauthorized SQL code or commands.

  * Apache Tomcat (CVE-2025-31650): A improper Input Validation vulnerability in Apache Tomcat that could create memory leak when incorrect error handling for some invalid HTTP priority headers resulted in incomplete clean-up of the failed request.

  * MongoDB (CVE-2024-53900, CVE:CVE-2025-23061): Improper use of `$where` in match and a nested `$where` filter with a `populate()` match in Mongoose can lead to search injection.




**Impact**

These vulnerabilities target user-facing components, web application servers, and back-end databases. A SQL injection flaw in Fortinet FortiWeb can lead to data theft or system compromise. A separate issue in Apache Tomcat involves a memory leak from improper input validation, which could be exploited for a denial-of-service (DoS) attack. Finally, a vulnerability in MongoDB's Mongoose library allows attackers to bypass security filters and access unauthorized data through malicious search queries.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 6ab3bd3b58fb4325ac2d3cc73461ec9e | 100804| BerriAI - SSRF - CVE:CVE-2024-6587| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 2e6c4d02f42a4c3ca90649d50cb13e1d | 100812| Fortinet FortiWeb - Remote Code Execution - CVE:CVE-2025-25257| Log| Block| This is a New Detection
CIS Managed Ruleset| fd360d8fd9994e6bab6fb06067fae7f7 | 100813| Apache Tomcat - DoS - CVE:CVE-2025-31650| Log| Disabled| This is a New Detection
CIS Managed Ruleset| f9e01e28c5d6499cac66364b4b6a5bb1 | 100815| MongoDB - Remote Code Execution - CVE:CVE-2024-53900, CVE:CVE-2025-23061| Log| Block| This is a New Detection
CIS Managed Ruleset| 700d4fcc7b1f481a80cbeee5688f8e79 | 100816| MongoDB - Remote Code Execution - CVE:CVE-2024-53900, CVE:CVE-2025-23061| Log| Block| This is a New Detection


## WAF - WAF Release - 2025-07-21 - Emergency
**Published on:** Mon, 21 Jul 2025 00:00:00 GMT

This week's update highlights several high-impact vulnerabilities affecting Microsoft SharePoint Server. These flaws, involving unsafe deserialization, allow unauthenticated remote code execution over the network, posing a critical threat to enterprise environments relying on SharePoint for collaboration and document management.

**Key Findings**

  * Microsoft SharePoint Server (CVE-2025-53770): A critical vulnerability involving unsafe deserialization of untrusted data, enabling unauthenticated remote code execution over the network. This flaw allows attackers to execute arbitrary code on vulnerable SharePoint servers without user interaction.
  * Microsoft SharePoint Server (CVE-2025-53771): A closely related deserialization issue that can be exploited by unauthenticated attackers, potentially leading to full system compromise. The vulnerability highlights continued risks around insecure serialization logic in enterprise collaboration platforms.



**Impact**

Together, these vulnerabilities significantly weaken the security posture of on-premise Microsoft SharePoint Server deployments. By enabling remote code execution without authentication, they open the door for attackers to gain persistent access, deploy malware, and move laterally across enterprise environments.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 34dac2b38b904163bc587cc32168f6f0 | 100817| Microsoft SharePoint - Deserialization - CVE:CVE-2025-53770| N/A| Block| This is a New Detection
CIS Managed Ruleset| d21f327516a145bc9d1b05678de656c4 | 100818| Microsoft SharePoint - Deserialization - CVE:CVE-2025-53771| N/A| Block| This is a New Detection

For more details, also refer to [our blog](https://blog.cloudflare.com/cloudflare-protects-against-critical-sharepoint-vulnerability-cve-2025-53770/).


## WAF - WAF Release - 2025-07-21
**Published on:** Mon, 21 Jul 2025 00:00:00 GMT

This week's update spotlights several critical vulnerabilities across Citrix NetScaler Memory Disclosure, FTP servers and network application. Several flaws enable unauthenticated remote code execution or sensitive data exposure, posing a significant risk to enterprise security.

**Key Findings**

  * Wing FTP Server (CVE-2025-47812): A critical Remote Code Execution (RCE) vulnerability that enables unauthenticated attackers to execute arbitrary code with root/SYSTEM-level privileges by exploiting a Lua injection flaw.
  * Infoblox NetMRI (CVE-2025-32813): A remote unauthenticated command injection flaw that allows an attacker to execute arbitrary commands, potentially leading to unauthorized access.
  * Citrix Netscaler ADC (CVE-2025-5777, CVE-2023-4966): A sensitive information disclosure vulnerability, also known as "Citrix Bleed2", that allows the disclosure of memory and subsequent remote access session hijacking.
  * Akamai CloudTest (CVE-2025-49493): An XML External Entity (XXE) injection that could lead to read local files on the system by manipulating XML input.



**Impact**

These vulnerabilities affect critical enterprise infrastructure, from file transfer services and network management appliances to application delivery controllers. The Wing FTP RCE and Infoblox command injection flaws offer direct paths to deep system compromise, while the Citrix "Bleed2" and Akamai XXE vulnerabilities undermine system integrity by enabling session hijacking and sensitive data theft.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 6ab3bd3b58fb4325ac2d3cc73461ec9e | 100804| BerriAI - SSRF - CVE:CVE-2024-6587| Log| Log| This is a New Detection
CIS Managed Ruleset| 0e17d8761f1a47d5a744a75b5199b58a | 100805| Wing FTP Server - Remote Code Execution - CVE:CVE-2025-47812| Log| Block| This is a New Detection
CIS Managed Ruleset| 81ace5a851214a2f9c58a1e7919a91a4 | 100807| Infoblox NetMRI - Command Injection - CVE:CVE-2025-32813| Log| Block| This is a New Detection
CIS Managed Ruleset| cd8fa74e8f6f476c9380ae217899130f | 100808| Citrix Netscaler ADC - Buffer Error - CVE:CVE-2025-5777| Log| Disabled| This is a New Detection
CIS Managed Ruleset| e012c7bece304a1daf80935ed1cf8e08 | 100809| Citrix Netscaler ADC - Information Disclosure - CVE:CVE-2023-4966| Log| Block| This is a New Detection
CIS Managed Ruleset| 5d348a573a834ffd968faffc6e70469f | 100810| Akamai CloudTest - XXE - CVE:CVE-2025-49493| Log| Block| This is a New Detection


## WAF - WAF Release - 2025-07-14
**Published on:** Mon, 14 Jul 2025 00:00:00 GMT

This week’s vulnerability analysis highlights emerging web application threats that exploit modern JavaScript behavior and SQL parsing ambiguities. Attackers continue to refine techniques such as attribute overloading and obfuscated logic manipulation to evade detection and compromise front-end and back-end systems.

**Key Findings**

  * XSS – Attribute Overloading: A novel cross-site scripting technique where attackers abuse custom or non-standard HTML attributes to smuggle payloads into the DOM. These payloads evade traditional sanitization logic, especially in frameworks that loosely validate attributes or trust unknown tokens.
  * XSS – onToggle Event Abuse: Exploits the lesser-used onToggle event (triggered by elements like `<details>`) to execute arbitrary JavaScript when users interact with UI elements. This vector is often overlooked by static analyzers and can be embedded in seemingly benign components.



**Impact**

These vulnerabilities target both user-facing components and back-end databases, introducing potential vectors for credential theft, session hijacking, or full data exfiltration. The XSS variants bypass conventional filters through overlooked HTML behaviors, while the obfuscated SQLi enables attackers to stealthily probe back-end logic, making them especially difficult to detect and block.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| a8918353372b4191b10684eb2aa3d845 | 100798| XSS - Attribute Overloading| Log| Block| This is a New Detection
CIS Managed Ruleset| 31dd299ba375414dac9260c037548d06 | 100799| XSS - OnToggle| Log| Block| This is a New Detection


## WAF - Increased IP List Limits for Enterprise Accounts
**Published on:** Mon, 07 Jul 2025 00:00:00 GMT

We have significantly increased the limits for [IP Lists](https://developers.cloudflare.com/waf/tools/lists/) on Enterprise plans to provide greater flexibility and control:

  * **Total number of lists** : Increased from 10 to 1,000.
  * **Total number of list items** : Increased from 10,000 to 500,000.



Limits for other list types and plans remain unchanged. For more details, refer to the [lists availability](https://developers.cloudflare.com/waf/tools/lists/#availability).


## WAF - WAF Release - 2025-07-07
**Published on:** Mon, 07 Jul 2025 00:00:00 GMT

This week’s roundup uncovers critical vulnerabilities affecting enterprise VoIP systems, webmail platforms, and a popular JavaScript framework. The risks range from authentication bypass to remote code execution (RCE) and buffer handling flaws, each offering attackers a path to elevate access or fully compromise systems.

**Key Findings**

  * Next.js - Auth Bypass: A newly detected authentication bypass flaw in the Next.js framework allows attackers to access protected routes or APIs without proper authorization, undermining application access controls.
  * Fortinet FortiVoice (CVE-2025-32756): A buffer error vulnerability in FortiVoice systems that could lead to memory corruption and potential code execution or service disruption in enterprise telephony environments.
  * Roundcube (CVE-2025-49113): A critical RCE flaw allowing unauthenticated attackers to execute arbitrary PHP code via crafted requests, leading to full compromise of mail servers and user inboxes.



**Impact**

These vulnerabilities affect core business infrastructure, from web interfaces to voice communications and email platforms. The Roundcube RCE and FortiVoice buffer flaw offer potential for deep system access, while the Next.js auth bypass undermines trust boundaries in modern web apps.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| b6558cac8c874bd6878734057eb35ee6 | 100795| Next.js - Auth Bypass| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 58fcf6d9c05d4b7a8f41e0a3c329aeb0 | 100796| Fortinet FortiVoice - Buffer Error - CVE:CVE-2025-32756| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 34ed0624bc864ea88bbea55bab314023 | 100797| Roundcube - Remote Code Execution - CVE:CVE-2025-49113| Log| Disabled| This is a New Detection


## WAF - WAF Release - 2025-06-16
**Published on:** Mon, 16 Jun 2025 00:00:00 GMT

This week’s roundup highlights multiple critical vulnerabilities across popular web frameworks, plugins, and enterprise platforms. The focus lies on remote code execution (RCE), server-side request forgery (SSRF), and insecure file upload vectors that enable full system compromise or data exfiltration.

**Key Findings**

  * Cisco IOS XE (CVE-2025-20188): Critical RCE vulnerability enabling unauthenticated attackers to execute arbitrary commands on network infrastructure devices, risking total router compromise.
  * Axios (CVE-2024-39338): SSRF flaw impacting server-side request control, allowing attackers to manipulate internal service requests when misconfigured with unsanitized user input.
  * vBulletin (CVE-2025-48827, CVE-2025-48828): Two high-impact RCE flaws enabling attackers to remotely execute PHP code, compromising forum installations and underlying web servers.
  * Invision Community (CVE-2025-47916): A critical RCE vulnerability allowing authenticated attackers to run arbitrary code in community platforms, threatening data and lateral movement risk.
  * CrushFTP (CVE-2025-32102, CVE-2025-32103): SSRF vulnerabilities in upload endpoint processing permit attackers to pivot internal network scans and abuse internal services.
  * Roundcube (CVE-2025-49113): RCE via email processing enables attackers to execute code upon viewing a crafted email — particularly dangerous for webmail deployments.
  * WooCommerce WordPress Plugin (CVE-2025-47577): Dangerous file upload vulnerability permits unauthenticated users to upload executable payloads, leading to full WordPress site takeover.
  * Cross-Site Scripting (XSS) Detection Improvements: Enhanced detection patterns.



**Impact**

These vulnerabilities span core systems — from routers to e-commerce to email. RCE in Cisco IOS XE, Roundcube, and vBulletin poses full system compromise. SSRF in Axios and CrushFTP supports internal pivoting, while WooCommerce’s file upload bug opens doors to mass WordPress exploitation.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 233bcf0ce50f400989a7e44a35fefd53 | 100783| Cisco IOS XE - Remote Code Execution - CVE:CVE-2025-20188| Log| Block| This is a New Detection
CIS Managed Ruleset| 9284e3b1586341acb4591bfd8332af5d | 100784| Axios - SSRF - CVE:CVE-2024-39338| Log| Block| This is a New Detection
CIS Managed Ruleset| 2672b175a25548aa8e0107b12e1648d2 | 100785| vBulletin - Remote Code Execution - CVE:CVE-2025-48827, CVE:CVE-2025-48828| Log| Block| This is a New Detection
CIS Managed Ruleset| b77a19fb053744b49eacdab00edcf1ef | 100786| Invision Community - Remote Code Execution - CVE:CVE-2025-47916| Log| Block| This is a New Detection
CIS Managed Ruleset| aec2274743064523a9667248d6f5eb48 | 100791| CrushFTP - SSRF - CVE:CVE-2025-32102, CVE:CVE-2025-32103| Log| Block| This is a New Detection
CIS Managed Ruleset| 7b80e1f5575d4d99bb7d56ae30baa18a | 100792| Roundcube - Remote Code Execution - CVE:CVE-2025-49113| Log| Block| This is a New Detection
CIS Managed Ruleset| 52d76f9394494b0382c7cb00229ba236 | 100793| XSS - Ontoggle| Log| Disabled| This is a New Detection
CIS Managed Ruleset| d38e657bd43f4d809c28157dfa338296 | 100794| WordPress WooCommerce Plugin - Dangerous File Upload - CVE:CVE-2025-47577| Log| Block| This is a New Detection


## WAF - WAF Release - 2025-06-09
**Published on:** Mon, 09 Jun 2025 00:00:00 GMT

This week’s update spotlights four critical vulnerabilities across CMS platforms, VoIP systems, and enterprise applications. Several flaws enable remote code execution or privilege escalation, posing significant enterprise risks.

**Key Findings**

  * WordPress OttoKit Plugin (CVE-2025-27007): Privilege escalation flaw allows unauthenticated attackers to create or elevate user accounts, compromising WordPress administrative control.
  * SAP NetWeaver (CVE-2025-42999): Remote Code Execution vulnerability enables attackers to execute arbitrary code on SAP NetWeaver systems, threatening core ERP and business operations.
  * Fortinet FortiVoice (CVE-2025-32756): Buffer error vulnerability may lead to memory corruption and potential code execution, directly impacting enterprise VoIP infrastructure.
  * Camaleon CMS (CVE-2024-46986): Remote Code Execution vulnerability allows attackers to gain full control over Camaleon CMS installations, exposing hosted content and underlying servers.



**Impact**

These vulnerabilities target widely deployed CMS, ERP, and VoIP systems. RCE flaws in SAP NetWeaver and Camaleon CMS allow full takeover of business-critical applications. Privilege escalation in OttoKit exposes WordPress environments to full administrative compromise. FortiVoice buffer handling issues risk destabilizing or fully compromising enterprise telephony systems.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 4afd50a3ef1948bba87c4e620debd86e | 100769| WordPress OttoKit Plugin - Privilege Escalation - CVE:CVE-2025-27007| Log| Block| This is a New Detection
CIS Managed Ruleset| 24134c41c3e940daa973b4b95f57b448 | 100770| SAP NetWeaver - Remote Code Execution - CVE:CVE-2025-42999| Log| Block| This is a New Detection
CIS Managed Ruleset| 4f219ac0be3545a5be5f0bf34df8857a | 100779| Fortinet FortiVoice - Buffer Error - CVE:CVE-2025-32756| Log| Block| This is a New Detection
CIS Managed Ruleset| bc8dfbe8cbac4c039725ec743b840107 | 100780| Camaleon CMS - Remote Code Execution - CVE:CVE-2024-46986| Log| Block| This is a New Detection


## WAF - WAF Release - 2025-06-02
**Published on:** Mon, 02 Jun 2025 00:00:00 GMT

This week’s roundup highlights five high-risk vulnerabilities affecting SD-WAN, load balancers, and AI platforms. Several flaws enable unauthenticated remote code execution or authentication bypass.

**Key Findings**

  * Versa Concerto SD-WAN (CVE-2025-34026, CVE-2025-34027): Authentication bypass vulnerabilities allow attackers to gain unauthorized access to SD-WAN management interfaces, compromising network segmentation and control.
  * Kemp LoadMaster (CVE-2024-7591): Remote Code Execution vulnerability enables attackers to execute arbitrary commands, potentially leading to full device compromise within enterprise load balancing environments.
  * AnythingLLM (CVE-2024-0759): Server-Side Request Forgery (SSRF) flaw allows external attackers to force the LLM backend to make unauthorized internal network requests, potentially exposing sensitive internal resources.
  * Anyscale Ray (CVE-2023-48022): Remote Code Execution vulnerability affecting distributed AI workloads, allowing attackers to execute arbitrary code on Ray cluster nodes.
  * Server-Side Request Forgery (SSRF) - Generic & Obfuscated Payloads: Ongoing advancements in SSRF payload techniques observed, including obfuscation and expanded targeting of cloud metadata services and internal IP ranges.



**Impact**

These vulnerabilities expose critical infrastructure across networking, AI platforms, and SaaS integrations. Unauthenticated RCE and auth bypass flaws in Versa Concerto, Kemp LoadMaster, and Anyscale Ray allow full system compromise. AnythingLLM and SSRF payload variants expand attack surfaces into internal cloud resources, sensitive APIs, and metadata services, increasing risk of privilege escalation, data theft, and persistent access.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 752cfb5e6f9c46f0953c742139b52f02 | 100764| Versa Concerto SD-WAN - Auth Bypass - CVE:CVE-2025-34027| Log| Block| This is a New Detection
CIS Managed Ruleset| a01171de18034901b48a5549a34edb97 | 100765| Versa Concerto SD-WAN - Auth Bypass - CVE:CVE-2025-34026| Log| Block| This is a New Detection
CIS Managed Ruleset| 840b35492a7543c18ffe50fc0d99b2db | 100766| Kemp LoadMaster - Remote Code Execution - CVE:CVE-2024-7591| Log| Block| This is a New Detection
CIS Managed Ruleset| 121b7070de3a459dbe80d7ed95aa3a4f | 100767| AnythingLLM - SSRF - CVE:CVE-2024-0759| Log| Block| This is a New Detection
CIS Managed Ruleset| 215417f989e2485a9c50eca0840a0966 | 100768| Anyscale Ray - Remote Code Execution - CVE:CVE-2023-48022| Log| Block| This is a New Detection
CIS Managed Ruleset| 3ed619a17d4141bda3a8c3869d16ee18 | 100781| SSRF - Generic Payloads| N/A| Disabled| This is a New Detection
CIS Managed Ruleset| 7ce73f6a70be49f8944737465c963d9d | 100782| SSRF - Obfuscated Payloads| N/A| Disabled| This is a New Detection


## WAF - Updated attack score model
**Published on:** Wed, 28 May 2025 00:00:00 GMT

We have deployed an updated attack score model focused on enhancing the detection of multiple false positives (FPs).

As a result of this improvement, some changes in observed attack scores are expected.


## WAF - WAF Release - 2025-05-27
**Published on:** Tue, 27 May 2025 00:00:00 GMT

This week’s roundup covers nine vulnerabilities, including six critical RCEs and one dangerous file upload. Affected platforms span cloud services, CI/CD pipelines, CMSs, and enterprise backup systems. Several are now addressed by updated WAF managed rulesets.

**Key Findings**

  * Ingress-Nginx (CVE-2025-1098): Unauthenticated RCE via unsafe annotation handling. Impacts Kubernetes clusters.
  * GitHub Actions (CVE-2025-30066): RCE through malicious workflow inputs. Targets CI/CD pipelines.
  * Craft CMS (CVE-2025-32432): Template injection enables unauthenticated RCE. High risk to content-heavy sites.
  * F5 BIG-IP (CVE-2025-31644): RCE via TMUI exploit, allowing full system compromise.
  * AJ-Report (CVE-2024-15077): RCE through untrusted template execution. Affects reporting dashboards.
  * NAKIVO Backup (CVE-2024-48248): RCE via insecure script injection. High-value target for ransomware.
  * SAP NetWeaver (CVE-2025-31324): Dangerous file upload flaw enables remote shell deployment.
  * Ivanti EPMM (CVE-2025-4428, 4427): Auth bypass allows full access to mobile device management.
  * Vercel (CVE-2025-32421): Information leak via misconfigured APIs. Useful for attacker recon.



**Impact**

These vulnerabilities expose critical components across Kubernetes, CI/CD pipelines, and enterprise systems to severe threats including unauthenticated remote code execution, authentication bypass, and information leaks. High-impact flaws in Ingress-Nginx, Craft CMS, F5 BIG-IP, and NAKIVO Backup enable full system compromise, while SAP NetWeaver and AJ-Report allow remote shell deployment and template-based attacks. Ivanti EPMM’s auth bypass further risks unauthorized control over mobile device fleets.

GitHub Actions and Vercel introduce supply chain and reconnaissance risks, allowing malicious workflow inputs and data exposure that aid in targeted exploitation. Organizations should prioritize immediate patching, enhance monitoring, and deploy updated WAF and IDS signatures to defend against likely active exploitation.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 6a61a14f44af4232a44e45aad127592a | 100746| Vercel - Information Disclosure| Log| Disabled| This is a New Detection
CIS Managed Ruleset| bd30b3c43eb44335ab6013c195442495 | 100754| AJ-Report - Remote Code Execution - CVE:CVE-2024-15077| Log| Block| This is a New Detection
CIS Managed Ruleset| 6a13bd6e5fc94b1d9c97eb87dfee7ae4 | 100756| NAKIVO Backup - Remote Code Execution - CVE:CVE-2024-48248| Log| Block| This is a New Detection
CIS Managed Ruleset| a4af6f2f15c9483fa9eab01d1c52f6d0 | 100757| Ingress-Nginx - Remote Code Execution - CVE:CVE-2025-1098| Log| Disabled| This is a New Detection
CIS Managed Ruleset| bd30b3c43eb44335ab6013c195442495 | 100759| SAP NetWeaver - Dangerous File Upload - CVE:CVE-2025-31324| Log| Block| This is a New Detection
CIS Managed Ruleset| dab2df4f548349e3926fee845366ccc1 | 100760| Craft CMS - Remote Code Execution - CVE:CVE-2025-32432| Log| Block| This is a New Detection
CIS Managed Ruleset| 5eb23f172ed64ee08895e161eb40686b | 100761| GitHub Action - Remote Code Execution - CVE:CVE-2025-30066| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 827037f2d5f941789efcba6260fc041c | 100762| Ivanti EPMM - Auth Bypass - CVE:CVE-2025-4428, CVE:CVE-2025-4427| Log| Block| This is a New Detection
CIS Managed Ruleset| ddee6d1c4f364768b324609cebafdfe6 | 100763| F5 Big IP - Remote Code Execution - CVE:CVE-2025-31644| Log| Disabled| This is a New Detection


## WAF - WAF Release - 2025-05-19
**Published on:** Mon, 19 May 2025 00:00:00 GMT

This week's analysis covers four vulnerabilities, with three rated critical due to their Remote Code Execution (RCE) potential. One targets a high-traffic frontend platform, while another targets a popular content management system. These detections are now part of the CIS Managed Ruleset in _Block_ mode.

**Key Findings**

  * Commvault Command Center (CVE-2025-34028) exposes an unauthenticated RCE via insecure command injection paths in the web UI. This is critical due to its use in enterprise backup environments.
  * BentoML (CVE-2025-27520) reveals an exploitable vector where serialized payloads in model deployment APIs can lead to arbitrary command execution. This targets modern AI/ML infrastructure.
  * Craft CMS (CVE-2024-56145) allows RCE through template injection in unauthenticated endpoints. It poses a significant risk for content-heavy websites with plugin extensions.
  * Apache HTTP Server (CVE-2024-38475) discloses sensitive server config data due to misconfigured `mod_proxy` behavior. While not RCE, this is useful for pre-attack recon.



**Impact**

These newly detected vulnerabilities introduce critical risk across modern web stacks, AI infrastructure, and content platforms: unauthenticated RCEs in Commvault, BentoML, and Craft CMS enable full system compromise with minimal attacker effort.

Apache HTTPD information leak can support targeted reconnaissance, increasing the success rate of follow-up exploits. Organizations using these platforms should prioritize patching and monitor for indicators of exploitation using updated WAF detection rules.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 5c3559ad62994e5b932d7d0075129820 | 100745| Apache HTTP Server - Information Disclosure - CVE:CVE-2024-38475| Log| Block| This is a New Detection
CIS Managed Ruleset| 28a22a685bba478d99bc904526a517f1 | 100747| Commvault Command Center - Remote Code Execution - CVE:CVE-2025-34028| Log| Block| This is a New Detection
CIS Managed Ruleset| 2e6bb954d0634e368c49d7d1d7619ccb | 100749| BentoML - Remote Code Execution - CVE:CVE-2025-27520| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 91250eebec894705b62305b2f15bfda4 | 100753| Craft CMS - Remote Code Execution - CVE:CVE-2024-56145| Log| Block| This is a New Detection


## WAF - Improved Payload Logging for WAF Managed Rules
**Published on:** Thu, 08 May 2025 00:00:00 GMT

We have upgraded WAF Payload Logging to enhance rule diagnostics and usability:

  * **Targeted logging** : Logs now capture only the specific portions of requests that triggered WAF rules, rather than entire request segments.
  * **Visual highlighting** : Matched content is visually highlighted in the UI for faster identification.
  * **Enhanced context** : Logs now include surrounding context to make diagnostics more effective.

![Log entry showing payload logging details](https://developers.cloudflare.com/_astro/2025-05-payload-logging-update.1M29LjNm_Z23wApX.webp)

Payload Logging is available to all Enterprise customers. If you have not used Payload Logging before, check how you can [get started](https://developers.cloudflare.com/waf/managed-rules/payload-logging/).

**Note:** The structure of the `encrypted_matched_data` field in Logpush has changed from `Map<Field, Value>` to `Map<Field, {Before: bytes, Content: Value, After: bytes}>`. If you rely on this field in your Logpush jobs, you should review and update your processing logic accordingly.


## WAF - WAF Release - 2025-05-05
**Published on:** Mon, 05 May 2025 00:00:00 GMT

This week's analysis covers five CVEs with varying impact levels. Four are rated critical, while one is rated high severity. Remote Code Execution vulnerabilities dominate this set.

**Key Findings**

GFI KerioControl (CVE-2024-52875) contains an unauthenticated Remote Code Execution (RCE) vulnerability that targets firewall appliances. This vulnerability can let attackers gain root level system access, making this CVE particularly attractive for threat actors.

The SonicWall SMA vulnerabilities remain concerning due to their continued exploitation since 2021. These critical vulnerabilities in remote access solutions create dangerous entry points to networks.

**Impact**

Customers using the Managed Ruleset will receive rule coverage following this week's release. Below is a breakdown of the recommended prioritization based on current exploitation trends:

  * GFI KerioControl (CVE-2024-52875) - Highest priority; unauthenticated RCE
  * SonicWall SMA (Multiple vulnerabilities) - Critical for network appliances
  * XWiki (CVE-2025-24893) - High priority for development environments
  * Langflow (CVE-2025-3248) - Important for AI workflow platforms
  * MinIO (CVE-2025-31489) - Important for object storage implementations

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 921660147baa48eaa9151077d0b7a392 | 100724| GFI KerioControl - Remote Code Execution - CVE:CVE-2024-52875| Log| Block| This is a New Detection
CIS Managed Ruleset| a3900934273b4a488111f810717a9e42 | 100748| XWiki - Remote Code Execution - CVE:CVE-2025-24893| Log| Block| This is a New Detection
CIS Managed Ruleset| 616ad0e03892473191ca1df4e9cf745d | 100750| SonicWall SMA - Dangerous File Upload - CVE:CVE-2021-20040, CVE:CVE-2021-20041, CVE:CVE-2021-20042| Log| Block| This is a New Detection
CIS Managed Ruleset| 1a11fbe84b49451193ee1ee6d29da333 | 100751| Langflow - Remote Code Execution - CVE:CVE-2025-3248| Log| Block| This is a New Detection
CIS Managed Ruleset| 5eb7ed601e6844828b9bdb05caa7b208 | 100752| MinIO - Auth Bypass - CVE:CVE-2025-31489| Log| Block| This is a New Detection


## WAF - WAF Release - 2025-04-26 - Emergency
**Published on:** Sat, 26 Apr 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 54ea354d7f2d43c69b238d1419fcc883 | 100755| React.js - Router and Remix Vulnerability - CVE:CVE-2025-43864, CVE:CVE-2025-43865| Block| Block| This is a New Detection


## WAF - WAF Release - 2025-04-22
**Published on:** Tue, 22 Apr 2025 00:00:00 GMT

Each of this week's rule releases covers a distinct CVE, with half of the rules targeting Remote Code Execution (RCE) attacks. Of the 6 CVEs covered, four were scored as critical, with the other two scored as high.

When deciding which exploits to tackle, CIS tunes into the attackers' areas of focus. CIS's network intelligence provides a unique lens into attacker activity – for instance, through the volume of blocked requests related with CVE exploits after updating WAF Managed Rules with new detections.

From this week's releases, one indicator that RCE is a "hot topic" attack type is the fact that the Oracle PeopleSoft RCE rule accounts for half of all of the new rule matches. This rule patches CVE-2023-22047, a high-severity vulnerability in the Oracle PeopleSoft suite that allows unauthenticated attackers to access PeopleSoft Enterprise PeopleTools data through remote code execution. This is particularly concerning because of the nature of the data managed by PeopleSoft – this can include payroll records or student profile information. This CVE, along with five others, are addressed with the latest detection update to WAF Managed Rules.

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| faa032d9825e4844a1188f3ba5be3327 | 100738| GitLab - Auth Bypass - CVE:CVE-2023-7028| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 2e96b6d5cdd94f7782b90e266c9531fa | 100740| Splunk Enterprise - Remote Code Execution - CVE:CVE-2025-20229| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 5c9c095bc1e5411195edb893f40bbc2b | 100741| Oracle PeopleSoft - Remote Code Execution - CVE:CVE-2023-22047| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 1d7a3932296c42fd827055335462167c | 100742| CrushFTP - Auth Bypass - CVE:CVE-2025-31161| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 5eb7ed601e6844828b9bdb05caa7b208 | 100743| Ivanti - Buffer Error - CVE:CVE-2025-22457| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 410317f1e32b41859fa3214dd52139a8 | 100744| Oracle Access Manager - Remote Code Execution - CVE:CVE-2021-35587| Log| Disabled| This is a New Detection


## WAF - WAF Release - 2025-04-14
**Published on:** Mon, 14 Apr 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 9209bb65527f4c088bca5ffad6b2d36c | 100739A| Next.js - Auth Bypass - CVE:CVE-2025-29927 - 2| Log| Disabled| This is a New Detection


## WAF - WAF Release - 2025-04-02
**Published on:** Wed, 02 Apr 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 8b8074e73b7d4aba92fc68f3622f0483 | 100732| Sitecore - Code Injection - CVE:CVE-2025-27218| Log| Block| This is a New Detection
CIS Managed Ruleset| 8350947451a1401c934f5e660f101cca | 100733| Angular-Base64-Upload - Remote Code Execution - CVE:CVE-2024-42640| Log| Block| This is a New Detection
CIS Managed Ruleset| a9ec9cf625ff42769298671d1bbcd247 | 100734| Apache Camel - Remote Code Execution - CVE:CVE-2025-29891| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 3d6bf99039b54312a1a2165590aea1ca | 100735| Progress Software WhatsUp Gold - Remote Code Execution - CVE:CVE-2024-4885| Log| Block| This is a New Detection
CIS Managed Ruleset| d104e3246dc14ac7851b4049d9d8c5f2 | 100737| Apache Tomcat - Remote Code Execution - CVE:CVE-2025-24813| Log| Block| This is a New Detection
CIS Managed Ruleset| 21c7a963e1b749e7b1753238a28a42c4 | 100659| Common Payloads for Server-side Template Injection| N/A| Disabled| N/A
CIS Managed Ruleset| 887843ffbe90436dadd1543adaa4b037 | 100659| Common Payloads for Server-side Template Injection - Base64| N/A| Disabled| N/A
CIS Managed Ruleset| 3565b80fc5b541b4832c0fc848f6a9cf | 100642| LDAP Injection| N/A| Disabled| N/A
CIS Managed Ruleset| 44d7bf9bf0fa4898b8579573e0713e9f | 100642| LDAP Injection Base64| N/A| Disabled| N/A
CIS Managed Ruleset| e35c9a670b864a3ba0203ffb1bc977d1 | 100005| DotNetNuke - File Inclusion - CVE:CVE-2018-9126, CVE:CVE-2011-1892, CVE:CVE-2022-31474| N/A| Disabled| N/A
CIS Managed Ruleset| cd8db44032694fdf8d6e22c1bb70a463 | 100527| Apache Struts - CVE:CVE-2021-31805| N/A| Block| N/A
CIS Managed Ruleset| 0d838d9ab046443fa3f8b3e50c99546a | 100702| Command Injection - CVE:CVE-2022-24108| N/A| Block| N/A
CIS Managed Ruleset| 533fbad558ce4c5ebcf013f09a5581d0 | 100622C| Ivanti - Command Injection - CVE:CVE-2023-46805, CVE:CVE-2024-21887, CVE:CVE-2024-22024| N/A| Block| N/A
CIS Managed Ruleset| 04176552f62f4b75bf65981206d0b009 | 100536C| GraphQL Command Injection| N/A| Disabled| N/A
CIS Managed Ruleset| 25883bf28575433c952b830c1651d0c8 | 100536| GraphQL Injection| N/A| Disabled| N/A
CIS Managed Ruleset| 7b70da1bb8d243bd80cd7a73af00f61d | 100536A| GraphQL Introspection| N/A| Disabled| N/A
CIS Managed Ruleset| 58c4853c250946359472b7eaa41e5b67 | 100536B| GraphQL SSRF| N/A| Disabled| N/A
CIS Managed Ruleset| 1c241ed5f5bd44b19e17476b433e5b3d | 100559A| Prototype Pollution - Common Payloads| N/A| Disabled| N/A
CIS Managed Ruleset| af748489e1c2411d80d855954816b26f | 100559A| Prototype Pollution - Common Payloads - Base64| N/A| Disabled| N/A
CIS Managed Ruleset| ccc47ab7e34248c09546c284fcea5ed2 | 100734| Apache Camel - Remote Code Execution - CVE:CVE-2025-29891| N/A| Disabled| N/A


## WAF - WAF Release - 2025-03-22 - Emergency
**Published on:** Sat, 22 Mar 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 34583778093748cc83ff7b38f472013e | 100739| Next.js - Auth Bypass - CVE:CVE-2025-29927| N/A| Disabled| This is a New Detection


## Workers, Pages, WAF - New Managed WAF rule for Next.js CVE-2025-29927.
**Published on:** Sat, 22 Mar 2025 00:00:00 GMT

**Update: Mon Mar 24th, 11PM UTC** : Next.js has made further changes to address a smaller vulnerability introduced in the patches made to its middleware handling. Users should upgrade to Next.js versions `15.2.4`, `14.2.26`, `13.5.10` or `12.3.6`. **If you are unable to immediately upgrade or are running an older version of Next.js, you can enable the WAF rule described in this changelog as a mitigation**.

**Update: Mon Mar 24th, 8PM UTC** : Next.js has now [backported the patch for this vulnerability](https://github.com/advisories/GHSA-f82v-jwr5-mffw) to cover Next.js v12 and v13. Users on those versions will need to patch to `13.5.9` and `12.3.5` (respectively) to mitigate the vulnerability.

**Update: Sat Mar 22nd, 4PM UTC** : We have changed this WAF rule to opt-in only, as sites that use auth middleware with third-party auth vendors were observing failing requests.

**We strongly recommend updating your version of Next.js (if eligible)** to the patched versions, as your app will otherwise be vulnerable to an authentication bypass attack regardless of auth provider.

#### Enable the Managed Rule (strongly recommended)

This rule is opt-in only for sites on the Pro plan or above in the [WAF managed ruleset](https://developers.cloudflare.com/waf/managed-rules/).

To enable the rule:

  1. Head to Security > WAF > Managed rules in the CIS dashboard for the zone (website) you want to protect.
  2. Click the three dots next to **CIS Managed Ruleset** and choose **Edit**
  3. Scroll down and choose **Browse Rules**
  4. Search for **CVE-2025-29927** (ruleId: `34583778093748cc83ff7b38f472013e`)
  5. Change the **Status** to **Enabled** and the **Action** to **Block**. You can optionally set the rule to Log, to validate potential impact before enabling it. Log will not block requests.
  6. Click **Next**
  7. Scroll down and choose **Save**



This will enable the WAF rule and block requests with the `x-middleware-subrequest` header regardless of Next.js version.

#### Create a WAF rule (manual)

For users on the Free plan, or who want to define a more specific rule, you can create a [Custom WAF rule](https://developers.cloudflare.com/waf/custom-rules/create-dashboard/) to block requests with the `x-middleware-subrequest` header regardless of Next.js version.

To create a custom rule:

  1. Head to Security > WAF > Custom rules in the CIS dashboard for the zone (website) you want to protect.
  2. Give the rule a name - e.g. `next-js-CVE-2025-29927`
  3. Set the matching parameters for the rule match any request where the `x-middleware-subrequest` header `exists` per the rule expression below.




    (len(http.request.headers["x-middleware-subrequest"]) > 0)

  1. Set the action to 'block'. If you want to observe the impact before blocking requests, set the action to 'log' (and edit the rule later).
  2. **Deploy** the rule.

![Next.js CVE-2025-29927 WAF rule](https://developers.cloudflare.com/_astro/waf-rule-cve-2025-29927.0i0XiweZ_Z8mlyw.webp)

#### Next.js CVE-2025-29927

We've made a WAF (Web Application Firewall) rule available to all sites on CIS to protect against the [Next.js authentication bypass vulnerability](https://github.com/advisories/GHSA-f82v-jwr5-mffw) (`CVE-2025-29927`) published on March 21st, 2025.

**Note** : This rule is not enabled by default as it blocked requests across sites for specific authentication middleware.

  * This managed rule protects sites using Next.js on Workers and Pages, as well as sites using CIS to protect Next.js applications hosted elsewhere.
  * This rule has been made available (but not enabled by default) to all sites as part of our [WAF Managed Ruleset](https://developers.cloudflare.com/waf/managed-rules/reference/cloudflare-managed-ruleset/) and blocks requests that attempt to bypass authentication in Next.js applications.
  * The vulnerability affects almost all Next.js versions, and has been fully patched in Next.js `14.2.26` and `15.2.4`. Earlier, interim releases did not fully patch this vulnerability.
  * **Users on older versions of Next.js (`11.1.4` to `13.5.6`) did not originally have a patch available**, but this the patch for this vulnerability and a subsequent additional patch have been backported to Next.js versions `12.3.6` and `13.5.10` as of Monday, March 24th. Users on Next.js v11 will need to deploy the stated workaround or enable the WAF rule.



The managed WAF rule mitigates this by blocking _external_ user requests with the `x-middleware-subrequest` header regardless of Next.js version, but we recommend users using Next.js 14 and 15 upgrade to the patched versions of Next.js as an additional mitigation.


## WAF - WAF Release - 2025-03-19 - Emergency
**Published on:** Wed, 19 Mar 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 470b477e27244fddb479c4c7a2cafae7 | 100736| Generic HTTP Request Smuggling| N/A| Disabled| This is a New Detection


## WAF - WAF Release - 2025-03-17
**Published on:** Mon, 17 Mar 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 28b2a12993a04e62a98abcd9e59ec18a | 100725| Fortinet FortiManager - Remote Code Execution - CVE:CVE-2023-42791, CVE:CVE-2024-23666| Log| Block|
CIS Managed Ruleset| f253d755910e4998bd90365d1dbf58df | 100726| Ivanti - Remote Code Execution - CVE:CVE-2024-8190| Log| Block|
CIS Managed Ruleset| 19ae0094a8d845a1bb1997af0ad61fa7 | 100727| Cisco IOS XE - Remote Code Execution - CVE:CVE-2023-20198| Log| Disabled| Fixed action value in changelog; no rule changes.
CIS Managed Ruleset| 83a677f082264693ad64a2827ee56b66 | 100728| Sitecore - Remote Code Execution - CVE:CVE-2024-46938| Log| Block|
CIS Managed Ruleset| 166b7ce85ce443538f021228a6752a38 | 100729| Microsoft SharePoint - Remote Code Execution - CVE:CVE-2023-33160| Log| Block|
CIS Managed Ruleset| 35fe23e7bd324d00816c82d098d47b69 | 100730| Pentaho - Template Injection - CVE:CVE-2022-43769, CVE:CVE-2022-43939| Log| Block|
CIS Managed Ruleset| 2ce80fe815254f25b3c8f47569fe1e0d | 100700| Apache SSRF vulnerability CVE-2021-40438| N/A| Block|


## WAF - WAF Release - 2025-03-11 - Emergency
**Published on:** Tue, 11 Mar 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 0823d16dd8b94cc6b27a9ab173febb31 | 100731| Apache Camel - Code Injection - CVE:CVE-2025-27636| N/A| Block| This is a New Detection


## WAF - WAF Release - 2025-03-10
**Published on:** Mon, 10 Mar 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| d4f68c1c65c448e58fe4830eb2a51e3d | 100722| Ivanti - Information Disclosure - CVE:CVE-2025-0282| Log| Block| This is a New Detection
CIS Managed Ruleset| fda130e396224ffc9f0a9e72259073d5 | 100723| Cisco IOS XE - Information Disclosure - CVE:CVE-2023-20198| Log| Block| This is a New Detection


## WAF - Updated leaked credentials database
**Published on:** Fri, 07 Mar 2025 00:00:00 GMT

Added new records to the leaked credentials database. The record sources are: Have I Been Pwned (HIBP) database, RockYou 2024 dataset, and another third-party database.


## WAF - WAF Release - 2025-03-03
**Published on:** Mon, 03 Mar 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 90356ececae3444b9accb3d393e63099 | 100721| Ivanti - Remote Code Execution - CVE:CVE-2024-13159, CVE:CVE-2024-13160, CVE:CVE-2024-13161| Log| Block| This is a New Detection
CIS Managed Ruleset| 6cf09ce2fa73482abb7f677ecac42ce2 | 100596| Citrix Content Collaboration ShareFile - Remote Code Execution - CVE:CVE-2023-24489| N/A| Block|


## WAF - WAF Release - 2025-02-24
**Published on:** Mon, 24 Feb 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| f7b9d265b86f448989fb0f054916911e | 100718A| SonicWall SSLVPN 2 - Auth Bypass - CVE:CVE-2024-53704| Log| Block| This is a New Detection
CIS Managed Ruleset| 77c13c611d2a4fa3a89c0fafc382fdec | 100720| Palo Alto Networks - Auth Bypass - CVE:CVE-2025-0108| Log| Block| This is a New Detection


## WAF - WAF Release - 2025-02-18
**Published on:** Tue, 18 Feb 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| d1d45e4f59014f0fb22e0e6aa2ffa4b8 | 100715| FortiOS - Auth Bypass - CVE:CVE-2024-55591| Log| Block| This is a New Detection
CIS Managed Ruleset| 14b5cdeb4cde490ba37d83555a883e12 | 100716| Ivanti - Auth Bypass - CVE:CVE-2021-44529| Log| Block| This is a New Detection
CIS Managed Ruleset| 498fcd81a62a4b5ca943e2de958094d3 | 100717| SimpleHelp - Auth Bypass - CVE:CVE-2024-57727| Log| Block| This is a New Detection
CIS Managed Ruleset| 6e0d8afc36ba4ce9836f81e63b66df22 | 100718| SonicWall SSLVPN - Auth Bypass - CVE:CVE-2024-53704| Log| Block| This is a New Detection
CIS Managed Ruleset| 8eb4536dba1a4da58fbf81c79184699f | 100719| Yeti Platform - Auth Bypass - CVE:CVE-2024-46507| Log| Block| This is a New Detection


## WAF - WAF Release - 2025-02-11
**Published on:** Tue, 11 Feb 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 742306889c2e4f6087de6646483b4c26 | 100708| Aviatrix Network - Remote Code Execution - CVE:CVE-2024-50603| Log| Block| This is a New Detection
CIS Managed Ruleset| 042228dffe0a4f1587da0e737e924ca3 | 100709| Next.js - Remote Code Execution - CVE:CVE-2024-46982| Log| Disabled| This is a New Detection
CIS Managed Ruleset| 2a12278325464d6682afb53483a7d8ff | 100710| Progress Software WhatsUp Gold - Directory Traversal - CVE:CVE-2024-12105| Log| Block| This is a New Detection
CIS Managed Ruleset| 82ce3424fbe84e9e99d77332baa8eb34 | 100711| WordPress - Remote Code Execution - CVE:CVE-2024-56064| Log| Block| This is a New Detection
CIS Managed Ruleset| 5afacd39dcfd42f89a6c43f787f5d34e | 100712| WordPress - Remote Code Execution - CVE:CVE-2024-9047| Log| Block| This is a New Detection
CIS Managed Ruleset| 05842b06f0a4415880b58f7fbf72cf8a | 100713| FortiOS - Auth Bypass - CVE:CVE-2022-40684| Log| Block| This is a New Detection


## WAF - Updated leaked credentials database
**Published on:** Tue, 04 Feb 2025 00:00:00 GMT

Added new records to the leaked credentials database from a third-party database.


## WAF - WAF Release - 2025-01-21
**Published on:** Tue, 21 Jan 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| f4a310393c564d50bd585601b090ba9a | 100303| Command Injection - Nslookup| Log| Block| This was released as aad6f9f85e034022b6a8dee4b8d152f4
CIS Managed Ruleset| fd5d5678ce594ea898aa9bf149e6b538 | 100534| Web Shell Activity| Log| Block| This was released as 39c8f6066c19466ea084e51e82fe4e7f


## WAF - WAF Release - 2025-01-13
**Published on:** Mon, 13 Jan 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Managed Ruleset| 6e0bfbe4b9c6454c8bd7bd24f49e5840 | 100704| Cleo Harmony - Auth Bypass - CVE:CVE-2024-55956, CVE:CVE-2024-55953| Log| Block| New Detection
CIS Managed Ruleset| c993997b7d904a9e89448fe6a6d43bc2 | 100705| Sentry - SSRF| Log| Block| New Detection
CIS Managed Ruleset| f40ce742be534ba19d610961ce6311bb | 100706| Apache Struts - Remote Code Execution - CVE:CVE-2024-53677| Log| Block| New Detection
CIS Managed Ruleset| 67ac639a845c482d948b465b2233da1f | 100707| FortiWLM - Remote Code Execution - CVE:CVE-2023-48782, CVE:CVE-2023-34993, CVE:CVE-2023-34990| Log| Block| New Detection
CIS Managed Ruleset| 870cca2b874d41738019d4c3e31d972a | 100007C_BETA| Command Injection - Common Attack Commands| | Disabled|


## WAF - WAF Release - 2025-01-06
**Published on:** Mon, 06 Jan 2025 00:00:00 GMT

Ruleset| Rule ID| Legacy Rule ID| Description| Previous Action| New Action| Comments
---|---|---|---|---|---|---
CIS Specials| 3a321b10270b42549ac201009da08beb | 100678| Pandora FMS - Remote Code Execution - CVE:CVE-2024-11320| Log| Block| New Detection
CIS Specials| 1fe510368b4a47dda90363c2ecdf3d02 | 100679| Palo Alto Networks - Remote Code Execution - CVE:CVE-2024-0012, CVE:CVE-2024-9474| Log| Block| New Detection
CIS Specials| b7ba636927b44ee288b9a697a40f2a35 | 100680| Ivanti - Command Injection - CVE:CVE-2024-37397| Log| Block| New Detection
CIS Specials| 6bd9b07c8acc4beeb17c8bee58ae3c89 | 100681| Really Simple Security - Auth Bypass - CVE:CVE-2024-10924| Log| Block| New Detection
CIS Specials| c86e79e15a4a4307870f6f77e37f2da6 | 100682| Magento - XXE - CVE:CVE-2024-34102| Log| Block| New Detection
CIS Specials| 945f41b48be9485f953116015054c752 | 100683| CyberPanel - Remote Code Execution - CVE:CVE-2024-51567| Log| Block| New Detection
CIS Specials| aec9a2e554a34a8fa547d069dfe93d7b | 100684| Microsoft SharePoint - Remote Code Execution - CVE:CVE-2024-38094, CVE:CVE-2024-38024, CVE:CVE-2024-38023| Log| Block| New Detection
CIS Specials| e614dd46c1ce404da1909e841454c856 | 100685| CyberPanel - Remote Code Execution - CVE:CVE-2024-51568| Log| Block| New Detection
CIS Specials| 685a4edf68f740b4a2c80d45e92362e5 | 100686| Seeyon - Remote Code Execution| Log| Block| New Detection
CIS Specials| 204f9d948a124829acb86555b9f1c9f8 | 100687| WordPress - Remote Code Execution - CVE:CVE-2024-10781, CVE:CVE-2024-10542| Log| Block| New Detection
CIS Specials| 19587024724e49329d5b482d0d7ca374 | 100688| ProjectSend - Remote Code Execution - CVE:CVE-2024-11680| Log| Block| New Detection
CIS Specials| fa49213e55484f6c824e0682a5260b70 | 100689| Palo Alto GlobalProtect - Remote Code Execution - CVE:CVE-2024-5921| Log| Block| New Detection
CIS Specials| 11b5fc23e85b41ca90316bddd007118b | 100690| Ivanti - Remote Code Execution - CVE:CVE-2024-37404| Log| Block| New Detection
CIS Specials| aaeada52bcc840598515de6cc3e49f64 | 100691| Array Networks - Remote Code Execution - CVE:CVE-2023-28461| Log| Block| New Detection
CIS Specials| e2c7ce1ecd6847219f8d9aedfcc6f5bb | 100692| CyberPanel - Remote Code Execution - CVE:CVE-2024-51378| Log| Block| New Detection
CIS Specials| 84d481b1f49c4735afa2fb2bb615335e | 100693| Symfony Profiler - Auth Bypass - CVE:CVE-2024-50340| Log| Block| New Detection
CIS Specials| 9f258f463f9f4b26ad07e3c209d08c8a | 100694| Citrix Virtual Apps - Remote Code Execution - CVE:CVE-2024-8069| Log| Block| New Detection
CIS Specials| b490d6edcfec4028aef45cf08aafb2f5 | 100695| MSMQ Service - Remote Code Execution - CVE:CVE-2023-21554| Log| Block| New Detection
CIS Specials| c8f65bc9eeef4665820ecfe411b7a8c7 | 100696| Nginxui - Remote Code Execution - CVE:CVE-2024-49368| Log| Block| New Detection
CIS Specials| d5f2e133e34640198d06d7b345954c7e | 100697| Apache ShardingSphere - Remote Code Execution - CVE:CVE-2022-22733| Log| Block| New Detection
CIS Specials| c34432e257074cffa9fa15f3f5311209 | 100698| Mitel MiCollab - Auth Bypass - CVE:CVE-2024-41713| Log| Block| New Detection
CIS Specials| 3bda15acd73a4b55a5f60cd2b3e5e46e | 100699| Apache Solr - Auth Bypass - CVE:CVE-2024-45216| Log| Block| New Detection
