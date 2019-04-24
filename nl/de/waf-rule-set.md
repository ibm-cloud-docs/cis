---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-15"

keywords: Web Application Firewall Ruleset, rule sets  

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# WAF-Standardregelsatz
{:#waf-default-ruleset}

| Regel | Aktion |
|----------|---------------|
|Numbers Botnet|Sicherheitsabfrage ausgeben
|CtrlFunc Botnet|Sicherheitsabfrage ausgeben
|Generic LFI against common paths in ARGS|Blockieren
|Generic Local File Inclusion rule with enhancements|Simulieren
|Generic LFI against common paths in URI|Blockieren
|Generic LFI against common paths in URI without post processing|Blockieren
|Generic RCE against common commands|Blockieren
|Generic RCE against shell commands|Blockieren
|Generic RCE against common network commands|Simulieren
|Prevent RCE against the nc family of commands|Blockieren
|SQLi probing|Blockieren
|Block SQLi string function evasion|Blockieren
|Block SQLi string concatination evasions|Blockieren
|Block SQLi sleep probing|Blockieren
|Block SQLi sleep probing (wait for)|Blockieren
|SQLi attempt (Conditional) |Blockieren
|SQLi attempt (Where)|Blockieren
|SQLi attempt (IS NULL)|Blockieren
|SQLi attempt (Equation) [ ]|Blockieren
|SQLi attempt (Math Comparison) []|Blockieren
|SQLi attempt (Math Comparison) Beta []|Simulieren
|SQLi attempt (End comparison) PATH []|Blockieren
|SQLi attempt (End comparison) URI []|Blockieren
|SQLi attempt (End comparison) ARGS []|Blockieren
|SQLi attempt (Sub query Evasion) []|Blockieren
|SQLi attempt (Wildcard Evasion) []|Blockieren
|SQLi attempt (Early Func) []|Blockieren
|SQLi attempt (Embedded Func) []|Simulieren
|SQLi attempt (MultiLevel Func) []|Blockieren
|SQLi attempt (Union Vector) []|Simulieren
|SQLi probe|Blockieren
|Disallow SQLi comments  |Blockieren
|Disallow strings ending in SQLi comments |Simulieren
|SQLi attempt (Wildcard Escape)|Blockieren
|Block invalid X-Forwarded-Host headers - |Sicherheitsabfrage ausgeben
|Block requests to version control systems|Blockieren
|Block Wow! Signal Comment Bot|Blockieren
|CVE-2014-6271 - ShellShock|Blockieren
|CVE-2014-6271 - ShellShock|Blockieren
|Common DDoS flood|Sicherheitsabfrage ausgeben
|Common XSS probing|Sicherheitsabfrage ausgeben
|XSS probing with alert keyword|Sicherheitsabfrage ausgeben
|XSS probing with script tags|Blockieren
|XSS probing with javascript events|Blockieren
|XSS probing with javascript events (Strict)|Sicherheitsabfrage ausgeben
|XSS probing with javascript URI|Sicherheitsabfrage ausgeben
|XSS hidden in base64 data URIs |Sicherheitsabfrage ausgeben
|XSS atob() detection evasion|Blockieren
|XSS eval() detection evasion|Blockieren
|XSS lenient eval() detection evasion|Simulieren
|Block semalt crawler|Blockieren
|Drop Spaced-Out DDoS bot|Blockieren
|Stop null cookie headers|Blockieren
|Disallow PHP code tags in headers|Blockieren
|Block incorrectly formatted Mozilla User Agents|Blockieren
|Generic XSS Probing|Sicherheitsabfrage ausgeben
|SVG XSS Attempt|Sicherheitsabfrage ausgeben
|Prevent IIS DoS - CVE-2015-1635 []|Blockieren
|Prevent fake googlebots from crawling|Blockieren
|Prevent fake bingbots from crawling|Blockieren
|Prevent fake BaiduBots from crawling|Blockieren
|Prevent fake yandexbot from crawling|Blockieren
|Block fake baidu user agents used in DoS attacks|Blockieren
|Block attempts to obtain information that may disclose information about the origin server|Blockieren
|Prevent access to extensions that may be used by text editors when saving/backup |Blockieren
|Block attempts to access the apache status page /server-status|Simulieren
|Drop probes from the Acunetix scanner|Sicherheitsabfrage ausgeben
|Drop Java probes from the Acunetix scanner|Sicherheitsabfrage ausgeben
|CVE-2015-7857 Joomla SQL Injection|Blockieren
|Log when two host headers are sent with a request|Simulieren
|False IE6 detection [Type B]|Sicherheitsabfrage ausgeben
|False IE6 detection [Type C]|Sicherheitsabfrage ausgeben
|Block spoofed/corrupted Google Chrome user agents|Blockieren
|Block nginx alias header injection attempts|Sicherheitsabfrage ausgeben
|Block known login bruteforces|Sicherheitsabfrage ausgeben
|Block attempted exploits against Imgmagik CVE-2016-3714 |Blockieren
|Block attempted exploits against GraphicsMagick CVE-2016-5118 |Blockieren
|PHPMailer RCE - CVE-2016-10033 Type A|Blockieren
|PHPMailer RCE - CVE-2016-10033 Type B|Blockieren
|Block CVE-2017-5638 exploitation attempts (Content-Type)|Blockieren
|Prevent IIS RCE CVE-2017-7269 attempts |Blockieren
|Struts / OGNL SSI inclusion attempt (CVE-2017-9791 etc.)|Blockieren
|Block 'drop table ...' SQL injection attempts []|Simulieren
|Block HTTP requests with user-agent matching 26 alphabets only|Blockieren
|Dropping requests with X-Requested-With having an APK ID from the Endurance attack|Simulieren
|Dropping CVE-2017-9805 matching requests|Blockieren
|SQLi comment probe|Simulieren
|SQLi attempt []|Simulieren
|SQLi attempt []|Blockieren
|SQLi cross-parameter comments []|Simulieren
|XSS probing with javascript events|Simulieren
|Executable RFI protection|Simulieren
|Redirected RFI protection|Simulieren
|SQLi for UNION SELECT ALL NULL|Simulieren
|CVE-2017-7525 - Struts / Jackson RCE|Blockieren
|Bad UA :: Brute Force Attempt|Sicherheitsabfrage ausgeben
|Fake UA :: Used in Wordpress bruteforce|Sicherheitsabfrage ausgeben
|Fake UA :: Used in Wordpress bruteforce|Sicherheitsabfrage ausgeben
|Fake UA :: Used in Wordpress bruteforce|Sicherheitsabfrage ausgeben
|Fake UA :: Used in Wordpress bruteforce|Sicherheitsabfrage ausgeben
|Fake UA :: Used in Wordpress bruteforce|Sicherheitsabfrage ausgeben
|Fake UA :: Used in Wordpress bruteforce|Sicherheitsabfrage ausgeben
|Blocking WordPress mfunc vulnerability|Blockieren
|Blocking CDorked.A favicon|Blockieren
|Rule to Mitigate Atlassian Confluence Security Advisory 2015-01-21|Sicherheitsabfrage ausgeben
|Exploit DB 28129 Practico CMS Login SQLi|Blockieren
|WebHive LOIC|Sicherheitsabfrage ausgeben
|UITSEC attack script|Blockieren
|CVE-2013-2251 - Apache Struts RCE|Simulieren
|Drop requests trying to exploit CloudBees Jenkins RCE (CVE-2017-1000353)|Simulieren
|Mitigation for Apache Tomcat CVE-2016-6816|Blockieren
|Block Large Requests to xmlrpc.php for Drupal CMS|Blockieren
|Block requests with odd array arguments|Blockieren
|Block Rosetta Flash|Sicherheitsabfrage ausgeben
|Block Rosetta Flash|Sicherheitsabfrage ausgeben
|Joomla JCE Exploit|Blockieren
|Dropping User-Agent/X-Forwarded-For RCE attempt against Joomla. CVE-2015-8562|Blockieren
|Block unauthorized user registration in Joomla CVE-2016-8870|Blockieren
|Block unauthorized user registration in Joomla CVE-2016-8869|Blockieren
|Block group based privilege elevation CVE-2016-9838|Blockieren
|Block com_fields SQLI in Joomla|Blockieren
|Block com_fields SQLI in Joomla|Blockieren
|Blocks the Magento exploit labeled as SUPEE-5344|Blockieren
|Disallow Magento setup files to be reached APPSEC-1421|Blockieren
|Disallow RCE though the Magento API APPSEC-1420 (Type A)|Blockieren
|Disallow RCE though the Magento API APPSEC-1420 (Type B)|Blockieren
|Apache / PHP 5.x Remote Code Execution Exploit|Sicherheitsabfrage ausgeben
|Disallow php:// URIs to avoid RCE and LFI|Blockieren
|Disallow obfuscated PHP to avoid RCE|Blockieren
|Forbidden Plone request|Blockieren
|WHMCS 5.2.7 Vulnerability|Blockieren
|WHMCS 5.2.8 Vulnerability|Blockieren
|WHMCS 5.2.10 Vulnerability|Blockieren
|WordPress Pingback Blocker|Sicherheitsabfrage ausgeben
|Disable WAF for wp-admin|Ein
|Disable WAF for WordPress post.php|Ein
|Exploit DB 28485 Blind SQL Injection|Blockieren
|Wordpress Jetpack Protection|Blockieren
|Disallow timthumb from pulling php files|Blockieren
|Block dynamic scripts being in cache directories|Blockieren
|Disallow timthumb from pulling external sources|Simulieren
|Yoast WordPress - Blind SQLi|Blockieren
|Block abnormally long hostnames in pingbacks|Blockieren
|Block abnormally long comments|Blockieren
|Block TwentyFifteen DOM XSS Attack|Blockieren
|Prevent CVE-2015-2213 SQL Injection in comment system|Blockieren
|Fix RCE in EWWW Image Optimizer for WordPress|Blockieren
|Disable WAF for Verified VaultPress backup requests|Ein
|Prevent Mailport RCE via file upload|Blockieren
|Prevent RCE via upload in Revolution Slider|Blockieren
|Prevent files in update unpackers from being run|Blockieren
|Prevent RCE via upload in Gravity Forms|Blockieren
|Prevent abuse against wp-json api Type A|Blockieren
|Prevent abuse against wp-json api Type B|Blockieren
|Prevent abuse against wp-json api Type C|Simulieren
|wp-config.php LFI protection|Blockieren
|Drop XML in enclosure post meta field|Blockieren
|CVE-2018-6389: dropping requests that try JS script DoS Amplification attacks|Simulieren
