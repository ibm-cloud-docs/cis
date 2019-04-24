---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-15"

keywords: Web Application Firewall Ruleset, rule sets  

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# WAF 기본 규칙 세트
{:#waf-default-ruleset}

|규칙 |조치 |
|----------|---------------|
|Numbers Botnet|인증 확인
|CtrlFunc Botnet|인증 확인
|Generic LFI against common paths in ARGS|차단
|Generic Local File Inclusion rule with enhancements|시뮬레이션
|Generic LFI against common paths in URI|차단
|Generic LFI against common paths in URI without post processing|차단
|Generic RCE against common commands|차단
|Generic RCE against shell commands|차단
|Generic RCE against common network commands|시뮬레이션
|Prevent RCE against the nc family of commands|차단
|SQLi probing|차단
|Block SQLi string function evasion|차단
|Block SQLi string concatination evasions|차단
|Block SQLi sleep probing|차단
|Block SQLi sleep probing (wait for)|차단
|SQLi attempt (Conditional) |차단
|SQLi attempt (Where)|차단
|SQLi attempt (IS NULL)|차단
|SQLi attempt (Equation) [ ]|차단
|SQLi attempt (Math Comparison) []|차단
|SQLi attempt (Math Comparison) Beta []|시뮬레이션
|SQLi attempt (End comparison) PATH []|차단
|SQLi attempt (End comparison) URI []|차단
|SQLi attempt (End comparison) ARGS []|차단
|SQLi attempt (Sub query Evasion) []|차단
|SQLi attempt (Wildcard Evasion) []|차단
|SQLi attempt (Early Func) []|차단
|SQLi attempt (Embedded Func) []|시뮬레이션
|SQLi attempt (MultiLevel Func) []|차단
|SQLi attempt (Union Vector) []|시뮬레이션
|SQLi probe|차단
|Disallow SQLi comments  |차단
|Disallow strings ending in SQLi comments |시뮬레이션
|SQLi attempt (Wildcard Escape)|차단
|Block invalid X-Forwarded-Host headers - |인증 확인
|Block requests to version control systems|차단
|Block Wow! Signal Comment Bot|차단
|CVE-2014-6271 - ShellShock|차단
|CVE-2014-6271 - ShellShock|차단
|Common DDoS flood|인증 확인
|Common XSS probing|인증 확인
|XSS probing with alert keyword|인증 확인
|XSS probing with script tags|차단
|XSS probing with javascript events|차단
|XSS probing with javascript events (Strict)|인증 확인
|XSS probing with javascript URI|인증 확인
|XSS hidden in base64 data URIs |인증 확인
|XSS atob() detection evasion|차단
|XSS eval() detection evasion|차단
|XSS lenient eval() detection evasion|시뮬레이션
|Block semalt crawler|차단
|Drop Spaced-Out DDoS bot|차단
|Stop null cookie headers|차단
|Disallow PHP code tags in headers|차단
|Block incorrectly formatted Mozilla User Agents|차단
|Generic XSS Probing|인증 확인
|SVG XSS Attempt|인증 확인
|Prevent IIS DoS - CVE-2015-1635 []|차단
|Prevent fake googlebots from crawling|차단
|Prevent fake bingbots from crawling|차단
|Prevent fake BaiduBots from crawling|차단
|Prevent fake yandexbot from crawling|차단
|Block fake baidu user agents used in DoS attacks|차단
|Block attempts to obtain information that may disclose information about the origin server|차단
|Prevent access to extensions that may be used by text editors when saving/backup |차단
|Block attempts to access the apache status page /server-status|시뮬레이션
|Drop probes from the Acunetix scanner|인증 확인
|Drop Java probes from the Acunetix scanner|인증 확인
|CVE-2015-7857 Joomla SQL Injection|차단
|Log when two host headers are sent with a request|시뮬레이션
|False IE6 detection [Type B]|인증 확인
|False IE6 detection [Type C]|인증 확인
|Block spoofed/corrupted Google Chrome user agents|차단
|Block nginx alias header injection attempts|인증 확인
|Block known login bruteforces|인증 확인
|Block attempted exploits against Imgmagik CVE-2016-3714 |차단
|Block attempted exploits against GraphicsMagick CVE-2016-5118 |차단
|PHPMailer RCE - CVE-2016-10033 Type A|차단
|PHPMailer RCE - CVE-2016-10033 Type B|차단
|Block CVE-2017-5638 exploitation attempts (Content-Type)|차단
|Prevent IIS RCE CVE-2017-7269 attempts |차단
|Struts / OGNL SSI inclusion attempt (CVE-2017-9791 etc.)|차단
|Block 'drop table ...' SQL injection attempts []|시뮬레이션
|Block HTTP requests with user-agent matching 26 alphabets only|차단
|Dropping requests with X-Requested-With having an APK ID from the Endurance attack|시뮬레이션
|Dropping CVE-2017-9805 matching requests|차단
|SQLi comment probe|시뮬레이션
|SQLi attempt []|시뮬레이션
|SQLi attempt []|차단
|SQLi cross-parameter comments []|시뮬레이션
|XSS probing with javascript events|시뮬레이션
|Executable RFI protection|시뮬레이션
|Redirected RFI protection|시뮬레이션
|SQLi for UNION SELECT ALL NULL|시뮬레이션
|CVE-2017-7525 - Struts / Jackson RCE|차단
|Bad UA :: Brute Force Attempt|인증 확인
|Fake UA :: Used in Wordpress bruteforce|인증 확인
|Fake UA :: Used in Wordpress bruteforce|인증 확인
|Fake UA :: Used in Wordpress bruteforce|인증 확인
|Fake UA :: Used in Wordpress bruteforce|인증 확인
|Fake UA :: Used in Wordpress bruteforce|인증 확인
|Fake UA :: Used in Wordpress bruteforce|인증 확인
|Blocking WordPress mfunc vulnerability|차단
|Blocking CDorked.A favicon|차단
|Rule to Mitigate Atlassian Confluence Security Advisory 2015-01-21|인증 확인
|Exploit DB 28129 Practico CMS Login SQLi|차단
|WebHive LOIC|인증 확인
|UITSEC attack script|차단
|CVE-2013-2251 - Apache Struts RCE|시뮬레이션
|Drop requests trying to exploit CloudBees Jenkins RCE (CVE-2017-1000353)|시뮬레이션
|Mitigation for Apache Tomcat CVE-2016-6816|차단
|Block Large Requests to xmlrpc.php for Drupal CMS|차단
|Block requests with odd array arguments|차단
|Block Rosetta Flash|인증 확인
|Block Rosetta Flash|인증 확인
|Joomla JCE Exploit|차단
|Dropping User-Agent/X-Forwarded-For RCE attempt against Joomla. CVE-2015-8562|차단
|Block unauthorized user registration in Joomla CVE-2016-8870|차단
|Block unauthorized user registration in Joomla CVE-2016-8869|차단
|Block group based privilege elevation CVE-2016-9838|차단
|Block com_fields SQLI in Joomla|차단
|Block com_fields SQLI in Joomla|차단
|Blocks the Magento exploit labeled as SUPEE-5344|차단
|Disallow Magento setup files to be reached APPSEC-1421|차단
|Disallow RCE though the Magento API APPSEC-1420 (Type A)|차단
|Disallow RCE though the Magento API APPSEC-1420 (Type B)|차단
|Apache / PHP 5.x Remote Code Execution Exploit|인증 확인
|Disallow php:// URIs to avoid RCE and LFI|차단
|Disallow obfuscated PHP to avoid RCE|차단
|Forbidden Plone request|차단
|WHMCS 5.2.7 Vulnerability|차단
|WHMCS 5.2.8 Vulnerability|차단
|WHMCS 5.2.10 Vulnerability|차단
|WordPress Pingback Blocker|인증 확인
|Disable WAF for wp-admin|켜기
|Disable WAF for WordPress post.php|켜기
|Exploit DB 28485 Blind SQL Injection|차단
|Wordpress Jetpack Protection|차단
|Disallow timthumb from pulling php files|차단
|Block dynamic scripts being in cache directories|차단
|Disallow timthumb from pulling external sources|시뮬레이션
|Yoast WordPress - Blind SQLi|차단
|Block abnormally long hostnames in pingbacks|차단
|Block abnormally long comments|차단
|Block TwentyFifteen DOM XSS Attack|차단
|Prevent CVE-2015-2213 SQL Injection in comment system|차단
|Fix RCE in EWWW Image Optimizer for WordPress|차단
|Disable WAF for Verified VaultPress backup requests|켜기
|Prevent Mailport RCE via file upload|차단
|Prevent RCE via upload in Revolution Slider|차단
|Prevent files in update unpackers from being run|차단
|Prevent RCE via upload in Gravity Forms|차단
|Prevent abuse against wp-json api Type A|차단
|Prevent abuse against wp-json api Type B|차단
|Prevent abuse against wp-json api Type C|시뮬레이션
|wp-config.php LFI protection|차단
|Drop XML in enclosure post meta field|차단
|CVE-2018-6389: dropping requests that try JS script DoS Amplification attacks|시뮬레이션