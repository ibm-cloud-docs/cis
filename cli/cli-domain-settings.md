---

copyright:
  years: 2018
lastupdated: "2018-10-29"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Domain

The following `domain-settings` commands are available:

* Display domain-settings
* Update domain-settings

## Display domain-settings
**NAME**

   `domain-settings` - Get details of a feature for the domain.

**USAGE**

   `ibmcloud cis domain-settings DNS_DOMAIN_ID (-g, --group GROUP | -f, --feature FEATURE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the id of DNS domain.

**OPTIONS**

   `-g value, --group value`    Display features in a same group.Valid values for "group" are "all", "domain", "reliability", "performance", "security".

   `-f value, --feature value`  Feature of domain settings to check. Valid values are as follow: 
   
                               "always_use_https": 
                                   Redirect all requests with scheme "http" to "https". This applies to all http requests to the domain.
                               "automatic_https_rewrites": 
                                   Help fix mixed content by changing "http" to "https" for all resources or links on your web site that can be served with HTTPS.
                               "browser_check": 
                                   Evaluate HTTP headers from your visitors browser for threats. If a threat is found a block page will be delivered.
                               "challenge_ttl": 
                                   Specify how long a visitor with a bad IP reputation is allowed access to your website after completing a challenge.
                               "cname_flattening": 
                                   Follow a CNAME to where it points and return that IP address instead of the CNAME record.
                                   By default, only flatten the CNAME at the root of your domain.
                               "hotlink_protection": 
                                   Protect your images from off-site linking.
                               "http2": 
                                   Accelerate your website with HTTP/2.
                               "image_load_optimization": 
                                   Improve load time for pages that include images on mobile devices with slow network connections. (enterprise plan only)
                               "image_size_optimization": 
                                   Improve image load time by optimizing images hosted on your domain. (enterprise plan only)
                               "ip_geolocation": 
                                   Include the country code of the visitor location with all requests to your website.
                               "ipv6": 
                                   Enable IPv6 support and gateway.
                               "max_upload": 
                                   The amount of data visitors can upload to your website in a single request.
                               "min_tls_version": 
                                   Only allow HTTPS connections from visitors that support the selected TLS protocol version or newer.
                               "minify": 
                                   Reduce the file size of source code on your website.
                               "mobile_redirect": 
                                   Redirect visitors that are using mobile devices to a mobile-optimized website.
                               "opportunistic_encryption": 
                                   Opportunistic Encryption allows browsers to benefit from the improved performance of HTTP/2 
                                   by letting them know that your site is available over an encrypted connection.
                               "origin_error_page_pass_thru": 
                                   When Origin Error Page is set to "On", CIS will proxy the 502 and 504 error pages directly from the origin. (enterprise plan only)
                               "prefetch_preload": 
                                   CIS will prefetch any URLs included in the prefetch HTTP header. (enterprise plan only)
                               "pseudo_ipv4": 
                                   Adds an IPv4 header to requests when a client is using IPv6, but the server only supports IPv4.
                               "response_buffering": 
                                   Enable or disable buffering of responses from the origin server. (enterprise plan only)
                               "script_load_optimization": 
                                   Improve the paint time for pages that include JavaScript. (enterprise plan only)
                               "security_header": 
                                   Enforce web security policy for your website.
                               "server_side_exclude": 
                                   Automatically hide specific content from suspicious visitors.
                               "sha1_support": 
                                   Enable support for legacy user agents that do not support certificates signed with modern SHA-2 signatures.
                               "tls_client_auth": 
                                   TLS client certificate presented for authentication on origin pull. (enterprise plan only)
                               "true_client_ip_header": 
                                   CIS will send the end user’s IP address in the True-Client-IP header. (enterprise plan only)
                               "waf": 
                                   A Web Application Firewall (WAF) blocks requests that contain malicious content.
                               "websockets": 
                                   Allow WebSockets connections to your origin server.
                                   
   `-i value, --instance value`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-o value, --output value`    Specify output format, only JSON is supported now.

**Output**
  * ID                     
  * Value         
  * Modified On  
  * Editable      

## Update domain-settings

**NAME**

   `domain-settings-update` - Update a feature for the domain.

**USAGE**

   `ibmcloud cis domain-settings-update DNS_DOMAIN_ID (-f, --feature FEATURE) (-v, --value VALUE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the id of DNS domain.

**OPTIONS**

   `-f value, --feature value`      The Domain feature to get Valid values are as follow: 
   
                               "always_use_https": 
                                   Redirect all requests with scheme "http" to "https". This applies to all http requests to the domain.
                               "automatic_https_rewrites": 
                                   Help fix mixed content by changing "http" to "https" for all resources or links on your web site that can be served with HTTPS.
                               "browser_check": 
                                   Evaluate HTTP headers from your visitors browser for threats. If a threat is found a block page will be delivered.
                               "challenge_ttl": 
                                   Specify how long a visitor with a bad IP reputation is allowed access to your website after completing a challenge.
                               "cname_flattening": 
                                   Follow a CNAME to where it points and return that IP address instead of the CNAME record.
                                   By default, only flatten the CNAME at the root of your domain.
                               "hotlink_protection": 
                                   Protect your images from off-site linking.
                               "http2": 
                                   Accelerate your website with HTTP/2.
                               "image_load_optimization": 
                                   Improve load time for pages that include images on mobile devices with slow network connections. (enterprise plan only)
                               "image_size_optimization": 
                                   Improve image load time by optimizing images hosted on your domain. (enterprise plan only)
                               "ip_geolocation": 
                                   Include the country code of the visitor location with all requests to your website.
                               "ipv6": 
                                   Enable IPv6 support and gateway.
                               "max_upload": 
                                   The amount of data visitors can upload to your website in a single request.
                               "min_tls_version": 
                                   Only allow HTTPS connections from visitors that support the selected TLS protocol version or newer.
                               "minify": 
                                   Reduce the file size of source code on your website.
                               "mobile_redirect": 
                                   Redirect visitors that are using mobile devices to a mobile-optimized website.
                               "opportunistic_encryption": 
                                   Opportunistic Encryption allows browsers to benefit from the improved performance of HTTP/2 
                                   by letting them know that your site is available over an encrypted connection.
                               "origin_error_page_pass_thru": 
                                   When Origin Error Page is set to "On", CIS will proxy the 502 and 504 error pages directly from the origin. (enterprise plan only)
                               "prefetch_preload": 
                                   CIS will prefetch any URLs included in the prefetch HTTP header. (enterprise plan only)
                               "pseudo_ipv4": 
                                   Adds an IPv4 header to requests when a client is using IPv6, but the server only supports IPv4.
                               "response_buffering": 
                                   Enable or disable buffering of responses from the origin server. (enterprise plan only)
                               "script_load_optimization": 
                                   Improve the paint time for pages that include JavaScript. (enterprise plan only)
                               "security_header": 
                                   Enforce web security policy for your website.
                               "server_side_exclude": 
                                   Automatically hide specific content from suspicious visitors.
                               "sha1_support": 
                                   Enable support for legacy user agents that do not support certificates signed with modern SHA-2 signatures.
                               "tls_client_auth": 
                                   TLS client certificate presented for authentication on origin pull. (enterprise plan only)
                               "true_client_ip_header": 
                                   CIS will send the end user’s IP address in the True-Client-IP header. (enterprise plan only)
                               "waf": 
                                   A Web Application Firewall (WAF) blocks requests that contain malicious content.
                               "websockets": 
                                   Allow WebSockets connections to your origin server.

   `-v value, --type value`      The value set to the feature for domain.
 
                              Valid values for "always_use_https" are "on", "off".
                              Valid values for "automatic_https_rewrites" are "on", "off".
                              Valid values for "browser_check" are "on", "off".
                              Valid values for "challenge_ttl" are "300, 900, 1800, 2700, 3600, 7200, 10800, 14400, 28800, 57600, 86400, 604800, 2592000, 31536000".
                              Valid values for "cname_flattening" are "flatten_all", "flatten_at_root".
                                  "flatten_all": Flatten all CNAME records under your domain.
                                  "flatten_at_root": Flatten CNAME at root domain. This is the default value.
                              Valid values for "hotlink_protection" are "on", "off".
                              Valid values for "http2" are "on", "off".
                              Valid values for "image_load_optimization" are "on", "off".
                              Valid values for "image_size_optimization" are "off", "lossless", "lossy".
                                  "off": Disable Image Size Optimization.
                                  "lossless": Reduce the size of image files without impacting visual quality.
                                  "lossy": The file size of JPEG images is reduced using lossy compression, which may reduce visual quality.
                              Valid values for "ip_geolocation" are "on", "off".
                              Valid values for "ipv6" are "on", "off".
                              Valid values(in MB) for "max_upload" are:
                                  100, 125, 150, 175, 200 and 225, 250, 275, 300, 325, 350, 375, 400, 425, 450, 475, 500 only for Enterprise Plan.
                              Valid values for "min_tls_version" are "1.0", "1.1", "1.2", "1,3".
                              Valid values for "minify" are "css", "html", "js".
                                  "css": Automatically minify all CSS for your website.Valid values for "css" are "on", "off".
                                  "html": Automatically minify all HTML for your website.Valid values for "html" are "on", "off".
                                  "js": Automatically minify all JS for your website.Valid values for "js" are "on", "off".
                                  Eg: -v css=on,html=off,js=on
                              Valid values for "mobile_redirect" are "status", "mobile_subdomain", "strip_uri".
                                  "status": Whether or not the mobile redirection is enabled.Valid values for "status" are "on", "off".
                                  "mobile_subdomain": Which subdomain prefix you wish to redirect visitors on mobile devices to(subdomain must already exist).
                                  "strip_uri": Whether to drop the current page path and redirect to the mobile subdomain URL root.Valid values for "strip_uri" are "true", "false".
                                  Eg: -v status=on,mobile_subdomain=m,strip_uri=true
                              Valid values for "opportunistic_encryption" are "on", "off".
                              Valid values for "origin_error_page_pass_thru" are "on", "off".
                              Valid values for "prefetch_preload" are "on", "off".
                              Valid values for "pseudo_ipv4" are "overwrite_header", "off", "add_header".
                                  "overwrite_header": Overwrite the existing Cf-Connecting-IP and X-Forwarded-For headers with a pseudo IPv4 address.
                                  "off": Disable Pseudo IPv4.
                                  "add_header": Add additional Cf-Pseudo-IPv4 header only.
                              Valid values for "response_buffering" are "on", "off".
                              Valid values for "script_load_optimization" are "on", "off".
                              Valid values for "security_header" are "nosniff", "enabled", "max_age", "include_subdomains", "preload".
                                  "nosniff": Whether or not to send 'X-Content-Type-Options: nosniff' header.Valid values for "nosniff" are "true", "false".
                                  "enabled": Whether or not security_header is enabled.Valid values for "enabled" are "true", "false".
                                  "max_age": Specify the duration(in seconds) security_header are cached in browsers.
                                  "include_subdomains": Every domain below the domain will inherit the same security_header.Valid values for "include_subdomains" are "true", "false".
                                  "preload": Whether or not to permit browsers to preload security_header config.Valid values for "enabled" are "true", "false".
                                  Eg: -v enabled=true,max_age=100,include_subdomains=true,preload=true,nosniff=true
                              Valid values for "server_side_exclude" are "on", "off".
                              Valid values for "sha1_support" are "on", "off".
                              Valid values for "tls_client_auth" are "on", "off".
                              Valid values for "true_client_ip_header" are "on", "off".
                              Valid values for "waf" are "on", "off".
                              Valid values for "websockets" are "on", "off".
   
   `-i value, --instance value`  Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.

   `-o value, --output value`    Specify output format, only JSON is supported now.


**Output**
  * ID                     
  * Value         
  * Modified On  
  * Editable       
