---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-15"

keywords: Web Application Firewall Ruleset, rule sets  

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Serie di regole predefinite WAF
{:#waf-default-ruleset}

| Regola | Azione |
|----------|---------------|
|Numbers Botnet|verifica
|CtrlFunc Botnet|verifica
|Generic LFI against common paths in ARGS|blocca
|Generic Local File Inclusion rule with enhancements|simula
|Generic LFI against common paths in URI|blocca
|Generic LFI against common paths in URI without post processing|blocca
|Generic RCE against common commands|blocca
|Generic RCE against shell commands|blocca
|Generic RCE against common network commands|simula
|Prevent RCE against the nc family of commands|blocca
|SQLi probing|blocca
|Block SQLi string function evasion|blocca
|Block SQLi string concatination evasions|blocca
|Block SQLi sleep probing|blocca
|Block SQLi sleep probing (wait for)|blocca
|SQLi attempt (Conditional) |blocca
|SQLi attempt (Where)|blocca
|SQLi attempt (IS NULL)|blocca
|SQLi attempt (Equation) [ ]|blocca
|SQLi attempt (Math Comparison) []|blocca
|SQLi attempt (Math Comparison) Beta []|simula
|SQLi attempt (End comparison) PATH []|blocca
|SQLi attempt (End comparison) URI []|blocca
|SQLi attempt (End comparison) ARGS []|blocca
|SQLi attempt (Sub query Evasion) []|blocca
|SQLi attempt (Wildcard Evasion) []|blocca
|SQLi attempt (Early Func) []|blocca
|SQLi attempt (Embedded Func) []|simula
|SQLi attempt (MultiLevel Func) []|blocca
|SQLi attempt (Union Vector) []|simula
|SQLi probe|blocca
|Disallow SQLi comments  |blocca
|Disallow strings ending in SQLi comments |simula
|SQLi attempt (Wildcard Escape)|blocca
|Block invalid X-Forwarded-Host headers - |verifica
|Block requests to version control systems|blocca
|Block Wow! Signal Comment Bot|blocca
|CVE-2014-6271 - ShellShock|blocca
|CVE-2014-6271 - ShellShock|blocca
|Common DDoS flood|verifica
|Common XSS probing|verifica
|XSS probing with alert keyword|verifica
|XSS probing with script tags|blocca
|XSS probing with javascript events|blocca
|XSS probing with javascript events (Strict)|verifica
|XSS probing with javascript URI|verifica
|XSS hidden in base64 data URIs |verifica
|XSS atob() detection evasion|blocca
|XSS eval() detection evasion|blocca
|XSS lenient eval() detection evasion|simula
|Block semalt crawler|blocca
|Drop Spaced-Out DDoS bot|blocca
|Stop null cookie headers|blocca
|Disallow PHP code tags in headers|blocca
|Block incorrectly formatted Mozilla User Agents|blocca
|Generic XSS Probing|verifica
|SVG XSS Attempt|verifica
|Prevent IIS DoS - CVE-2015-1635 []|blocca
|Prevent fake googlebots from crawling|blocca
|Prevent fake bingbots from crawling|blocca
|Prevent fake BaiduBots from crawling|blocca
|Prevent fake yandexbot from crawling|blocca
|Block fake baidu user agents used in DoS attacks|blocca
|Block attempts to obtain information that may disclose information about the origin server|blocca
|Prevent access to extensions that may be used by text editors when saving/backup |blocca
|Block attempts to access the apache status page /server-status|simula
|Drop probes from the Acunetix scanner|verifica
|Drop Java probes from the Acunetix scanner|verifica
|CVE-2015-7857 Joomla SQL Injection|blocca
|Log when two host headers are sent with a request|simula
|False IE6 detection [Type B]|verifica
|False IE6 detection [Type C]|verifica
|Block spoofed/corrupted Google Chrome user agents|blocca
|Block nginx alias header injection attempts|verifica
|Block known login bruteforces|verifica
|Block attempted exploits against Imgmagik CVE-2016-3714 |blocca
|Block attempted exploits against GraphicsMagick CVE-2016-5118 |blocca
|PHPMailer RCE - CVE-2016-10033 Type A|blocca
|PHPMailer RCE - CVE-2016-10033 Type B|blocca
|Block CVE-2017-5638 exploitation attempts (Content-Type)|blocca
|Prevent IIS RCE CVE-2017-7269 attempts |blocca
|Struts / OGNL SSI inclusion attempt (CVE-2017-9791 etc.)|blocca
|Block 'drop table ...' SQL injection attempts []|simula
|Block HTTP requests with user-agent matching 26 alphabets only|blocca
|Dropping requests with X-Requested-With having an APK ID from the Endurance attack|simula
|Dropping CVE-2017-9805 matching requests|blocca
|SQLi comment probe|simula
|SQLi attempt []|simula
|SQLi attempt []|blocca
|SQLi cross-parameter comments []|simula
|XSS probing with javascript events|simula
|Executable RFI protection|simula
|Redirected RFI protection|simula
|SQLi for UNION SELECT ALL NULL|simula
|CVE-2017-7525 - Struts / Jackson RCE|blocca
|Bad UA :: Brute Force Attempt|verifica
|Fake UA :: Used in Wordpress bruteforce|verifica
|Fake UA :: Used in Wordpress bruteforce|verifica
|Fake UA :: Used in Wordpress bruteforce|verifica
|Fake UA :: Used in Wordpress bruteforce|verifica
|Fake UA :: Used in Wordpress bruteforce|verifica
|Fake UA :: Used in Wordpress bruteforce|verifica
|Blocking WordPress mfunc vulnerability|blocca
|Blocking CDorked.A favicon|blocca
|Rule to Mitigate Atlassian Confluence Security Advisory 2015-01-21|verifica
|Exploit DB 28129 Practico CMS Login SQLi|blocca
|WebHive LOIC|verifica
|UITSEC attack script|blocca
|CVE-2013-2251 - Apache Struts RCE|simula
|Drop requests trying to exploit CloudBees Jenkins RCE (CVE-2017-1000353)|simula
|Mitigation for Apache Tomcat CVE-2016-6816|blocca
|Block Large Requests to xmlrpc.php for Drupal CMS|blocca
|Block requests with odd array arguments|blocca
|Block Rosetta Flash|verifica
|Block Rosetta Flash|verifica
|Joomla JCE Exploit|blocca
|Dropping User-Agent/X-Forwarded-For RCE attempt against Joomla. CVE-2015-8562|blocca
|Block unauthorized user registration in Joomla CVE-2016-8870|blocca
|Block unauthorized user registration in Joomla CVE-2016-8869|blocca
|Block group based privilege elevation CVE-2016-9838|blocca
|Block com_fields SQLI in Joomla|blocca
|Block com_fields SQLI in Joomla|blocca
|Blocks the Magento exploit labeled as SUPEE-5344|blocca
|Disallow Magento setup files to be reached APPSEC-1421|blocca
|Disallow RCE though the Magento API APPSEC-1420 (Type A)|blocca
|Disallow RCE though the Magento API APPSEC-1420 (Type B)|blocca
|Apache / PHP 5.x Remote Code Execution Exploit|verifica
|Disallow php:// URIs to avoid RCE and LFI|blocca
|Disallow obfuscated PHP to avoid RCE|blocca
|Forbidden Plone request|blocca
|WHMCS 5.2.7 Vulnerability|blocca
|WHMCS 5.2.8 Vulnerability|blocca
|WHMCS 5.2.10 Vulnerability|blocca
|WordPress Pingback Blocker|verifica
|Disable WAF for wp-admin|attiva
|Disable WAF for WordPress post.php|attiva
|Exploit DB 28485 Blind SQL Injection|blocca
|Wordpress Jetpack Protection|blocca
|Disallow timthumb from pulling php files|blocca
|Block dynamic scripts being in cache directories|blocca
|Disallow timthumb from pulling external sources|simula
|Yoast WordPress - Blind SQLi|blocca
|Block abnormally long hostnames in pingbacks|blocca
|Block abnormally long comments|blocca
|Block TwentyFifteen DOM XSS Attack|blocca
|Prevent CVE-2015-2213 SQL Injection in comment system|blocca
|Fix RCE in EWWW Image Optimizer for WordPress|blocca
|Disable WAF for Verified VaultPress backup requests|attiva
|Prevent Mailport RCE via file upload|blocca
|Prevent RCE via upload in Revolution Slider|blocca
|Prevent files in update unpackers from being run|blocca
|Prevent RCE via upload in Gravity Forms|blocca
|Prevent abuse against wp-json api Type A|blocca
|Prevent abuse against wp-json api Type B|blocca
|Prevent abuse against wp-json api Type C|simula
|wp-config.php LFI protection|blocca
|Drop XML in enclosure post meta field|blocca
|CVE-2018-6389: dropping requests that try JS script DoS Amplification attacks|simula
