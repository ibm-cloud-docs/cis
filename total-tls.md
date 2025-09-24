---

copyright:
  years: 2025
lastupdated: "2025-09-24"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Creating Total TLS
{: #using-total-tls}
{: api}

Total TLS allows CIS to issue individual certificates for your proxied hostnames. These certificates protect the proxied hostnames not covered by [Universal certificates](/docs/cis?topic=cis-managing-edge-certs#universal-certificate-type).
{: shortdesc}

Total TLS certificates follow the Common Name (CN) restriction of 64 characters [`(RFC 5280)`](https://www.rfc-editor.org/rfc/rfc5280.html){: external}. If you have a hostname that exceeds this length, you can create an [Advanced Certificate](/docs/cis?topic=cis-managing-edge-certs#advanced-certificate-type) through API to cover it.
{: important}

The issued certificates have a type of **Advanced - Total TLS**, and their default validity period is 90 days.

## Getting the Total TLS for API
{: #get-total-ttls}

Follow these steps to get the Total TLS:
1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.
1. When all variables are initiated, get the Total TLS:

   ```sh
   curl --request GET \
     --url https://api.cis.cloud.ibm.com/v1/{CRN}/zones/{ZONE_ID}/acm/total_tls \
     --header 'Content-Type: application/json' \
     --header 'X-AUTH-USER-TOKEN: REDACTED'
   ```
   {: pre}

## Changing the Total TLS with API
{: #create-ttls}

Follow these steps to create the Total TLS:

1. Set up your API environment with the correct variables.
1. Store the following values in variables to be used in the API command:

   `CRN`: The full URL-encoded Cloud Resource Name (CRN) of the service instance.

   `ZONE_ID`: The domain ID.
1. When all variables are initiated, create the Total TLS:

   ```sh
   curl --request POST \
     --url https://api.cis.cloud.ibm.com/v1/{CRN}/zones/{ZONE_ID}/acm/total_tls \
     --header 'Content-Type: application/json' \
     --header 'X-AUTH-USER-TOKEN: REDACTED' \
     --data '{
         "enabled": true,
         "certificate_authority": "google"
     }'
   ```
   {: pre}

   To enable Total TLS with the API, send a `POST` request with the `enabled` parameter set to either `true` or `false`.
   You can also specify a certificate authority by providing a value for the `certificate_authority` parameter.

## Limitations
{: #limitation-ttls}

Total TLS has the following limitations:

* Total TLS doesn't issue certificates for any hostnames that are used with:
   - [Global load balancers](/docs/cis?group=working-with-global-load-balancers)
   - [Range applications](/docs/cis?group=range)
* Total TLS is not supported for [partial CNAME setup](/docs/cis?topic=cis-cname-setup).

You can use other types of certificates or manually [order advanced certificates](/docs/cis?topic=cis-managing-edge-certs) for these hostnames.

## Deleting certificates
{: #ttls-delete}

After [Total TLS is enabled](/docs/cis?topic=cis-using-total-tls&interface=api#create-ttls), be cautious when deleting Total TLS-managed certificates associated with proxied hostnames. Doing so signals that the hostname should be excluded from future Total TLS issuance. The system will not automatically provision new certificates for that hostname, even if its DNS record is deleted and re-created later.
