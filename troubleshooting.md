---
copyright:
  years: 2018
lastupdated: "2018-03-02"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Troubleshooting your CIS network connection

## How do I know if my data is passing through my IBM Cloud CIS connection?

IBM Cloud CIS uses HTTP headers, which it can read, add, or modify. The header lets us trace how a request was routed, using a CF-Ray number. The CF-Ray number can be found by a `curl` command or with a Google Chrome plug in called "Claire".

To know whether data has passed through IBM Cloud CIS, you need to locate the “Ray ID” which will be present on every packet.

**Unix command line tools:**

 * curl for HTTP:
`$ curl -vso /dev/null http://example.com`

 * dig for DNS:
`$ dig www.example.com`

 * traceroute for network:
`$ traceroute example.com`

**For example:**

Terminal command:  `curl -svo /dev/null YOUR_URL_HERE. -L`

Results in: `CF-RAY: 1ca349b6c1300da3-SJC`

## How do I trace a route?

To see whether a route goes through your IBM Cloud CIS pathway, you can perform a ‘dig’ in a Terminal window for Mac or Linux
or use `nslookup` in the Windows command prompt for Windows.

If the packet has a CF-Ray value, then it has travelled through CIS.

The `traceroute` command shows the entire path that an IP request has taken.

The support team makes use of these commands to assist you.

## If you see a privacy warning:

The certificates issued by IBM Cloud CIS cover the root domain (`example.com`) and one level of subdomain (`*.example.com`). If you’re trying to reach a second-level subdomain (`*.*.example.com`) you will see a privacy warning in your browser, because these host names are not added to the SAN.

Also, please allow up to 15 minutes for one of our partner Certificates Authorities (CAs) to issue a new certificate. You’ll see a privacy warning in your browser if your new certificate has not yet been issued.

## What do I do if I’m under a DDoS attack?

 * **Step 1:** Turn on "Defense Mode" from your dashboard
 * **Step 2:** Set your DNS records for maximum security
 * **Step 3:** Do not rate-limit or throttle requests from IBM CIS
 * **Step 4:** Block specific IP ranges, countries, and visitors as needed

During "Defense Mode", each new visitor is met with a "Captcha" security challenge, which they must pass before being given a cookie for unchallenged access. That way, botnet traffic is blocked until the "Defense Mode" is turned off. Visitors that do not meet the security challenge are added to the (bad) IP Reputation database.

## Other problems you might encounter:

Here are some common error messages that you or your support team might see:

| Error Code    | Reason |
| ------------- | ------------- |
| 1001  | DNS Resolution Error. Either the customer recently signed up and their DNS information has not yet propagated, or whomever is managing the DNS has a failure. |
| 521  | Origin web server refused connection from CIS. Either the origin web server is not running, or something is blocking IBM CIS IP addresses. |
| 522  | Connection timeout to the origin server (30 second default). Either CIS may be rate-limited, the web server may be consuming all resources (shared server), or there may be network connectivity issues between the web server and IBM CIS. |
| 523  | Origin server is unreachable. Ensure that the origin IP address for the DNS record is the same as the one appearing in the CIS DNS Settings page. |
| 524  | IBM CIS could make a TCP connection but did not receive a response from the web server. A long-running application or database query is interfering. |

### Not seeing any network traffic

If you’re not seeing traffic, and you’re using a CNAME, make sure that there is a redirect in place, so the traffic is not being routed to the root domain. Remember that some DNS propagations can take up to 48 hours to complete.

### Website offline

Here is what you might see:

`IBM CIS cannot connect to the origin server (error 521, 522, 523)`.

**Website offline - no cached version**

1. The server is online, but it is blocking the CIS request.
2. The origin server is offline and CIS does not have a backup website image (Always Online is turned off).

What you can do:

* Verify that the CIS IP addresses are whitelisted..
* Make sure that IBM CIS IPs are not being rate-limited.
* Here is the list of [IPs to whitelist](whitelisted-ips.html)

### 502 error “The dreaded 502”

This error is one of the most common ones you may see. It typically occurs when a portion of a network is unavailable, for example, at the start of a DDoS attack. A particular data center may be unavailable for a time. Traffic will be re-routed. Run a trace route or check the IBM CIS status page. 

Here is what you might see: `Error 502 - bad gateway error`

What happened:

* A portion of the IBM CIS network is having an issue.
* Usually the problem is limited to one server in one data center.
* It affects only a portion of the site's visitors.
* The IBM CIS Technical Operations team deals with these.

What you can do:

* Send the results from `www.YOUR_DOMAIN.com/cdn-cgi/trace` in a ticket to [Support](https://console.bluemix.net/docs/support/index.html#contacting-support).
* Temporarily toggle your DNS Records to off (No proxy).

