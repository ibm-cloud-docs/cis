---

copyright:
  years: 2021, 2026
lastupdated: "2026-01-16"

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Setting up Terraform for {{site.data.keyword.cis_short_notm}}
{: #terraform-setup-cis}

Terraform on {{site.data.keyword.cloud}} enables predictable and consistent creation of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multi-tier cloud environments following Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the creation, update, and deletion of your {{site.data.keyword.cis_full_notm}} instances by using HashiCorp Configuration Language (HCL).
{: shortdesc}

Looking for a managed Terraform on {{site.data.keyword.cloud}} solution? Try out [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't have to worry about setting up and maintaining the Terraform command line and the {{site.data.keyword.cloud}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can easily install from the {{site.data.keyword.cloud}} catalog.
{: tip}

## Installing Terraform and configuring resources for {{site.data.keyword.cis_full_notm}}
{: #install-terraform}

Before creating an authorization by using Terraform, complete the following prerequisites:

* Make sure that you have the [required access](/docs/cis?topic=cis-at_iam_CIS) to create and work with {{site.data.keyword.cis_full_notm}}.
* Install the Terraform CLI and configure the IBM Cloud Provider plug-in for Terraform. For more information, see [Getting started with Terraform on IBM Cloud](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started). The plug-in abstracts the IBM Cloud APIs that are used to complete this task.
* Create a Terraform configuration file named `main.tf`. Use this file to define the authorization between services by writing Terraform code in HashiCorp Configuration Language (HCL). For more information, see the [Terraform documentation](https://developer.hashicorp.com/terraform/language){: external}.

1. In your Terraform configuration file, find the Terraform code that you used to create the CIS instance.
1. Create a {{site.data.keyword.cis_short_notm}} instance by using the `ibm_resource_instance` resource argument in your `main.tf` file. The {{site.data.keyword.cis_short_notm}} instance in the following example is named `test` and is created with the Standard pricing plan. The `resource_group_id` is `data.ibm_resource_group.group.id`, and the location property is set to `global`.
   ```terraform
   data "ibm_resource_group" "group" {
     name = "test"
   }

   resource "ibm_cis" "cis_instance" {
     name              = "test"
     plan              = "standard-next"
     resource_group_id = data.ibm_resource_group.group.id
     tags              = ["tag1", "tag2"]
     location          = "global"

     //User can increase timeouts
     timeouts {
       create = "15m"
       update = "15m"
       delete = "15m"
     }
   }
   ```
   {: codeblock}

   If you don't specify the `resource_group_id`, the CIS instance is created in the default resource group. The `API_KEY` must have permissions for this group.

   If you migrate from one plan to another, the change is considered a modification of an existing resource. It isn't considered as a resource creation or deletion.
   {: important}

1. After you finish building your configuration file, initialize the Terraform CLI. For more information, see [Initialize the Working Directory](https://developer.hashicorp.com/terraform/cli/init){: external}.

   ```terraform
   terraform init
   ```
   {: pre}

1. Provision the resources from the `main.tf` file. For more information, see [Terraform workflow for provisioning infrastructure](https://developer.hashicorp.com/terraform/cli/run){: external}.

   1. Run `terraform plan` to generate a Terraform execution plan to preview the proposed actions.

      ```terraform
      terraform plan
      ```
      {: pre}

   1. Run `terraform apply` to create the resources that are defined in the plan.

      ```terraform
      terraform apply
      ```
      {: pre}

1. From the [{{site.data.keyword.cloud_notm}} resource list](/resources){: external}, select the {{site.data.keyword.cis_short_notm}} instance that you created and note the instance ID.
1. Verify that the access policy is successfully assigned. For more information, see [Reviewing assigned access in the console](/docs/account?topic=account-assign-access-resources&interface=ui#review-your-access-console).

## What's next?
{: #terraform-setup-next}

Now that you successfully created your first {{site.data.keyword.cis_short_notm}} service instance with Terraform on {{site.data.keyword.cloud_notm}}, you can visit the CIS [{{site.data.keyword.cis_short}} Terraform registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis){: external} to perform additional tasks using Terraform.
