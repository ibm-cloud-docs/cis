---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-15"

keywords: Web Application Firewall Ruleset, rule sets  

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# WAF デフォルト・ルール・セット
{:#waf-default-ruleset}

| ルール | アクション |
|----------|---------------|
|Numbers Botnet|要求
|CtrlFunc Botnet|要求
|Generic LFI against common paths in ARGS|ブロック
|Generic Local File Inclusion rule with enhancements|シミュレート
|Generic LFI against common paths in URI|ブロック
|Generic LFI against common paths in URI without post processing|ブロック
|Generic RCE against common commands|ブロック
|Generic RCE against shell commands|ブロック
|Generic RCE against common network commands|シミュレート
|Prevent RCE against the nc family of commands|ブロック
|SQLi probing|ブロック
|Block SQLi string function evasion|ブロック
|Block SQLi string concatination evasions|ブロック
|Block SQLi sleep probing|ブロック
|Block SQLi sleep probing (wait for)|ブロック
|SQLi attempt (Conditional) |ブロック
|SQLi attempt (Where)|ブロック
|SQLi attempt (IS NULL)|ブロック
|SQLi attempt (Equation) [ ]|ブロック
|SQLi attempt (Math Comparison) []|ブロック
|SQLi attempt (Math Comparison) Beta []|シミュレート
|SQLi attempt (End comparison) PATH []|ブロック
|SQLi attempt (End comparison) URI []|ブロック
|SQLi attempt (End comparison) ARGS []|ブロック
|SQLi attempt (Sub query Evasion) []|ブロック
|SQLi attempt (Wildcard Evasion) []|ブロック
|SQLi attempt (Early Func) []|ブロック
|SQLi attempt (Embedded Func) []|シミュレート
|SQLi attempt (MultiLevel Func) []|ブロック
|SQLi attempt (Union Vector) []|シミュレート
|SQLi probe|ブロック
|Disallow SQLi comments  |ブロック
|Disallow strings ending in SQLi comments |シミュレート
|SQLi attempt (Wildcard Escape)|ブロック
|Block invalid X-Forwarded-Host headers - |要求
|Block requests to version control systems|ブロック
|Block Wow! Signal Comment Bot|ブロック
|CVE-2014-6271 - ShellShock|ブロック
|CVE-2014-6271 - ShellShock|ブロック
|Common DDoS flood|要求
|Common XSS probing|要求
|XSS probing with alert keyword|要求
|XSS probing with script tags|ブロック
|XSS probing with javascript events|ブロック
|XSS probing with javascript events (Strict)|要求
|XSS probing with javascript URI|要求
|XSS hidden in base64 data URIs |要求
|XSS atob() detection evasion|ブロック
|XSS eval() detection evasion|ブロック
|XSS lenient eval() detection evasion|シミュレート
|Block semalt crawler|ブロック
|Drop Spaced-Out DDoS bot|ブロック
|Stop null cookie headers|ブロック
|Disallow PHP code tags in headers|ブロック
|Block incorrectly formatted Mozilla User Agents|ブロック
|Generic XSS Probing|要求
|SVG XSS Attempt|要求
|Prevent IIS DoS - CVE-2015-1635 []|ブロック
|Prevent fake googlebots from crawling|ブロック
|Prevent fake bingbots from crawling|ブロック
|Prevent fake BaiduBots from crawling|ブロック
|Prevent fake yandexbot from crawling|ブロック
|Block fake baidu user agents used in DoS attacks|ブロック
|Block attempts to obtain information that may disclose information about the origin server|ブロック
|Prevent access to extensions that may be used by text editors when saving/backup |ブロック
|Block attempts to access the apache status page /server-status|シミュレート
|Drop probes from the Acunetix scanner|要求
|Drop Java probes from the Acunetix scanner|要求
|CVE-2015-7857 Joomla SQL Injection|ブロック
|Log when two host headers are sent with a request|シミュレート
|False IE6 detection [Type B]|要求
|False IE6 detection [Type C]|要求
|Block spoofed/corrupted Google Chrome user agents|ブロック
|Block nginx alias header injection attempts|要求
|Block known login bruteforces|要求
|Block attempted exploits against Imgmagik CVE-2016-3714 |ブロック
|Block attempted exploits against GraphicsMagick CVE-2016-5118 |ブロック
|PHPMailer RCE - CVE-2016-10033 Type A|ブロック
|PHPMailer RCE - CVE-2016-10033 Type B|ブロック
|Block CVE-2017-5638 exploitation attempts (Content-Type)|ブロック
|Prevent IIS RCE CVE-2017-7269 attempts |ブロック
|Struts / OGNL SSI inclusion attempt (CVE-2017-9791 etc.)|ブロック
|Block 'drop table ...' SQL injection attempts []|シミュレート
|Block HTTP requests with user-agent matching 26 alphabets only|ブロック
|Dropping requests with X-Requested-With having an APK ID from the Endurance attack|シミュレート
|Dropping CVE-2017-9805 matching requests|ブロック
|SQLi comment probe|シミュレート
|SQLi attempt []|シミュレート
|SQLi attempt []|ブロック
|SQLi cross-parameter comments []|シミュレート
|XSS probing with javascript events|シミュレート
|Executable RFI protection|シミュレート
|Redirected RFI protection|シミュレート
|SQLi for UNION SELECT ALL NULL|シミュレート
|CVE-2017-7525 - Struts / Jackson RCE|ブロック
|Bad UA :: Brute Force Attempt|要求
|Fake UA :: Used in Wordpress bruteforce|要求
|Fake UA :: Used in Wordpress bruteforce|要求
|Fake UA :: Used in Wordpress bruteforce|要求
|Fake UA :: Used in Wordpress bruteforce|要求
|Fake UA :: Used in Wordpress bruteforce|要求
|Fake UA :: Used in Wordpress bruteforce|要求
|Blocking WordPress mfunc vulnerability|ブロック
|Blocking CDorked.A favicon|ブロック
|Rule to Mitigate Atlassian Confluence Security Advisory 2015-01-21|要求
|Exploit DB 28129 Practico CMS Login SQLi|ブロック
|WebHive LOIC|要求
|UITSEC attack script|ブロック
|CVE-2013-2251 - Apache Struts RCE|シミュレート
|Drop requests trying to exploit CloudBees Jenkins RCE (CVE-2017-1000353)|シミュレート
|Mitigation for Apache Tomcat CVE-2016-6816|ブロック
|Block Large Requests to xmlrpc.php for Drupal CMS|ブロック
|Block requests with odd array arguments|ブロック
|Block Rosetta Flash|要求
|Block Rosetta Flash|要求
|Joomla JCE Exploit|ブロック
|Dropping User-Agent/X-Forwarded-For RCE attempt against Joomla. CVE-2015-8562|ブロック
|Block unauthorized user registration in Joomla CVE-2016-8870|ブロック
|Block unauthorized user registration in Joomla CVE-2016-8869|ブロック
|Block group based privilege elevation CVE-2016-9838|ブロック
|Block com_fields SQLI in Joomla|ブロック
|Block com_fields SQLI in Joomla|ブロック
|Blocks the Magento exploit labeled as SUPEE-5344|ブロック
|Disallow Magento setup files to be reached APPSEC-1421|ブロック
|Disallow RCE though the Magento API APPSEC-1420 (Type A)|ブロック
|Disallow RCE though the Magento API APPSEC-1420 (Type B)|ブロック
|Apache / PHP 5.x Remote Code Execution Exploit|要求
|Disallow php:// URIs to avoid RCE and LFI|ブロック
|Disallow obfuscated PHP to avoid RCE|ブロック
|Forbidden Plone request|ブロック
|WHMCS 5.2.7 Vulnerability|ブロック
|WHMCS 5.2.8 Vulnerability|ブロック
|WHMCS 5.2.10 Vulnerability|ブロック
|WordPress Pingback Blocker|要求
|Disable WAF for wp-admin|オン
|Disable WAF for WordPress post.php|オン
|Exploit DB 28485 Blind SQL Injection|ブロック
|Wordpress Jetpack Protection|ブロック
|Disallow timthumb from pulling php files|ブロック
|Block dynamic scripts being in cache directories|ブロック
|Disallow timthumb from pulling external sources|シミュレート
|Yoast WordPress - Blind SQLi|ブロック
|Block abnormally long hostnames in pingbacks|ブロック
|Block abnormally long comments|ブロック
|Block TwentyFifteen DOM XSS Attack|ブロック
|Prevent CVE-2015-2213 SQL Injection in comment system|ブロック
|Fix RCE in EWWW Image Optimizer for WordPress|ブロック
|Disable WAF for Verified VaultPress backup requests|オン
|Prevent Mailport RCE via file upload|ブロック
|Prevent RCE via upload in Revolution Slider|ブロック
|Prevent files in update unpackers from being run|ブロック
|Prevent RCE via upload in Gravity Forms|ブロック
|Prevent abuse against wp-json api Type A|ブロック
|Prevent abuse against wp-json api Type B|ブロック
|Prevent abuse against wp-json api Type C|シミュレート
|wp-config.php LFI protection|ブロック
|Drop XML in enclosure post meta field|ブロック
|CVE-2018-6389: dropping requests that try JS script DoS Amplification attacks|シミュレート
