---

copyright:
  years: 2026
lastupdated: "2026-04-24"

keywords:

subcollection: cis

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I seeing Too Many Requests in Terraform plan?
{: #ts-too-many-request-tf}
{: troubleshoot}

When you use Terraform to manage CIS, you might encounter the error **Too Many Requests (429)** during `terraform plan` or `terraform apply`. These errors occur when API request rates exceed the supported limits, which can happen in environments with multiple resources, repeated operations, or when requests are issued in quick succession. Because Terraform can perform concurrent operations and retry failed requests, the total number of API calls can increase rapidly, leading to rate limiting and potentially causing deployments to fail or become unreliable.
{: shortdesc}

During Terraform operations, CIS API requests can fail with this error: **Too Many Requests (429)**
{: tsSymptoms}

This error can occur repeatedly, typically when you manage CIS resources, such as:

* `ibm_cis_firewall_rules`
* `ibm_cis_mtls_app`

The issue can persist even when Terraform parallelism is reduced and might block deployments.

This issue is caused by exceeding CIS API rate limits.
{: tsCauses}

* CIS enforces a default API rate limit (for example, approximately 1,200 requests per 5 minutes per user).
* Terraform runs operations in parallel by default, which can generate a high number of API requests in a short time.
* Even with reduced parallelism, the following factors can still trigger rate limiting:
   * A large number of CIS resources in a single deployment
   * Repeated retries of failed API calls by Terraform
   * Use of a single technical user for all API operations

Because CIS does not currently show configurable throttling or backoff controls for Terraform, request bursts can exceed the allowed limits.

Use the following resolutions to reduce the number of API requests and minimize the likelihood of encountering rate limiting during Terraform operations with CIS.
{: tsResolve}

1. Reduce Terraform parallelism. 

   Terraform runs up to 10 operations concurrently by default. Lowering this value reduces the number of simultaneous API calls. Run Terraform with reduced parallelism: `terraform apply -parallelism=2` or `terraform apply -parallelism=1`

   Lowering parallelism reduces the number of simultaneous API requests and can help prevent rate limiting.

1. Check CIS API rate limits. When you use Terraform with CIS APIs, API requests are subject to rate limits (for example, approximately 1,200 requests per 5 minutes per user). If Terraform attempts to create or modify many resources in a short period, these limits can be exceeded.

   Review your deployment size and frequency to ensure that the total number of API requests stays within supported limits.

1. Check for repeated API retries. Terraform might retry failed API requests, which can increase the total number of requests and contribute to rate limiting.

   You can enable debug logging to investigate request behavior: `TF_LOG=DEBUG terraform apply`

   Review the logs for repeated API calls, such as:
   * `GET`
   * `POST`
   * `PATCH`
   * `PUT`

   Frequent or repeated requests can indicate retry activity that is contributing to the issue.

1. Contact support if the issue persists. If the issue continues after applying these steps, contact IBM Support.

   Provide the following information to assist with troubleshooting:

   * Approximate number of resources being created or updated
   * Sample Terraform configuration (if available)
   * Estimated number of API requests being sent
   * Relevant Terraform debug logs 
