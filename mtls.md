---

copyright:
  years: 2020, 2025
lastupdated: "2025-07-24"

keywords:

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

Mutual TLS is not enabled by default. It is an additional service that requires prior authorization and enablement and is enabled per domain.

To obtain authorization, [create a support case](/docs/account?topic=account-open-case).

After mTLS is turned on for your account, take the following steps to enable it.
1. Navigate to the **Security** page in the CIS console.
1. Select the **Mutual TLS** tab.
1. Click **Enable** to enable the feature.

After mTLS is enabled, it can't be disabled.
{: note}

To set up mTLS authentication in the IBM CIS console for a particular endpoint:
1. In the Root certificates table, click **Add** to define a new root certificate.
1. Paste the certificate content into the content field. Provide a name for the Root CA, and add one or more fully qualified domain names (FQDNs) of the endpoints that you want to use this certificate.
   These FQDNs are the hostnames that are used for the resources protected by the application policy. You must associate the Root CA with the FQDN used by the application that is protected.

1. Click **Save**.

   If your zone is using an intermediate certificate in addition to the root certificate, upload the entire chain.
   {: note}

1. In the MTLS access policies table, create a new access application that enforces mTLS authentication. The application must be built with a hostname that was associated in the certificate upload modal. The policy section is pre-set to enforce a decision of `non_identity`, and an `include` rule to match any valid certificate.

## Testing mTLS access using cURL
{: #test-curl}

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

   If the client is properly authenticated, the response will include a CF_Authorization Set-Cookie header, indicating successful mTLS authentication.

## Validating mutual TLS
{: #validating-mtls}

Follow this validation workflow when you enable this access policy:

1. All requests to the origin are evaluated for a valid client certificate.
   The client device sends the client "hello". The access application responds with "hello" and a request for the client certificate.
1. The client returns a valid certificate.
1. Client authentication handshake is completed against the root certificate authority.
1. For chains, a check for expired certificates exists.
   Chain verification is applicable to certificate validation.
1. When the client certificate is trusted by the root certificate, a signed JSON Web Token (JWT) is generated for the client that allows the request and subsequent requests to proceed.
   If a request has no valid client certificate, `403 Forbidden` returns in the response.

To list access certificates with the API, see [List access certificates](/apidocs/cis#list-access-certificates).
