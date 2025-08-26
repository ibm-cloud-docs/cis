---

copyright:
  years: 2024, 2025
lastupdated: "2025-08-26"

keywords: managed rules

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Bot management fields
{: #bot-management-fields}

Bot Management provides access to several new variables within the expression builder of Ruleset Engine-based features, such as [WAF custom rules](/docs/cis?topic=cis-custom-rules-overview).
 

## Ruleset Engine fields
{: #ruleset-engine-fields}

Bot Management provides access to several new variables within the expression builder of Ruleset Engine-based products, such as WAF custom rules.

* **Bot Score** (`cf.bot_management.score`): An integer between 1-99 that indicates that a request comes from a bot.
* **Verified Bot** (`cf.bot_management.verified_bot`): A boolean value that is true if the request comes from a good bot, like Google or Bing. Most customers choose to allow this traffic. 
* **Serves Static Resource** (`cf.bot_management.static_resource`): An identifier that matches file extensions for many types of static resources. Use this variable if you send emails that retrieve static images.
* **ja3Hash** (`cf.bot_management.ja3_hash`) and **ja4** (`cf.bot_management.ja4`): A JA3/JA4 fingerprint helps you profile specific SSL/TLS clients across different destination IPs, Ports, and X509 certificates.
* **Bot Detection IDs** (`cf.bot_management.detection_ids`): List of IDs that correlate to the Bot Management heuristic detections made on a request (you can have multiple heuristic detections on the same request).
* **Verified Bot Categories** (`cf.verified_bot_category`): A string that allows you to segment your verified bot traffic by its type and purpose.
 
## Log fields
{: #log-fields}

After you enable Bot Management, CIS also surfaces bot information in its [HTTP requests log fields](/docs/cis?topic=cis-log-fields#logpull-available-fields): 

* BotDetectionIDs
* BotScore
* BotScoreSrc
* BotTags
