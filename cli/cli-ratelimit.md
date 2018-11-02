---

copyright:
  years: 2018
lastupdated: "2018-09-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Rate Limiting

The following `ratelimit` commands are available:

* Create
* Update
* List
* Detail
* Delete


## Create Rate Limit rule

**NAME**

    `ratelimit-rule-create` - Create a new rate limiting rule for a given DNS domain. (enterprise plan only)

**USAGE**

   `ibmcloud cis ratelimit-rule-create  DNS_DOMAIN_ID (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.

**OPTIONS**

   `-s, --json-str`  The JSON data describing a rate limit rule.

The required fields in JSON data are `match`, `threshold`, `period`, `action`:

 * `match`: Determines which traffic the rate limiting rule counts towards the threshold.
   * `request`: Matches HTTP requests.
     * `methods`:  HTTP Methods, can be a subset [`POST`,`PUT`] or all [`_ALL_`]. This field is not required to create a  
                                                             rate limit rule. Valid values are `GET`, `POST`, `PUT`, `DELETE`, `PATCH`, `HEAD`, `_ALL_`.
     * `schemes`:  HTTP Schemes, can be one [`HTTPS`], both [`HTTP`,`HTTPS`] or all [`_ALL_`]. This field is not required.
     * `url`: The URL pattern to match comprised of the host and path, for instance, example.org/path. Wildcards are expanded to match applicable traffic, query strings are not matched. Use `*` for all traffic to your zone. Max length is 1024.
   * `response`: Matches HTTP responses before they are returned to the client . If this is defined, then the entire counting of traffic occurs at this stage. This field is not required.
     * `status`: HTTP Status codes, can be one [403], many [401,403] or indicate all by not providing this value. This field is not required. Min value: 100, max value: 999.
     * `headers`: Array of response headers to match. If a response does not meet the header criteria then the request is not counted towards the rate limiting rule. The header matching criteria includes following properties.
       * `name`: The name of the response header to match.
       * `op`: The operator when matching, eq means equals, ne means not equals. Valid values are `eq` and `ne`.
       * `value`: The value of the header, which is exactly matched.
   * `threshold`: The threshold that triggers the rate limit mitigations, combined with period. For example, threshold per period. Min value: 2, max value: 1000000.                       
   * `period`: The time, in seconds, to count matching traffic. If the count exceeds threshold within this period the action is performed. Min value:1, max value: 3600.
   * `action`: The action performed when the threshold of matched traffic within the period defined is exceeded.
     * `mode`: The type of action performed. Valid values are: `simulate`, `ban`, `challenge`, `js_challenge`.
     * `timeout`: The time, in seconds, as an integer to perform the mitigation action. Timeout be the same or greater than the period. This field is valid only when mode is `simulate` or `ban`. Min value: 10, max value: 86400.
     * `response`: Custom content-type and body to return. This overrides the custom error for the zone. This field is not required. Omission results in the default HTML error page. This field is valid only when mode is `simulate` or `ban`.
       * `content_type`: The content-type of the body, which must be one of the following: `text/plain`, `text/xml`, `application/json`.
       * `body`: The body to return. The content here must conform to the `content_type`. Max length is 10240.

The optional fields are `id`, `disabled`, `description`, and `bypass`:
      
   * `id`: Identifier of the rate limiting rule.
   * `disabled`: Whether this rate limiting rule is currently disabled.
   * `description`: A note that you can use to describe the reason for a rate limiting rule.
   * `bypass`: Criteria that allows the rate limit to be bypassed. For example, to express that you shouldn’t apply a rate limit to a given set of URLs.
     * `name`: Valid values is `url`.
     * `value`: The url to bypass.

**Sample JSON data**:
```
                          {
                                  "id": "92f17202ed8bd63d69a66b86a49a8f6b",
                                  "disabled": false,
                                  "description": "Prevent multiple login failures to mitigate brute force attacks",
                                  "bypass": [
                                          {
                                                  "name": "url",
                                                  "value": "api.example.com/*"
                                          }
                                    ],
                                    "threshold": 60,
                                    "period": 900,
                                    "action": [
                                            {
                                                   "mode": "simulate",
                                                   "timeout": 86400,
                                                   "response": {
                                                           "content_type": "text/plain",
                                                           "body": "<error>This request has been rate-limited.</error>"
                                                   }
                                             }
                                     ],
                                     "match": {
                                             "request": {
                                                     "methods": [
                                                             "GET"
                                                      ],
                                                      "schemes": [
                                                             "HTTP",
                                                             "HTTPS"
                                                      ],
                                                      "url": "*.example.org/path*"
                                              },
                                              "response": {
                                                       "status": [
                                                               403, 401
                                                        ],
                                                       "headers": [
                                                                 {
                                                                         "name": "Cf-Cache-Status",
                                                                         "op": "eq",
                                                                         "value": "HIT"
                                                                  }
                                                        ]
                                              }
                                     }
                          }
```

   `-j, --json-file` A file contains input JSON data.
   
   `-i, --instance` Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   
   `-o, --output` Specify output format, only JSON is supported now.

**Output Table Columns:**

  * ID
  * disabled
  * description
  * match
  * bypass
  * threshold
  * period
  * action

## Update Rate Limit rule

**NAME**

   `ratelimit-rule-update` - update a rate limiting rule of a given DNS domain.

**USAGE**

   `ibmcloud cis ratelimit-rule-update DNS_DOMAIN_ID RATELIMIT_RULE_ID  (-s, --json-str JSON_STR | -j, --json-file JSON_FILE) [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`


**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `RATELIMIT_RULE_ID` is the ID of rate limiting rule. 

**OPTIONS**

   `-s, --json-str`  The JSON data describing a rate limit rule.

The required fields in JSON data are `id`, `match`, `threshold`, `period`, `action`:

  * `id`: Identifier of the rate limiting rule.
  * `match`: Determines which traffic the rate limit counts towards the threshold.
    * `request`: Matches HTTP requests.
      * `methods:  HTTP Methods, can be a subset [`POST`,`PUT`] or all [`_ALL_`]. This field is not required to create a rate limit rule. Valid values are `GET`, `POST`, `PUT`, `DELETE`, `PATCH`, `HEAD`, `_ALL_`.
      * `schemes`:  HTTP Schemes, can be one [`HTTPS`], both [`HTTP`,`HTTPS`] or all [`_ALL_`]. This field is not required.
      * `url: The URL pattern to match comprised of the host and path, for example, example.org/path. Wildcards are expanded to match applicable traffic, query strings are not matched. Use `*` for all traffic to your zone. Max length is 1024.
    * `response`: Matches HTTP responses before they are returned to the client . When defined, the entire counting of traffic occurs at this stage. This field is not required.
      * `status`: HTTP Status codes, can be one [403], many [401,403] or indicate all by not providing this value. This field is not required. Min value: 100, max value: 999.
      * `headers`: Array of response headers to match. If a response does not meet the header criteria then the request is not counted towards the rate limit. The header matching criteria includes following properties.
        * `name`: The name of the response header to match.
        * `op`: The operator when matching, eq means equals, ne means not equals. Valid values are `eq` and `ne`.
        * `value`: The value of the header, which is exactly matched.
  * `threshold`: The threshold that triggers the rate limit mitigations, combined with period. For example, threshold per period. Min value: 2, max value: 1000000.                       
  * `period`: The time, in seconds, to count matching traffic. If the count exceeds threshold within this period the action is performed. Min value:1, max value: 3600.
  * `action`: The action to be performed when the threshold of matched traffic within defined period is exceeded.
    * `mode`: The type of action performed. Valid values are: `simulate`, `ban`, `challenge`, `js_challenge`.
    * `timeout`: The time, in seconds as an integer, to perform the mitigation action. Timeout must be the same or greater than the period. This field is only valid when mode is `simulate` or `ban`. Min value: 10, max value: 86400.
    * `response`: Custom content-type and body to return. This overrides the custom error for the zone. This field is not required. Omission results in default HTML error page. This field is only valid when mode is `simulate` or `ban`.
      * `content_type`: The content-type of the body. Must be one of the following: `text/plain`, `text/xml`, `application/json`.
      * `body`: The body to return. The content here must conform to the content_type. Max length is 10240.

The optional fields are `disabled`, `description`, and `bypass`:      
                    
 * `disabled`: Whether this rate limiting rule is currently disabled.
 * `description`: A note that you can use to describe the reason for a rate limit.
 * `bypass`: Criteria that allows the rate limit to be bypassed. For example, to express that you shouldn’t apply a rate limit to a given set of URLs.
    * `name`: Valid values is `url`.
    * `value`: The url to bypass.

  `-j, --json-file` A file contains input JSON data.
  
  `-i, --instance` Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
  
  `-o, --output` Specify output format, only JSON is supported now.


**Output Table Columns**

  * ID
  * disabled
  * description
  * match
  * bypass
  * threshold
  * period
  * action


## List Rate Limit rules

**NAME**

   `ratelimit-rules` - List rate limiting rules of a given DNS domain.

**USAGE**

   `ibmcloud cis ratelimit-rules  DNS_DOMAIN_ID [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.

**OPTIONS**

  `-i, --instance`   Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
  
  `-o, --output`     Specify output format, only JSON is supported now.


**Output Table Columns**

  * ID
  * disabled
  * description
  * match
  * bypass
  * threshold
  * period
  * action



## Detail Rate Limit rule

**NAME**

   `ratelimit-rule` - Get details of a rate limiting rule by ID.

**USAGE**

   `ibmcloud cis ratelimit-rule DNS_DOMAIN_ID  RATELIMIT_RULE_ID [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `RATELIMIT_RULE_ID` is the ID of rate limit rule. 

**OPTIONS**

   `-i, --instance`   Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   
   `-o, --output`     Specify output format, only JSON is supported now.


**Output Table Columns**

  * ID
  * disabled
  * description
  * match
  * bypass
  * threshold
  * period
  * action



## Delete Rate Limit rule

**NAME**

   `ratelimit-rule-delete` - Delete a rate limiting rule by ID.

**USAGE**

   `ibmcloud cis ratelimit-rule-delete DNS_DOMAIN_ID RATELIMIT_RULE_ID [-i, --instance INSTANCE_NAME] [-o, --output FORMAT]`

**ARGUMENTS**

   `DNS_DOMAIN_ID` is the ID of DNS domain.
   
   `RATELIMIT_RULE_ID` is the ID of rate limit rule. 

**OPTIONS**

   `-i, --instance`   Instance name. If not set, the context instance specified by `ibmcloud cis instance-set` is used.
   
   `-o, --output`     Specify output format, only JSON is supported now.


**Output Table Columns**

   * ID


