---

copyright:
  years: 2019, 2025
lastupdated: "2025-02-28"

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Using fields, functions, and expressions
{: #fields-and-expressions}

Firewall rules are deprecated. CIS moved existing firewall rules to WAF custom rules. For more information on this change, see [Migrating to custom rules](/docs/cis?topic=cis-migrating-to-custom-rules).
{: deprecated} 

Along with actions, fields and expressions are the building blocks of firewall rules. These two elements work together when defining the criteria to use when a firewall rule is matched.
{: shortdesc}

## Fields
{: #fields}

When CIS receives an HTTP request, it is examined and a table of fields is produced to match against. This field table exists while the current request is being processed. Think of it as a table that holds the request properties to be matched against expressions.

Each field value can be sourced from different places, such as:

* Primitive propertiesare , obtained directly from the traffic – for example, `http.request.uri.path`.
* Derived values, resulting from a transformation, composition, or basic operation – for example, making the value of `http.request.uri.path` all lowercase and available as a field of another field.
* Computer values, resulting from a lookup, computation, or other intelligence – for example, a `cf.threat_score` calculated dynamically by a machine learning process that inspects related primitive and derived values.

### Available fields
{: #available-fields}

| Field name | Type | Example value | Notes |
| ------- | :--------- | :------------ | :--------- |
|http.cookie|String|session=A12345;-background=light|Entire cookie as a string|
|http.host|String| `www.example.com` | The hostname used in the full request URI|
|http.referer|String|_HTTP referer header_| |
|http.request.full_uri|String|`https://www.example.com/articles/index?section=539061&expand=comments`|The full URI as received by the web server (does not include _#fragment_, which is not sent to web servers)|
|http.request.method|String|POST|The HTTP method, in uppercase|
|http.request.uri|String|/articles/index?section=539061&expand=comments|The absolute URI of the request|
|http.request.uri.path|String|/articles/index|The path of the request|
|http.request.uri.query|String|section=539061&expand=comments|The whole query string, minus the delimiting prefix "?"|
|http.user_agent|String|Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36|The whole HTTP user agent|
|http.x_forwarded_for|String|_The full X-Forwarded-For HTTP header_ |
|ip.src|IP address|93.155.208.22|The client TCP IP address, which can be adjusted to reflect the real client IP of the original client as applicable (for example, by using HTTP headers like X-Forwarded-For or X-Real-IP)|
|ip.geoip.asnum|Number|222|The [Autonomous System](https://ibm.biz/BdzqdD) (AS) number|
|ip.geoip.country|String|GB|The [2-letter country code](https://www.iso.org/obp/ui/#search/code/){: external}|
|ssl|Boolean|true|Whether the HTTP connection to the client is encrypted|
{: caption="Available fields" caption-side="bottom"}

These standard fields follow the naming convention of the Wireshark display field reference. However, some subtle variations might exist in the preceding example values.
{: note}

In addition to the standard fields, the following Cloudflare-defined fields are also available:

| Field name | Type | Example value | Notes |
| ------- | :--------- | :------------ | :--------- |
|cf.client.bot|Boolean|true|This field indicates whether the request is coming from a known bot or crawler, regardless of good or bad intent.|
|cf.threat_score|Number|A 0-100 value|This field represents a risk score, 0 indicates low risk as determined by Cloudflare. Values greater than 10 can represent spammers or bots, and values greater than 40 point to bad actors on the internet. 
It is rare to see values higher than 60, so tune your firewall rules to challenge those greater than 10, and to block those greater than 50.|
{: caption="Available Cloudflare fields" caption-side="bottom"}

## Functions
{: #functions}

The firewall rules language has several functions to convert fields.

These functions are not currently supported in the CIS UI Visual Expression Builder.
{: note}

| Function name| Argument types | Return type | Usage example | Notes|
| ------- | :--------- | :------------ | :--------- | :--------- |
|lower|String|String|lower(http.host) == `"www.example.com"`|Converts a string field to lowercase. Only uppercase ASCII bytes are being converted. Every other bytes are left as-is.|
|upper|String|String|upper(http.host) == `"www.example.com"`|Converts a string field to uppercase. Only lowercase ASCII bytes are being converted. Every other bytes are left as-is.|
{: caption="Firewall rules functions" caption-side="bottom"}

## Expressions
{: #expressions}

An expression returns true or false based on a match against incoming traffic. For example:

```sh
http.host eq "www.example.com" and ip.src in 92.182.212.0/24
```
{: screen}

In this example, two single expressions comprise a compound expression. Think of each single expression as a condition. Each condition is evaluated individually before applying and logic to determine the final result of the compound expression.

Looking at the first single expression, you can see that it contains:

* a field - `http.host`
* a comparison operator - `eq`
* a value - `"www.example.com"`

Not all conditions have the same structure. Other examples that use different structures are discussed in the next section.

### Comparison operators
{: #comparison-operators}

The following comparison operators are available for use in expressions:

| English| C-like| Description|
| ------- | :--------- | :------------ |
|eq|==|Equal|
|ne|!=|Not equal|
|lt|<|Less than|
|le|<=|Less than or equal to|
|gt| &amp;gt; |Greater than|
|ge|&amp;gt;= |Greater than or equal to|
|contains| |Exactly contains|
|matches|~|[Re2](https://github.com/google/re2/wiki/Syntax) inspired regular expression|
|in| |Value appears in a set of values. Supports ranges that use the ".." notation. |
|not|!|See Boolean comparison|
|bitwise_and|&|Compare bit field value|
{: caption="Comparison operators for expressions" caption-side="bottom"}

Currently the CIS UI Visual Expression Builder supports only English operators.
{: note}

An expression might contain a mix of English and C-like operators. For example, `ip.src eq 93.184.216.34` is equivalent to `ip.src == 93.184.216.34`.

Certain comparison operators apply to specific fields based on type. The following matrix provides examples of which operators are available for various field types:

| English| C-like| String| IP address| Number|
| ------- | :--------- | :------------ | :--------- | :--------- |
|eq|==|http.request.uri.path eq "/articles/2008/"|ip.src eq 93.184.216.0|cf.threat_score eq 10|
|ne|!=|http.request.uri.path ne "/articles/2010/"|ip.src ne 93.184.216.0|cf.threat_score ne 60|
|lt|<|http.request.uri.path lt "/articles/2009/"| |cf.threat_score lt 10|
|le|<=|http.request.uri.path le "/articles/2008/"| |cf.threat_score le 20|
|gt|&amp;gt;|http.request.uri.path gt "/articles/2006/"| |cf.threat_score gt 25|
|ge|&amp;gt;=|Greater than or equal to| |cf.threat_score ge 60|
|contains| |http.request.uri.path contains "/articles/"| | |
|matches|~|http.request.uri.path ~ "^/articles/200[7-8]/$"| | |
|in| |http.request.method in { "HEAD" "GET" }|ip.src in { 93.184.216.0 93.184.216.1 }|cf.threat_score in {0 2 10}|
{: caption="Comparison operators for fields" caption-side="bottom"}

The evaluation of expressions that use string values is case-sensitive. As such, a firewall rule might require you to define more than one test condition. Enterprise customers can use a regular expression with the matches operator to capture multiple variations with a single expression.
{: important}

### Boolean comparison
{: #boolean-comparison}

For fields of Boolean type (for example, `ssl`) the field appears by itself in the expression when evaluating for a true condition. For a false condition, the **not** operator applies.

| True| False|
| ------- | :--------- |
|ssl|not ssl|
{: caption="Boolean comparison" caption-side="bottom"}

## Compound expressions
{: #compound-expressions}

You can create compound expressions by grouping two or more single expressions by using logical operators.

| English| C-like| Description|Example|Precedence|
| ------- | :--------- | :------------ | :--------- | :--------- |
|not|!|Logical NOT|not (http.host eq `"www.example.com"` and ip.src in 93.184.216.0/24)|1|
|and|&&|Logical AND|http.host eq `"www.example.com"` and ip.src in 93.184.216.0/24|2|
|xor|^^|Logical XOR|http.host eq `"www.example.com"` xor ip.src in 93.184.216.0/24|3|
|or|&verbar;&verbar;|Logical OR|http.host eq `"www.example.com"` or ip.src in 93.184.216.0/24|4|
{: caption="Compound expressions" caption-side="bottom"}

To alter the order of precedence, you can group expressions with parentheses. Using no parentheses, expressions are implicitly grouped based on standard precedence:

```sh
ssl and http.request.uri.path eq /login or http.request.uri.path eq /oauth
```
{: screen}

Applying explicit grouping:

```sh
(ssl and http.request.uri.path eq /login) or http.request.uri.path eq /oauth
```
{: screen}

Giving precedence to or with parentheses:

```sh
ssl and (http.request.uri.path eq /login or http.request.uri.path eq /oauth)
```
{: screen}

While `not` is used for grouping, it can be used to negate a single comparison. For example, `not ip.src eq 93.184.216.0` is equivalent to `not (ip.src eq 93.184.216.0)`.

Finally, you can also negate grouped expressions:

```sh
not (http.request.method eq "POST" and http.request.uri.path eq "/login")
```
{: screen}

### Deviations from Wireshark display filters
{: #deviations}

Firewall rules expressions are inspired by Wireshark display filters. However, the implementation deviates in the following ways:

* For CIDR IP equality tests, Wireshark allows ranges in the format `ip.src == 1.2.3.0/24`, while CIS supports equality tests using only a single IP address. To compare a CIDR, use the `in` operator; for example, `ip.src in {1.2.3.0/24}`.
* In Wireshark, `ssl` is a protocol field that contains hundreds of other fields of various types that are available for comparison in multiple ways. However, in Firewall Rules, `ssl` is a single Boolean field that is used to determine whether the connection from the client to CIS is encrypted.
* The `slice` operator is not supported.
* Not all functions are supported. Currently, `len()`, and `count()` are not supported.
