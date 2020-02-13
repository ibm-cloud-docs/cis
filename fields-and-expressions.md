---

copyright:
  years: 2019, 2020
lastupdated: "2020-02-10"

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:important: .important}
{:tip: .tip}

# Fields and expressions
{: #fields-and-expressions}

Along with actions, fields and expressions are the building blocks of Firewall Rules. These two elements work together when defining the criteria to use when a Firewall Rule is matched.
{:shortdesc}

## Fields

When CIS receives an HTTP request, it is examined and a table of fields is produced to match against. This field table exists for as long as the current request is being processed. Think of it as a table that holds the request properties to be matched against expressions.

Each field value can be sourced from different places, such as:

* Primitive properties, obtained directly from the traffic – for example, `http.request.uri.path`.
* Derived values, resulting from a transformation, composition, or basic operation – for example, makeing the value of `http.request.uri.path` all lowercase and available as a field of another field.
* Computer values, resulting from a lookup, computation, or other intelligence – for example, a `cf.threat_score` calculated dynamically by a machine learning process that inspects related primitive and derived values.

### Available fields

| Field name | Type | Example value | Notes |
| ------- | :--------- | :------------ | :--------- |
|http.cookie|String|session=A12345;-background=light|Entire cookie as a string|
|http.cookie|String|`www.example.com`|The host name used in the full request URI|
|http.referer|String|_HTTP referer header_||
|http.request.full_uri|String|`https://www.example.com/articles/index?section=539061&expand=comments`|The full URI as received by the web server (does not include _#fragment_ which is not sent to web servers)|
|http.request.method|String|POST|The HTTP method, in upper case|
|http.request.uri|String|/articles/index?section=539061&expand=comments|The absolute URI of the request|
|http.request.uri.path|String|/articles/index|The path of the request|
|http.request.uri.query|String|section=539061&expand=comments|The whole query string, minus the delimiting prefix "?"|
|http.user_agent|String|Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36|The whole HTTP user agent|
|http.x_forwarded_for|String|_The full X-Forwarded-For HTTP header_ |
|ip.src|IP address|93.155.208.22|The client TCP IP address, which may be adjusted to reflect the real client IP of the original client as applicable (for example, using HTTP headers like X-Forwarded-For or X-Real-IP)|
|ip.geoip.asnum|Number|222|The [Autonomous System](https://ibm.biz/BdzqdD) (AS) number|
|ip.geoip.country|String|GB|The [2-letter country code](https://support.cloudflare.com/hc/en-us/articles/217074967#1QrbtSK5NSL7A0FOWD2bbZ){:external}|
|ssl|Boolean|true|Whether the HTTP connection to the client is encrypted|

These standard fields follow the naming convention of the Wireshark display field reference. However, some subtle variations may exist in the example values provided above.
{: note}

In addition to the standard fields outlined above, the following Cloudflare-defined fields are also available:

| Field name | Type | Example value | Notes |
| ------- | :--------- | :------------ | :--------- |
|cf.client.bot|Boolean|true|This field indicates whether the request is coming from a known bot or crawler, regardless of good or bad intent.|
|cf.threat_score|Number|A 0-100 value|This field represents a risk score, 0 indicates low risk as determined by Cloudflare. Values above 10 may represent spammers or bots, and values above 40 point to bad actors on the Internet. It is rare to see values above 60, so tune your firewall rules to challenge those above 10, and to block those above 50.|

## Functions

The Firewall Rules language has a number of functions to convert fields:

These are not currently supported in the CIS UI **Visual Expression Builder**.
{: note}

| Function name| Argument types | Return type | Usage example | Notes|
| ------- | :--------- | :------------ | :--------- | :--------- |
|lower|String|String|lower(http.host) == `"www.example.com"`|Converts a string field to lowercase. Only uppercase ASCII bytes are being converted, every other bytes are left as-is.|
|upper|String|String|upper(http.host) == `"www.example.com"`|Converts a string field to uppercase. Only lowercase ASCII bytes are being converted, every other bytes are left as-is.|

## Expressions

An expression returns true or false based on a match against incoming traffic. For example:

```
http.host eq "www.example.com" and ip.src in 92.182.212.0/24
```

In the example above, two single expressions comprise a compound expression. Think of each single expression as a condition. Each condition is evaluated individually before applying and logic to determine the final result of the compound expression.

Looking at the first single expression above, you can see that it contains:

* a field - `http.host`
* a comparison operator - `eq`
* a value - `"www.example.com"`

Not all conditions have the same structure, as shown above. Additional examples using different structures are discussed in the next section.

### Comparison operators

The following comparison operators are available for use in expressions:

| English| C-like| Description|
| ------- | :--------- | :------------ |
|eq|==|Equal|
|ne|!=|Not equal|
|lt|<|Less than|
|le|<=|Less than or equal to|
|gt|>|Great than|
|ge|>=|Greater than or equal to|
|contains||Exactly contains|
|matches|~|[Re2](https://github.com/google/re2/wiki/Syntax) inspired regular expression|
|in||Value appears in a set of values. Supports ranges using the ".." notation. |
|not|!|See Boolean comparison|
|bitwise_and|&|Compare bit field value|

Currently the CIS UI **Visual Expression Builder** only supports English operators.
{: note}

An expression may contain a mix of English and C-like operators. For example, `ip.src eq 93.184.216.34` is equivalent to `ip.src == 93.184.216.34`.

Certain comparison operators apply to specific fields based on type. The following matrix provides examples of which operators are available for various field types:

| English| C-like| String|IP Address|Number|
| ------- | :--------- | :------------ | :--------- | :--------- |
|eq|==|http.request.uri.path eq "/articles/2008/"|ip.src eq 93.184.216.0|cf.threat_score eq 10|
|ne|!=|http.request.uri.path ne "/articles/2010/"|ip.src ne 93.184.216.0|cf.threat_score ne 60|
|lt|<|http.request.uri.path lt "/articles/2009/"||cf.threat_score lt 10|
|le|<=|http.request.uri.path le "/articles/2008/"||cf.threat_score le 20|
|gt|>|http.request.uri.path gt "/articles/2006/"||cf.threat_score gt 25|
|ge|>=|Greater than or equal to||cf.threat_score ge 60|
|contains||http.request.uri.path contains "/articles/"|||
|matches|~|http.request.uri.path ~ "^/articles/200[7-8]/$"|||
|in||http.request.method in { "HEAD" "GET" }|ip.src in { 93.184.216.0 93.184.216.1 }|cf.threat_score in {0 2 10}|

The evaluation of expressions using string values is case-sensitive. As such, a firewall rule may require you to define more than one test condition. Enterprise customers can use a regular expression with the matches operator to capture multiple variations with a single expression.
{: important}

### Boolean Comparison

For fields of boolean type (for example, `ssl`) the field appears by itself in the expression when evaluating for a true condition. For a false condition, the **not** operator applies.

| True| False|
| ------- | :--------- |
|ssl|not ssl|

## Compound expression

You can create compound expressions by grouping two or more single expressions using logical operators.

| English| C-like| Description|Example|Precedence|
| ------- | :--------- | :------------ | :--------- | :--------- |
|not|!|Logical NOT|not ( http.host eq `"www.example.com"` and ip.src in 93.184.216.0/24 )|1|
|and|&&|Logical AND|http.host eq `"www.example.com"` and ip.src in 93.184.216.0/24|2|
|xor|^^|Logical XOR|http.host eq `"www.example.com"` xor ip.src in 93.184.216.0/24|3|
|or|<code>&#124;&#124;</code>|Logical OR|http.host eq `"www.example.com"` or ip.src in 93.184.216.0/24|4|

To alter the order of precedence, you can group expressions with parentheses.

Using no parentheses, expressions are implicitly grouped based on standard precedence:

```
ssl and http.request.uri.path eq /login or http.request.uri.path eq /oauth
```

Applying explicit grouping:

```
(ssl and http.request.uri.path eq /login) or http.request.uri.path eq /oauth
```

Giving precedence to or with parentheses:

```
ssl and (http.request.uri.path eq /login or http.request.uri.path eq /oauth)
```

Note that while `not` is used for grouping, it can be used to negate a single comparison. For example, `not ip.src eq 93.184.216.0` is equivalent to `not (ip.src eq 93.184.216.0)`.

Finally, you can also negate grouped expressions:

```
not (http.request.method eq "POST" and http.request.uri.path eq "/login")
```

### Deviations from Wireshark Display Filters

Firewall Rules expressions are inspired by Wireshark Display Filters. However, the implementation deviates in the following ways:

* For CIDR IP equality tests, Wireshark allows ranges in the format `ip.src == 1.2.3.0/24`, while CIS only supports equality tests using a single IP address. To compare a CIDR, use the `in` operator; for example, `ip.src in {1.2.3.0/24}`.
* In Wireshark, `ssl` is a protocol field containing hundreds of other fields of various types that are available for comparison in multiple ways. However in Firewall Rules, `ssl` is a single boolean field used to determine if the connection from the client to CIS is encrypted.
* The `slice` operator is not supported.
* Not all functions are supported. We do not currently support `len()`, and `count()`.
