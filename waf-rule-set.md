---
copyright:
  years: 2018
lastupdated: "2018-03-06"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# WAF default rule set

| Rule | Action |
|----------|---------------|
|Numbers Botnet|challenge
|CtrlFunc Botnet|challenge
|Generic LFI against common paths in ARGS|block
|Generic Local File Inclusion rule with enhancements|simulate
|Generic LFI against common paths in URI|block
|Generic LFI against common paths in URI without post processing|block
|Generic RCE against common commands|block
|Generic RCE against shell commands|block
|Generic RCE against common network commands|simulate
|Prevent RCE against the nc family of commands|block
|SQLi probing|block
|Block SQLi string function evasion|block
|Block SQLi string concatination evasions|block
|Block SQLi sleep probing|block
|Block SQLi sleep probing (wait for)|block
|SQLi attempt (Conditional) |block
|SQLi attempt (Where)|block
|SQLi attempt (IS NULL)|block
|SQLi attempt (Equation) [ ]|block
|SQLi attempt (Math Comparison) []|block
|SQLi attempt (Math Comparison) Beta []|simulate
|SQLi attempt (End comparison) PATH []|block
|SQLi attempt (End comparison) URI []|block
|SQLi attempt (End comparison) ARGS []|block
|SQLi attempt (Sub query Evasion) []|block
|SQLi attempt (Wildcard Evasion) []|block
|SQLi attempt (Early Func) []|block
|SQLi attempt (Embedded Func) []|simulate
|SQLi attempt (MultiLevel Func) []|block
|SQLi attempt (Union Vector) []|simulate
|SQLi probe|block
|Disallow SQLi comments  |block
|Disallow strings ending in SQLi comments |simulate
|SQLi attempt (Wildcard Escape)|block
|Block invalid X-Forwarded-Host headers - |challenge
|Block requests to version control systems|block
|Block Wow! Signal Comment Bot|block
|CVE-2014-6271 - ShellShock|block
|CVE-2014-6271 - ShellShock|block
|Common DDoS flood|challenge
|Common XSS probing|challenge
|XSS probing with alert keyword|challenge
|XSS probing with script tags|block
|XSS probing with javascript events|block
|XSS probing with javascript events (Strict)|challenge
|XSS probing with javascript URI|challenge
|XSS hidden in base64 data URIs |challenge
|XSS atob() detection evasion|block
|XSS eval() detection evasion|block
|XSS lenient eval() detection evasion|simulate
|Block semalt crawler|block
|Drop Spaced-Out DDoS bot|block
|Stop null cookie headers|block
|Disallow PHP code tags in headers|block
|Block incorrectly formatted Mozilla User Agents|block
|Generic XSS Probing|challenge
|SVG XSS Attempt|challenge
|Prevent IIS DoS - CVE-2015-1635 []|block
|Prevent fake googlebots from crawling|block
|Prevent fake bingbots from crawling|block
|Prevent fake BaiduBots from crawling|block
|Prevent fake yandexbot from crawling|block
|Block fake baidu user agents used in DoS attacks|block
|Block attempts to obtain information that may disclose information about the origin server|block
|Prevent access to extensions that may be used by text editors when saving/backup |block
|Block attempts to access the apache status page /server-status|simulate
|Drop probes from the Acunetix scanner|challenge
|Drop Java probes from the Acunetix scanner|challenge
|CVE-2015-7857 Joomla SQL Injection|block
|Log when two host headers are sent with a request|simulate
|False IE6 detection [Type B]|challenge
|False IE6 detection [Type C]|challenge
|Block spoofed/corrupted Google Chrome user agents|block
|Block nginx alias header injection attempts|challenge
|Block known login bruteforces|challenge
|Block attempted exploits against Imgmagik CVE-2016-3714 |block
|Block attempted exploits against GraphicsMagick CVE-2016-5118 |block
|PHPMailer RCE - CVE-2016-10033 Type A|block
|PHPMailer RCE - CVE-2016-10033 Type B|block
|Block CVE-2017-5638 exploitation attempts (Content-Type)|block
|Prevent IIS RCE CVE-2017-7269 attempts |block
|Struts / OGNL SSI inclusion attempt (CVE-2017-9791 etc.)|block
|Block 'drop table ...' SQL injection attempts []|simulate
|Block HTTP requests with user-agent matching 26 alphabets only|block
|Dropping requests with X-Requested-With having an APK ID from the Endurance attack|simulate
|Dropping CVE-2017-9805 matching requests|block
|SQLi comment probe|simulate
|SQLi attempt []|simulate
|SQLi attempt []|block
|SQLi cross-parameter comments []|simulate
|XSS probing with javascript events|simulate
|Executable RFI protection|simulate
|Redirected RFI protection|simulate
|SQLi for UNION SELECT ALL NULL|simulate
|CVE-2017-7525 - Struts / Jackson RCE|block
|Bad UA :: Brute Force Attempt|challenge
|Fake UA :: Used in Wordpress bruteforce|challenge
|Fake UA :: Used in Wordpress bruteforce|challenge
|Fake UA :: Used in Wordpress bruteforce|challenge
|Fake UA :: Used in Wordpress bruteforce|challenge
|Fake UA :: Used in Wordpress bruteforce|challenge
|Fake UA :: Used in Wordpress bruteforce|challenge
|Blocking WordPress mfunc vulnerability|block
|Blocking CDorked.A favicon|block
|Rule to Mitigate Atlassian Confluence Security Advisory 2015-01-21|challenge
|Exploit DB 28129 Practico CMS Login SQLi|block
|WebHive LOIC|challenge
|UITSEC attack script|block
|CVE-2013-2251 - Apache Struts RCE|simulate
|Drop requests trying to exploit CloudBees Jenkins RCE (CVE-2017-1000353)|simulate
|Mitigation for Apache Tomcat CVE-2016-6816|block
|Block Large Requests to xmlrpc.php for Drupal CMS|block
|Block requests with odd array arguments|block
|Block Rosetta Flash|challenge
|Block Rosetta Flash|challenge
|Joomla JCE Exploit|block
|Dropping User-Agent/X-Forwarded-For RCE attempt against Joomla. CVE-2015-8562|block
|Block unauthorized user registration in Joomla CVE-2016-8870|block
|Block unauthorized user registration in Joomla CVE-2016-8869|block
|Block group based privilege elevation CVE-2016-9838|block
|Block com_fields SQLI in Joomla|block
|Block com_fields SQLI in Joomla|block
|Blocks the Magento exploit labeled as SUPEE-5344|block
|Disallow Magento setup files to be reached APPSEC-1421|block
|Disallow RCE though the Magento API APPSEC-1420 (Type A)|block
|Disallow RCE though the Magento API APPSEC-1420 (Type B)|block
|Apache / PHP 5.x Remote Code Execution Exploit|challenge
|Disallow php:// URIs to avoid RCE and LFI|block
|Disallow obfuscated PHP to avoid RCE|block
|Forbidden Plone request|block
|WHMCS 5.2.7 Vulnerability|block
|WHMCS 5.2.8 Vulnerability|block
|WHMCS 5.2.10 Vulnerability|block
|WordPress Pingback Blocker|challenge
|Disable WAF for wp-admin|on
|Disable WAF for WordPress post.php|on
|Exploit DB 28485 Blind SQL Injection|block
|Wordpress Jetpack Protection|block
|Disallow timthumb from pulling php files|block
|Block dynamic scripts being in cache directories|block
|Disallow timthumb from pulling external sources|simulate
|Yoast WordPress - Blind SQLi|block
|Block abnormally long hostnames in pingbacks|block
|Block abnormally long comments|block
|Block TwentyFifteen DOM XSS Attack|block
|Prevent CVE-2015-2213 SQL Injection in comment system|block
|Fix RCE in EWWW Image Optimizer for WordPress|block
|Disable WAF for Verified VaultPress backup requests|on
|Prevent Mailport RCE via file upload|block
|Prevent RCE via upload in Revolution Slider|block
|Prevent files in update unpackers from being run|block
|Prevent RCE via upload in Gravity Forms|block
|Prevent abuse against wp-json api Type A|block
|Prevent abuse against wp-json api Type B|block
|Prevent abuse against wp-json api Type C|simulate
|wp-config.php LFI protection|block
|Drop XML in enclosure post meta field|block
|CVE-2018-6389: dropping requests that try JS script DoS Amplification attacks|simulate
