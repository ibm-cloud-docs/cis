---

copyright:
  years: 2021
lastupdated: "2021-08-24"

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Setting up Terraform for {{site.data.keyword.cis_short_notm}}
{: #terraform-setup-cis}

Terraform on {{site.data.keyword.cloud}} enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} services so that you can rapidly build complex, multi-tier cloud environments following Infrastructure as Code (IaC) principles. Similar to using the {{site.data.keyword.cloud_notm}} CLI or API and SDKs, you can automate the provisioning, update, and deletion of your {{site.data.keyword.cis_full_notm}} instances by using HashiCorp Configuration Language (HCL).
{: shortdesc}

Looking for a managed Terraform on {{site.data.keyword.cloud}} solution? Try out [{{site.data.keyword.bplong}}](/docs/schematics?topic=schematics-getting-started). With {{site.data.keyword.bpshort}}, you can use the Terraform scripting language that you are familiar with, but you don't have to worry about setting up and maintaining the Terraform command line and the {{site.data.keyword.cloud}} Provider plug-in. {{site.data.keyword.bpshort}} also provides pre-defined Terraform templates that you can easily install from the {{site.data.keyword.cloud}} catalog.
{: tip}

## Installing Terraform and configuring resources for {{site.data.keyword.cis_full_notm}}
{: #install-terraform}

Before you begin, make sure that you have the [required access](/docs/cis?topic=cis-at_iam_CIS) to create and work with {{site.data.keyword.cis_full_notm}} resources. 

1. Follow the [Terraform on {{site.data.keyword.cloud}} getting started tutorial](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started) to install the Terraform CLI and configure the {{site.data.keyword.cloud}} Provider plug-in for Terraform. The plug-in abstracts the {{site.data.keyword.cloud}} APIs that are used to provision, update, or delete {{site.data.keyword.cis_full_notm}} service instances and resources.
2. Create a Terraform configuration file that is named `main.tf`. In this file, you add the configuration to create a {{site.data.keyword.cis_short_notm}} service instance and to assign a user an access policy in Identity and Access Management (IAM) for that instance by using HashiCorp Configuration Language (HCL). For more information, see the [Terraform documentation](https://www.terraform.io/docs/language/index.html){: external}.

   The {{site.data.keyword.cis_short_notm}} instance in the following example is named `test` and is created with the `standard` pricing plan. The `resource_group_id` is `data.ibm_resource_group.group.id`, and the location property is set to `global`.
   
   ```terraform
   data "ibm_resource_group" "group" {
     name = "test"
   }
   
   resource "ibm_cis" "cis_instance" {
     name              = "test"
     plan              = "standard"
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

3. Initialize the Terraform CLI.

   ```terraform
   terraform init
   ```
   {: pre}

4. Create a Terraform execution plan. The Terraform execution plan summarizes all the actions that need to be run to create the {{site.data.keyword.cis_short_notm}} instance in your account.

   ```terraform
   terraform plan
   ```
   {: pre}

5. Create the {{site.data.keyword.cis_short_notm}} instance and IAM access policy in {{site.data.keyword.cloud_notm}}.

   ```terraform
   terraform apply
   ```
   {: pre}

6. From the [{{site.data.keyword.cloud_notm}} resource list](/resources){: external}, select the {{site.data.keyword.cis_short_notm}} instance that you created and note the instance ID.
7. Verify that the access policy is successfully assigned. For more information, see [Reviewing assigned access in the console](/docs/account?topic=account-assign-access-resources#review-your-access-console).

## What's next?
{: #terraform-setup-next}

Now that you successfully created your first {{site.data.keyword.cis_short_notm}} service instance with Terraform on {{site.data.keyword.cloud_notm}}, you can visit the [{{site.data.keyword.cis_short}} Terraform registry](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis){: external} to perform additional tasks using Terraform.

