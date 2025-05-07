---

copyright:
  years: 2025
lastupdated: "2025-05-07"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# What do I do if my universal certificate won't progress from pending state?
{: #troubleshooting-universal-certificate}
{: troubleshoot}

You might encounter issues where a Universal Certificate remains in a Pending Validation state, leading to SSL errors.
{: shortdesc}

You encounter SSL errors, such as:
{: tsSymptoms}

* Chrome: `ERR_SSL_VERSION_OR_CIPHER_MISMATCH`
* Firefox: `SSL_ERROR_NO_CYPHER_OVERLAP`
 
To resolve this issue, follow these steps:
{: tsResolve}
 
1. Check the Universal Certificate status:

   1. Log in to IBM Cloud and view your CIS instance.
   1. Navigate to **Security > TLS > Edge certificates**.
   1. Locate the certificate with Type **Universal** and check its status.

      * If the status is **Active**, the certificate is working correctly.
      * If the status is **Pending Validation**, wait for the certificate to be issued.
   
         Activation can take some time. 
         {: note}

1. Validate Certificate Authority Authorization (CAA) records.

   If the certificate remains in **Pending Validation** status, ensure that the CAA records allow CIS to issue the certificate. 
   {: note}

If the issue persists after CAA validation, [contact IBM Support](/docs/cis?topic=cis-gettinghelp) for further troubleshooting.

