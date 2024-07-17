---

copyright:
  years: 2023, 2024
lastupdated: "2024-07-17"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# About bot management
{: #about-bot-mgmt}

Bot management blocks undesired or malicious internet bot traffic while allowing useful bots to access web properties. Bot management detects bot activity, discerns between desirable and undesirable bot behavior, and identifies the sources of the undesirable activity.
{: shortdesc}

Unmanaged bots can cause serious issues for web properties. Excessive bot traffic can put a heavy load on web servers, slowing or denying service to legitimate users (for example, DDoS attacks). Malicious bots can perform cyber attacks such as scraping content from websites, stealing user credentials, and spreading spam content.

## What bot managers do
{: #what-bot-managers-do}

A bot manager is any software product that manages bots. Bot managers should be able to block some bots and allow others through, instead of simply blocking all non-human traffic. If all bots are blocked and Google bots aren't able to index a page, for instance, then that page can't show up in Google search results, resulting in greatly reduced organic traffic to the website.

An effective bot manager accomplishes the following goals:

* Distinguishes bots from human visitors
* Identifies bot reputation
* Identifies bot origin IP addresses and block based on IP reputation
* Analyzes bot behavior
* Adds "good" bots to allowlists
* Challenges potential bots with a CAPTCHA test, JavaScript injection, or other methods
* Rate limits any potential bot that is over-using a service
* Denies access to certain content or resources for "bad" bots
* Serves alternative content to bots

## What are bots and what do they do?
{: #what-is-a-bot}

A bot is a computer program that automatically does certain actions on a network. The tasks a bot is programmed to do are fairly simple, but the bot can do these tasks repeatedly at a much faster rate than a human can.

Bots don't access the internet using a traditional web browser or a mouse to interact with visual content. Bots are software programs that typically use a "headless browser" to make HTTP requests and other activities.

Bots can do almost any repetitive, non-creative task that can be automated, including filling out forms, reading and downloading content, and even hold basic conversations with humans as chatbots. Like any tool that can be used for good, bots can be used for malicious behavior, too.

## Differences between good bots and bad bots
{: #good-bot-bad-bot}

It is estimated that up to half of all internet traffic is bot traffic. Some bots are malicious, and some are "good."

Bots that misuse online products or services can be considered "bad." Bad bots range from malicious to simply annoying; for instance, breaking into user accounts to steal data or buying concert tickets online to assist scalpers.

A bot that performs a helpful service can be considered "good." For example, customer service chatbots, search engine crawlers, and performance monitoring bots are generally good bots. Good bots look for and abide by the rules outlined in a website's `robots.txt` file.

## The `robots.txt` file
{: #robots-txt-file}

`Robots.txt` is a file that outlines the rules for bots accessing properties on a web server, though the file itself does not enforce these rules. Anyone programming a bot is expected to follow an honor system and make sure that their bot checks a website's `robots.txt` file before accessing the website. Malicious bots don't follow this system, which generates the need for bot management.

## How bot management works
{: #how-bot-management-works}

To identify bots, bot managers might use JavaScript challenges (which determine whether a traditional web browser is being used) or CAPTCHA challenges. They can also determine which users are humans and which are bots by behavioral analysis; by comparing a user's behavior to the standard behavior of users in the past.

When a bot is identified as bad, it can be redirected to a different page or blocked from accessing a web resource altogether.

Good bots can be added to an allowlist. A bot manager can also distinguish between good and bad bots by using further behavioral analysis.

Another bot management approach is to use the `robots.txt` file to set up a honeypot. A honeypot is a fake target for bad actors that, when accessed, exposes the bad actor as malicious. In the case of a bot, a honeypot could be a webpage on the site that's forbidden to bots by the `robots.txt` file. Good bots will read the `robots.txt` file and avoid that webpage; some bad bots will crawl the webpage. By tracking the IP address of the bots that access the honeypot, bad bots can be identified and blocked.

## Kinds of bot attacks bot management mitigates
{: #kinds-of-bot-attacks-mitigated}

A bot management solution can help stop a variety of attacks, including the following:

* DDoS attacks
* DoS attacks
* Credential stuffing
* Credit card stuffing
* Brute force password cracking
* Spam content
* Data scraping and web scraping
* Email address harvesting
* Ad fraud
* Click fraud

These bot activities are not always considered "malicious," but a bot manager should still be able to mitigate them:

* Inventory hoarding
* Automated posting on social forums or platforms
* Shopping cart stuffing

## How does {{site.data.keyword.cis_short_notm}} manage bots?
{: #how-does-cis-manage-bots}

{{site.data.keyword.cis_short_notm}} collects data from requests flowing through its network every day. With this data, powered by Cloudflare's machine learning and behavior analysis, {{site.data.keyword.cis_short_notm}} can identify likely bot activity and can provide you with information on how to allow or disallow specific bot traffic using Firewall Rules.

Cloudflare Bot Management uses the following detection mechanisms, each producing their own scores, which are then combined to form a single score:

* Machine learning: A highly accurate bot identification machine learning model trained on trillions of requests with minimal impact to request processing speed
* Heuristics engine: Detects bots by screening requests through a set of simple rules that capture bots based on certain attibutes of the requests made.
* Behavioral analysis: Detects bots that have never been seen, calculating and analyzing normal visitor behavior over an extended period of time.
* Verified bots: A way to avoid accidental blocks of useful bots using several validators and a bots directory of unique good bot identities.
* JS fingerprinting: A challenge-response system with challenge injected into the webpage on Cloudflare’s edge and rendered in the background for validation.
