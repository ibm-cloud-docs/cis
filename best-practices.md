---
  
copyright:
   years: 2018
lastupdated: "2018-03-13"
 
---


# Best practices for CIS setup

Because IBM CIS is positioned at the edge of your network, you’ll need to take a few steps to guarantee a smooth integration with your CIS services. Here are some recommended best practices for integrating CIS with your origin servers. 

You can do these steps either before or after you change your DNS and activate our proxy service. These recommendations allow IBM CIS to connect to your origin servers properly. They’ll help you prevent any issues with API or HTTPS traffic, and help your logs capture the correct IP addresses of your customers, rather than the protective CIS IP addresses.

Here’s what you’ll need to set up:

 * Best practice 1: Restore the originating IPs of your customers
 * Best practice 2: Incorporate CIS IP addresses
 * Best practice 3: Make sure your security settings don't interfere with API traffic
 * Best practice 4: Configure your security settings as strictly as possible
 
## Best practice 1: Know how to restore the originating IPs of your customers

As a reverse proxy, we provide the origination IP in these headers:

  * `CF-Connecting-IP`
  * `X-Forwarded-For`
  * `True-Client-IP` (optional)

You can restore user IP addresses using a variety of tools, for infrastructures such as Apache, Windows IIS, and NGINX.

## Best practice 2: Incorporate CIS IP addresses to make integration smoother

Here are the two steps to take:

  * Remove any rate limiting of CIS IP addresses
  * Set up your ACLs to allow only CIS IP addresses and other trusted parties

You can find the updated list of IP ranges for IBM CIS [at this location](whitelisted-ips.html).

## Best practice 3: Review your security settings to make sure they don’t interfere with API traffic

IBM CIS usually accelerates API traffic by removing connection overhead. However, the default security stance can interfere with many API calls. We recommend that you take a few actions to prevent interference with your API traffic once proxying is active.

 * Turn security features off selectively, using the **Page Rules** features.
 
   * Select the domain you'd like to modify
   * Create a Page Rule with the URL pattern of your API, such as `api.example.com`
   * Add the following changes:
      * Find **Security** and select **Off**
      * Turn **Security Level** to **Low**
      * Reset the **Security Level** to **Low**, **Essentially Off**, or **Off**
      * Set the **Browser Integrity Check** to **Off**
      * Select **Save and Deploy**

 * Alternatively, you can turn off **Browser Integrity Check** globally.
   * Select the domain you'd like to modify
     * Select the **Firewall** application
     * Select the **Web Application Firewall** application
     * Scroll to the bottom of the page
     * Select **Off**

| *What does the Browser Integrity Check do?* | 
|------------------------------------------------|
| *The browser integrity check looks for HTTP headers that are commonly abused by spammers. It denies traffic with those headers access to your page. It also blocks visitors that do not have a user agent, or who add a non-standard user agent (this tactic is commonly used by abuse bots, crawlers. or APIs).* |

## Best practice 4: Configure your security settings as strictly as possible

CIS provides some options for encrypting your traffic. As a reverse proxy, we close SSL connections at our datacenters and open a new TLS connection to your origin servers. For your termination with CIS, you can upload a custom certificate from your account, you can use a wildcard certificate provisioned for you by CIS, or both.

### Upload a custom certificate
 
You can upload your public and private key when you create an Enterprise domain. If you upload your own certificate, you gain immediate compatibility with encrypted traffic, and you maintain control over your certificate (for example, an Extended Validation (EV) certificate). Remember that you'll be responsible for managing your certificate if you upload a custom certificate. For example, IBM CIS won't track the certificate expiration dates. 
 
### Alternatively, utilize a certificate provisioned by CIS
 
IBM CIS has partnered with several Certificate Authorities (CAs) to provide domain wildcard certificates for our customers, by default. Manual verification could be required for setting up these certificates, and your support team can help you perform these additional steps.
 
### Change your TLS setting to **End-to-End CA Signed**
 
Most of our Enterprise customers utilize the End-to-End CA Signed security setting. An **End-to-End CA Signed** setting requires a valid, CA-signed certificate installed on your web server. The certificate's expiration date must be in the future, and it must have a matching *hostname* or *Subject Alternative Name (SAN)*.

