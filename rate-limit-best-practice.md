---

copyright:
  years: 2026
lastupdated: "2026-01-08"

keywords: HA for CIS, DR for CIS, CIS recovery time objective, CIS recovery point objective

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}


# Rate limiting best practices
{: #rate-limit-best}

The following sections cover typical rate limiting configurations for common use cases. You can combine the provided example rules and adjust them to your own scenario.

The main use cases for rate limiting are the following:

* Enforce granular access control to resources which includes the access control based on criteria such as user agent, IP address, referrer, host, country, and world region.
* Protect against credential stuffing and account takeover attacks.
* Limit the number of operations performed by individual clients. Includes preventing scraping by bots, accessing sensitive data, bulk creation of new accounts, and programmatic buying in e-commerce platforms.
* Protect REST APIs from resource exhaustion (targeted DDoS attacks) and resources from abuse in general.
* Protect GraphQL APIs by preventing server overload and limiting the number of operations.

## Enforcing granular access control
{: #enforce-granular-access}

You can use rate limiting to control how users and applications access your resources.
Rate limiting helps protect your application from abuse by restricting traffic based on attributes such as user agent, IP address, referrer, or host.

Each of the following examples demonstrates how to configure a rate-limiting rule for a specific access control scenario.

### Limiting request by user agent
{: #limit-user-agent}

You can restrict the number of requests that are allowed for a specific user agent. The following rule example allows mobile app users to make up to 100 requests every 10 minutes. You might also create a separate rule limiting the rate for desktop browsers.

| Setting | Value |
|----------|-----------------------|
| Matching criteria | User Agent equals `MobileApp` |
| Expression | `http.user_agent eq "MobileApp"` |
| Counting characteristics | IP |
| Rate (Requests/Period) | 100 requests / 10 minutes |
| Action | Managed Challenge |
{: caption="Example—Limit requests by user agent" caption-side="bottom"}

### Allowing specific IP addresses or ASNs
{: #Allow-specific-IP-addresses}

Control access by including or excluding certain IP addresses or Autonomous System Numbers (ASNs) from a rate limiting rule.

The following rate limiting rule example allows up to 10 requests per minute from the same IP address and make a `GET` request to the `/status` path, provided the IP address is not included in the [IP list](/docs/cis?topic=cis-custom-list-types#lists-ip-address) entitled `partner_ips`.

| Setting |	Value |
|----------|-----------------------|
| Matching criteria | URI Path equals `/status` and Request Method equals `GET` and IP Source Address is not in list `partner_ips` |
| Expression | `http.request.uri.path eq "/status" and http.request.method eq "GET" and not ip.src in $partner_ips` |
| Counting characteristics | IP |
| Rate (Requests/Period) | 10 requests / 1 minute |
| Action | Managed Challenge |
{: caption="Example—Allow specific IPs or ASNs" caption-side="bottom"}

### Limiting requests by referrer
{: #limit-by-ref}

You can limit requests that originate from referrer pages, such as third-party advertisements or external websites. This use case helps to reduce the risk of indirect denial-of-service (DDoS) attacks and helps you to manage request quotas.

| Setting |	Value |
|----------|-----------------------|
| Matching criteria | URI Path equals `/status` and Request Method equals `GET` |
| Expression | `http.request.uri.path eq "/status" and http.request.method eq "GET"` |
| Counting characteristics | Header (`Referrer`). The HTTP header name uses a misspelling of `referrer`. |
| Rate (Requests/Period) | 100 requests / 10 minutes |
| Action | Block |
{: caption="Example—Limit requests by referrer" caption-side="bottom"}

This example rule requires Advanced Rate Limiting.
{: note}

## Protecting against credential stuffing
{: #protect-against-credentials}

You can use rate limiting to protect login endpoints from [`credential stuffing`](https://www.ibm.com/docs/en/gdp/12.x?topic=policies-credential-stuffing-attack){: external} attacks. Credential stuffing occurs when attackers use automated scripts to try multiple username and password combinations on a login form. Rate limiting helps mitigate these attacks by restricting repeated failed login attempts from the same IP address.

The following examples show three rate-limiting rules that increase restrictions and penalties based on the number of failed login attempts.

### Rule 1: Initial protection threshold
{: #rule-1-initial-protection}

Rule 1 allows up to four failed login attempts per minute. When the limit is exceeded, the system triggers a Managed Challenge. This configuration helps legitimate users recover from occasional login errors while discouraging automated bots.

| Setting |	Value |
|----------|-----------------------|
| Matching criteria | Hostname equals `example.com` and URI Path equals `/login` and Request Method equals `POST` |
| Expression | `http.host eq "example.com" and http.request.uri.path eq "/login" and http.request.method eq "POST"`|
| Counting characteristics | IP |
| Increment counter when | URI Path equals `/login` and Method equals `POST` and Response code is in (401, 403) |
| Counting expression | `http.request.uri.path eq "/login" and http.request.method eq "POST" and http.response.code in {401 403}` |
| Rate (Requests/Period) | 4 requests / 1 minute |
| Action | Managed Challenge |
{: caption="Rule 1 configuration" caption-side="bottom"}

### Rule 2: Intermediate protection threshold
{: #rule-2-intermediate-protection}

If legitimate users pass the challenge when reaching rule 1's rate limit, Rule 2 applies additional protection for clients that continue to make failed login attempts. It allows up to 10 failed attempts over 10 minutes before triggering another Managed Challenge.

| Setting |	Value |
|----------|-----------------------|
| Matching criteria | Hostname equals `example.com` and URI Path equals `/login` and Request Method equals `POST` |
| Expression | `http.host eq "example.com" and http.request.uri.path eq "/login" and http.request.method eq "POST"`|
| Counting characteristics | IP |
| Increment counter when | URI Path equals `/login` and Request Method equals `POST` and Response Status Code is in (401, 403) |
| Counting expression | `http.request.uri.path eq "/login" and http.request.method eq "POST" and http.response.code in {401 403}` |
| Rate (Requests/Period) | 10 requests / 10 minutes |
| Action | Managed Challenge |
{: caption="Rule 2 configuration" caption-side="bottom"}

### Rule 3: Strict protection threshold
{: #rule-3-strict-protection}

Rule 3 enforces a stronger penalty to clients exceeding the rule 2 threshold by blocking an IP address for one day after 20 failed login attempts within an hour. This rule provides a final defense against persistent attack attempts.

| Setting |	Value |
|----------|-----------------------|
| Matching criteria | Host equals `example.com` |
| Expression | `http.host eq "example.com"`|
| Counting characteristics | IP |
| Increment counter when | URI Path equals `/login` and Request Method equals `POST` and Response Status Code is in (401, 403) |
| Counting expression | `http.request.uri.path eq "/login" and http.request.method eq "POST" and http.response.code in {401 403}` |
| Rate (Requests/Period) | 20 requests / 1 hour |
| Action | Block for 1 day |
{: caption="Rule 3 configuration" caption-side="bottom"}

All these example rules require a business plan or above.
{: important}

These three rules have a counting expression separate from the rule expression (also known as mitigation expression). When you configure a separate counting expression, the matching criteria is used when an action is triggered. In the counting expression, you can include conditions based on the HTTP response status code and HTTP response headers to integrate the rate limiting with your backend logic.

You can also decide to have two different expressions: a counting expression and a rule/mitigation expression — to define:

1. The requests used to compute the rate.
1. The requests actually acted upon.

For example, Rule 3 example computes the rate considering `POST` requests to `/login` that returned a `401` or `403` HTTP status code. However, when the rate limit is exceeded, CIS blocks every request to the `example.com` host generated by the same IP.

## Limiting the number of operations
{: #limit-number-of-operations}

You can use rate limiting to control how many operations a client performs within a specific time period. The rules that you configure depend on your application’s behavior and risk profile.

The following examples show how to prevent content scraping and automated activity that can overload your system or misuse your data. Examples include limiting requests by query string, JSON body parameters, or bot characteristics.

### Preventing content scraping by using query string
{: #prevent-content-scraping}

In this example, clients perform operations (such as price lookups or adding items to a basket) on an e-commerce website through query string parameters.
For example, a typical request that is sent by a client might be similar to the following:

```sh
GET https://store.com/merchant?action=lookup_price&product_id=215
Cookie: session_id=12345
```
{: pre}

Your security team might want to consider setting up a limit on the number of times a client can lookup prices to prevent bots — which might have eluded CIS Bot Management — from scraping the store's entire catalog.

| Setting | Value |
|----------|-----------------------|
| Matching criteria | URI Path equals `/merchant` and URI Query String contains `action=lookup_price` |
| Expression | `http.request.uri.path eq "/merchant" and http.request.uri.query contains "action=lookup_price"` |
| Counting characteristics | IP |
| Rate (Requests/Period) | 10 requests / 2 minutes |
| Action | Managed Challenge |
{: caption="Rule 1 configuration" caption-side="bottom"}

| Setting | Value |
|----------|-----------------------|
| Matching criteria | URI Path equals `/merchant` and URI Query String contains `action=lookup_price` |
| Expression | `http.request.uri.path eq "/merchant" and http.request.uri.query contains "action=lookup_price"` |
| Counting characteristics | IP |
| Rate (Requests/Period) | 20 requests / 5 minutes |
| Action | Block |
{: caption="Rule 2 configuration" caption-side="bottom"}

These two rate limiting rules match requests performing a selected action (look up price, in this example) and use `IP` as the counting characteristic. Similarly, to the [/login example](/docs/cis?topic=cis-rate-limit-best&interface=cli#protect-against-credentials), the two rules help reduce false positives in case of persistent (but legitimate) visitors.

You can limit the lookup of a specific `product_id` by using a query string parameter. By adding a query parameter as a counting characteristic, the rate is calculated across all requests, regardless of the client.

The following example limits the number of lookups for each `product_id` to 50 requests in 10 seconds.

| Setting | Value |
|----------|-----------------------|
| Matching criteria | URI Path equals `/merchant` |
| Expression | `http.request.uri.path eq "/merchant"` |
| Counting characteristics | Query (`product_id`) |
| Rate (Requests/Period) | 20 requests / 10 seconds |
| Action | Block |
{: caption="Rule limit via query string" caption-side="bottom"}

This example rule requires Advanced Rate Limiting.
{: note}

You might follow the same pattern of rate limiting rules to protect applications handling reservations and bookings.

### Preventing content scraping by using request body
{: #prevent-content-scraping}

Consider an application that handles the operation and its parameters through the request body in JSON format. For example, the `lookup_price` operation might look like the following:

```sh
POST https://api.store.com/merchant
Cookie: session_id=12345

Body:
{
  "action": "lookup_price",
  "product_id": 215
}
```
{: pre}

In this scenario, you can create a following rule to limit the number of actions from individual sessions:

| Setting | Value |
|----------|-----------------------|
| Matching criteria | URI Path equals `/merchant` and JSON String `action` equals `lookup_price` |
| Expression | `http.request.uri.path eq "/merchant" and lookup_json_string(http.request.body.raw, "action") eq "lookup_price"` |
| Counting characteristics | Cookie (`session_id`) |
| Rate (Requests/Period) | 10 requests / 2 minutes |
| Action | Managed Challenge |
{: caption="Rule—Limit lookup actions per session" caption-side="bottom"}

This example rule requires Advanced Rate Limiting and payload inspection.
{: note}

You can also limit the number of lookups of each `product_id` regardless of the client making the requests by deploying a rule like the following:

| Setting | Value |
|----------|-----------------------|
| Matching criteria | URI Path equals `/merchant` and JSON field `action` equals `lookup_price` |
| Expression | `http.request.uri.path eq "/merchant" and lookup_json_string(http.request.body.raw, "action") eq "lookup_price"` |
| Counting characteristics | JSON field (`product_id`) |
| Rate (Requests/Period) | 50 requests / 10 seconds |
| Action | Block |
{: caption="Rule—Limit lookup requests per product ID" caption-side="bottom"}

This example rule requires Advanced Rate Limiting and payload inspection.


If the request body is not JSON format, you can use the [http.request.body.raw](/docs/cis?topic=cis-custom-rules-fields-and-expressions&interface=ui#custom-rule-available-fields) field and regular expressions (along with the [matches operator](/docs/cis?topic=cis-custom-rules-fields-and-expressions&interface=ui#custom-rule-comparison-operators)) to achieve the same goal.
{: important}

### Limiting requests from bots
{: #limit-request-from-bots}

You can use rate limiting to control automated traffic from bots. A common approach is to monitor requests that return a high number of `403` or `404` response status codes, which often indicate automated scraping activity.

In this situation, you might configure a rule similar to the following:

| Setting |	Value |
| ---------- | ----------------------- |
| Matching criteria | Hostname equals `example.com` |
| Expression | `http.host eq "example.com"` |
| Counting characteristics | IP |
| Increment counter when | Response Status Code is in (401, 403) |
| Counting expression | `http.response.code in {401 403}` |
| Rate (Requests/Period) | 5 requests / 3 minutes |
| Action | Managed Challenge |
{: caption="Rule—Limit requests based on response status codes" caption-side="bottom"}

This example rule requires a Business plan or above.
{: note}

To control the rate of actions performed by automated sources, consider use rate limiting rules together with [Bot Management](/docs/cis?topic=cis-about-bot-mgmt&interface=cli). With Bot Management, you can use the [bot score](/docs/cis?topic=cis-bot-management-fields&interface=cli) as part of the matching criteria to apply the rule only to automated or likely automated traffic. For example, you can use a maximum score (or threshold) of `30` for likely automated traffic and `10` for automated traffic.

You can enhance protection by combining rate limiting with [Bot Management](/docs/cis?topic=cis-about-bot-mgmt&interface=cli). With Bot Management, you can use the [bot score](/docs/cis?topic=cis-bot-management-fields&interface=cli) as part of the matching criteria to apply the rule only to automated or likely automated traffic.

For example:

* A bot score lesser than `30` represents likely automated traffic.
* A bot score lesser than `10` represents confirmed automated traffic.

#### Limiting requests per session
{: #limiti-request-per-session}

If your application uses session cookies, use the cookie as the counting characteristic.
This method groups requests from different IPs within the same session—useful for detecting distributed bot attacks.

Rule 1

| Setting | Value |
|----------|-----------------------|
| Matching criteria | Bot Score less than 30 and URI Query String contains `action=delete` |
| Expression | `cis.bot_management.score lt 30 and http.request.uri.query contains "action=delete"` |
| Counting characteristics | Cookie (`session_id`) |
| Rate (Requests/Period) | 10 requests / 1 minute |
| Action | Managed Challenge |
{: caption="Limit request for bot score less than 30" caption-side="bottom"}

Rule 2

| Setting | Value |
|----------|-----------------------|
| Matching criteria | Bot Score less than 10 and URI Query String contains `action=delete` |
| Expression | `cis.bot_management.score lt 10 and http.request.uri.query contains "action=delete"` |
| Counting characteristics | Cookie (`session_id`) |
| Rate (Requests/Period) | 20 requests / 5 minutes |
| Action | Block |
{: caption="Limit request for bot score less than 10" caption-side="bottom"}

These example rules require Advanced Rate Limiting and Bot Management.
{: note}

#### Using JA3 fingerprints
{: #ja3-fingerprint}

If the application does not use a session cookie, you can use JA3 fingerprints to identify individual clients. A [JA3 fingerprint](/docs/cis?topic=cis-custom-rules-fields-and-expressions&interface=ui#bot-management-fields) is a unique identifier, available to customers with [Bot Management](/docs/cis?topic=cis-about-bot-mgmt&interface=cli), that allows CIS to identify requests coming from the same client. All clients have an associated fingerprint, whether they are automated or not.

| Setting | Value |
|----------|-----------------------|
| Matching criteria | URI Path equals `/merchant` and Bot Score less than 10 |
| Expression | `http.request.uri.path eq "/merchant" and cf.bot_management.score lt 10` |
| Counting characteristics | JA3 Fingerprint |
| Rate (Requests/Period) | 10 requests / 1 minute |
| Action | Managed Challenge |
{: caption="Limit request by using JA3 Fingerprint" caption-side="bottom"}

This example rule requires Advanced Rate Limiting and Bot Management.
{: note}

## Protecting REST APIs
{: #protect-rest-api}

REST APIs can create high load on backend systems because API requests often require intensive processing or large data lookups. Uncontrolled API access can cause performance degradation or even downtime.
Use Advanced Rate Limiting to prevent abuse, mitigate volumetric attacks, and protect critical resources.

### Protecting resources
{: #protect-resource}

Even `GET` requests can strain the application or consume bandwidth when used for large data downloads, such as files or images.

For instance, consider the following endpoint:

```sh
GET https://api.store.com/files/<FILE_ID>
Header: x-api-key=9375
```
{: pre}

To prevent abuse while allowing legitimate downloads, you can define a rule that limits file requests without writing separate rules for each file.

| Setting | Value |
|----------|-----------------------|
| Matching criteria | Hostname equals `api.example.com` and Request Method equals `GET` |
| Expression | `http.host eq "api.example.com" and http.request.method eq "GET"` |
| Counting characteristics | Path |
| Rate (Requests/Period) | As suggested by API Discovery or assessed by analyzing past traffic. |
| Action | Block |
{: caption="Rule — Limit file downloads by path" caption-side="bottom"}

This example rule requires Advanced Rate Limiting.
{: note}

This rule limits downloads to 10 requests per 10 minutes per file under `https://api.store.com/files/*`. By using Path as the counting characteristic, you can avoid creating new rules for every new `<FILE_ID>`. The rate is calculated per file, regardless of client IP or session ID.

You can further strengthen protection by combining `Path` with a client identifier such as `x-api-key` or `IP`. This approach allows you to restrict the number of downloads a specific client can make for a given file.

| Setting | Value |
|----------|-----------------------|
| Matching criteria | Hostname equals `api.store.com` and Request Method equals `GET` |
| Expression | `http.host eq "api.example.com" and http.request.method eq "GET"` |
| Counting characteristics | Path and Header (`x-api-key`) |
| Rate (Requests/Period) | As suggested by API Discovery or assessed by analyzing past traffic. |
| Action | Block |
{: caption="Rule — Limit file downloads by path and header" caption-side="bottom"}

This example rule requires Advanced Rate Limiting.
{: note}

## Protecting GraphQL APIs
{: #protect-grapgql-api}

Preventing server overload for GraphQL APIs can be different from preventing overload for RESTful APIs. One of the biggest challenges that are posed by applications that are built on GraphQL is that a single path manages all queries to the server, and every request is usually a `POST` operation. This prevents creating different rate limits for different API based on the HTTP method and URI path.

However, instead of using the method and path like a RESTful API, the purpose of the request is usually embedded in the body, which has information on what data the client wants to fetch or mutate (according to [GraphQL's terminology](https://graphql.org/learn/queries/){: external} for server-side data modification), along with any additional data that is required to carry out the action.


To prevent server overload, consider the following approaches:

* Limit the number of times a particular user can call the same GraphQL operation name.
* Limit the total amount of query complexity any given user is allowed to request.
* Limit any individual request's query complexity.

The following examples are based on an application that accepts reviews for movies.

```sh
POST https://moviereviews.example.com/graphql
Cookie: session_id=12345

Body:
{
  "data": {
    "createReview": {
      "stars": 5,
      "commentary": "This is a great movie!"
    }
  }
}
```
{: pre}

### Limiting the number of operations
{: #limit-number-operations}

To limit the rate of actions, create the following rule:

| Setting | Value |
|----------|-----------------------|
| Matching criteria | URI Path equals `/graphql` and Body contains `createReview` |
| Expression | `http.request.uri.path eq "/graphql" and http.request.body.raw contains "createReview"` |
| Counting characteristics | Cookie (`session_id`) |
| Rate (Requests/Period) | 5 requests / 1 hour |
| Action | Block |
{: caption="Limit the number of operations" caption-side="bottom"}

This example rule requires Advanced Rate Limiting and payload inspection.
{: note}

### Limiting the total amount of query complexity
{: #limit-total-amount-query}

The complexity of handling a GraphQL request can vary significantly. Because the API uses a single endpoint, it can be difficult to determine the complexity of each request before it is processed.

To prevent resource exhaustion on the origin server, limit the total request complexity per client over time, rather than limiting the number of requests. CIS Rate Limiting enables you to create rules that track complexity over time and block requests that exceed a defined complexity budget.

This method requires the origin server to assign a complexity score to each request and include that score in the HTTP response header. The rate-limiting mechanism then uses the score information to update the complexity budget for that specific client.

The following example defines a total complexity budget of 1,000 per hour:

| Setting | Value |
|----------|-----------------------|
| Matching criteria | URI Path contains `/graphql` |
| Expression | `http.request.uri.path eq "/graphql"` |
| Counting characteristics | Cookie (`session_id`) |
| Score per period | 1,000 |
| Period | 1 hour |
| Response header name | `score` |
| Action | Block |
{: caption="Limit the total amount of query complexity" caption-side="bottom"}

This example rule requires Advanced Rate Limiting and payload inspection.
{: note}

When the origin server processes a request, it adds a `score` HTTP header to the response with a value which indicates how much work the origin has performed to handle it. For example, `100`. In the next hour, the same client can perform requests up to an additional budget of `900`. As soon as this budget is exceeded, later requests are blocked until the timeout expires.

### Limiting any individual query’s complexity
{: #limit-any-individual-query}

API Shield customers can use GraphQL malicious query protection to protect their GraphQL APIs. This feature scans incoming GraphQL traffic for queries that might overload the origin server and cause a denial-of-service condition.

You can create rules to limit the depth and size of incoming GraphQL queries. These rules help block suspicious or excessively complex queries before they impact performance.
