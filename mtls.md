---

copyright:
  years: 2020, 2025
lastupdated: "2025-07-31"

keywords: mutual tls, mtls, authentication, certificates 

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Using mutual TLS
{: #mtls-features}

Mutual Transport Layer Security (mTLS) authentication ensures that traffic is both secure and trusted in both directions between a client and server. It is only available to customers at any Enterprise plan level.
{: shortdesc}

When mTLS is configured, access is granted only to requests with a corresponding client certificate. When a request reaches your application, CIS responds with a request for the client certificate. If the client fails to present the certificate, the request is not allowed to proceed. Otherwise, the key exchange proceeds.

![Diagram of mTLS handshake](images/mtls-handshake.png "Diagram of mTLS handshake"){: caption="Diagram of an mTLS handshake" caption-side="bottom"}

## Configuring mutual TLS
{: #configure-mtls}

Mutual TLS (mTLS) provides certificate-based client authentication for enhanced security. mTLS is not enabled by default and requires prior authorization on a per-domain basis. To configure mTLS, follow these steps:

1. Request authorization. [Create a support case](/docs/account?topic=account-open-case) to request mTLS enablement for your IBM Cloud account.

   After mTLS is enabled, it can't be disabled.
   {: note} 
   
1. Enable mTLS:

   1. In the CIS console, click **Security**, then select the **Mutual TLS** tab.
   1. Click **Enable**.

1. Upload Root certificates:

   1. In the **Root certificates** table on the **Mutual TLS** page, click **Add** to define a new root certificate.
   1. Paste the certificate content into the Certificate content field. Provide a name for the Root CA certificate, and add one or more fully qualified domain names (FQDNs) of the endpoints that will use this certificate.

      These FQDNs are the hostnames that are used by the resources protected by the mTLS application policy. You must associate the Root CA with the FQDN used by the protected application.

   1. Click **Save**. 

      If using an intermediate certificate, upload the entire certificate chain.
      {: note}

1. Create an mTLS access policy:

   1. In the **MTLS access policies** table on the **Mutual TLS** page, click **Create** to create an access application. 
   1. Select or enter a hostname that matches one of the FQDNs associated with the uploaded root certificate and click **Create**.

      The application policy is pre-set to use a decision of `non_identity`, and include a rule that matches any valid client certificate. 

1. Enable client certificate forwarding with the API:

   To forward validated client certificates to your origin server (useful for logging, auditing, or back-end authentication), you must enable forwarding.
   
   The client certificate is forwarded only with the first request in each mTLS connection.
   {: note}

   For an API **curl** example to enable client certificate forwarding, see the [Update access certificates settings](/apidocs/cis#update-access-cert-settings) API.

   Client certificate headers sent to your origin server:

   * `Cf-Client-Cert-Der-Base64`: Base64-encoded DER version of the client certificate
   * `Cf-Client-Cert-Sha256`: SHA-256 fingerprint of the client certificate
   
   To verify forwarding status with the API:
 
   ```sh
   curl -X GET https://api.cis.cloud.ibm.com/v1/crn:v1:bluemix:public:internet-svcs:global:a/<account-id>:<instance-id>::/zones/<zone-id>/access/certificates/settings \
    -H 'X-Auth-User-Token: Bearer <IAM-TOKEN>'
   ```
   {: pre}

1. Create a WAF custom rule to block unauthenticated requests:

   To improve security, especially for sensitive endpoints such as login paths or APIs, create a WAF rule to block requests that do not present a valid client certificate.

   1. In the CIS console, navigate back to the **Security** section, then select the **Custom rules** tab.
   1. Click **Create**.
   1. In the Create WAF custom rule side panel, click **Use Expression Editor**.
   1. Enter the following condition (update `hostname` and `path` as needed) in the **Use Expression Builder** field.

      ```sh
      (http.host eq "example.com" and http.request.uri.path eq "/authenticate" and not cf.tls_client_auth.cert_verified)
      ```
      {: pre}

   1. Set the **Action** to **Block**.
   1. Click **Create**.

   This rule allows access to authenticate only if the client certificate is successfully verified. Requests without mTLS or with invalid certificates are blocked.   
   {: note} 

## Testing mTLS access
{: #test-curl}

The following example uses **curl** to test mTLS authentication by making requests with and without a client certificate.

1. Attempt to access the site without a client certificate.

   This example demonstrates using **curl** to test access to a site that enforces mTLS. The target URL in this example is `https://auth.example.com`.

   ```sh
   curl -sv https://auth.example.com
   ```
   {: pre}

   Because no client certificate is provided, the request is expected to fail with a `403 Forbidden` response.
1. Add your client certificate and private key to the request:

   ```sh
   curl -sv https://auth.example.com --cert example.pem --key key.pem
   ```
   {: pre}

   If the client is properly authenticated, the response includes a `CF_Authorization Set-Cookie` header, indicating successful mTLS authentication.

## Validating mutual TLS
{: #validating-mtls}

When you enable this access policy, use the following workflow to validate client certificates:

All requests to the origin are evaluated for a valid client certificate.
{: note}

1. The client initiates a connection by sending a `Hello` message.
1. The access application responds with a `Hello` and requests the client certificate.
1. The client sends its certificate for validation.
1. The client certificate is authenticated against the configured root certificate authority.
1. If a certificate chain is used, the system also checks for expired certificates and validates the entire chain. 
1. If the client certificate is trusted, a signed JSON Web Token (JWT) is generated for the client that allows the request and subsequent requests to proceed. 
1. If the client doesn't present a valid certificate, the server returns a `403 Forbidden` response.

To retrieve access certificates with the API, see [List access certificates](/apidocs/cis#list-access-certificates).
