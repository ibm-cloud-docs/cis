---

copyright:
  years: 2024, 2024
lastupdated: "2024-07-17"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Generating configurations with Terraform
{: #terraform-generating-configuration}

Terraform can generate code for the resources you define in `import` blocks that do not already exist in your configuration.

[Experimental]{: tag-green} Configuration generation is available in Terraform v1.5 as an [experimental feature](https://developer.hashicorp.com/terraform/language/import/generating-configuration){: external}.

To generate a configuration with Terraform, perform the following procedure:

1. Add the `import` block:

    ```sh
    import {
      to = ibm_cis_ruleset.test
      id = "dcdec3fe0cbe41edac08619503da8de5:601b728b86e630c744c81740f72570c3:crn:v1:staging:public:internet-svcs-ci:global:a/01652b251c3ae2787110a995d8db0135:1a9174b6-0106-417a-844b-c8eb43a72f63::"
    }
    ```
    {: codeblock}

    Where:
    * `to`: Points to the address a resource will have in your state file. In this example, the resource module is followed by the resource name that is being added.
    * `id`: Can be a literal string of your resource's import ID, or an expression that evaluates to a string. In this example, the domain ID and the CRN are separated by a colon. See the [CIS Terraform import example](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/cis_tls_settings#import){: external}.

1. Plan and generate the configuration:

    ```txt
    $ terraform plan -generate-config-out=generated.tf
    ibm_cis_ruleset.test: Preparing import... [id=dcdec3fe0cbe41edac08619503da8de5:601b728b86e630c744c81740f72570c3:crn:v1:staging:public:internet-svcs-ci:global:a/01652b251c3ae2787110a995d8db0135:1a9174b6-0106-417a-844b-c8eb43a72f63::]
    ibm_cis_ruleset.test: Refreshing state... [id=dcdec3fe0cbe41edac08619503da8de5:601b728b86e630c744c81740f72570c3:crn:v1:staging:public:internet-svcs-ci:global:a/01652b251c3ae2787110a995d8db0135:1a9174b6-0106-417a-844b-c8eb43a72f63::]

    Terraform will perform the following actions:

      # ibm_cis_ruleset.test will be imported
      # (config will be generated)
        resource "ibm_cis_ruleset" "test" {
            cis_id     = "crn:v1:staging:public:internet-svcs-ci:global:a/01652b251c3ae2787110a995d8db0135:1a9174b6-0106-417a-844b-c8eb43a72f63::"
            domain_id  = "601b728b86e630c744c81740f72570c3"
            id         = "dcdec3fe0cbe41edac08619503da8de5"
            ruleset_id = "dcdec3fe0cbe41edac08619503da8de5"

            rulesets_obj {
                description  = "Updating a zone ruleset"
                kind         = "zone"
                last_updated = "2024-04-29T06:04:06.58962Z"
                name         = "default"
                phase        = "http_request_firewall_managed"
                version      = "2"

                rules {
                    categories           = []
                    description          = "deploying a managed rule"
                    enabled              = true
                    expression           = "ip.src ne 1.1.1.2"
                    id                   = "7787447241554207a18404a1b020fe50"
                    rule_action          = "execute"
                    rule_last_updated_at = "2024-04-29T06:04:06.58962Z"
                    rule_logging         = {}
                    rule_ref             = "efb7b8c949ac4650a09736fc376e9aee"
                    rule_version         = "1"

                    action_parameters {
                        id       = "efb7b8c949ac4650a09736fc376e9aee"
                        rulesets = []
                        version  = "latest"

                        overrides {
                            action  = "block"
                            enabled = true

                            categories {
                                action   = "block"
                                category = "wordpress"
                                enabled  = true
                            }

                            rules {
                                action     = "block"
                                enabled    = true
                                ruleset_id = "5de7edfa648c4d6891dc3e7f84534ffa"
                            }
                        }
                    }
                }
            }
        }

    Plan: 1 to import, 0 to add, 0 to change, 0 to destroy.
    ╷
    │ Warning: Config generation is experimental
    │
    │ Generating configuration during import is currently experimental, and the generated configuration format may change in future versions.
    ╵

    ─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

    Terraform has generated configuration and written it to generated.tf. Please review the configuration and edit it as necessary before adding it to version control.

    Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
    ```
    {: screen}

    * Use the command `terraform plan -generate-config-out=generated.tf` to generate the resource configurations. These configurations are added to the `generated.tf` file.

1. Apply the configuration:

    ```txt
    $ terraform apply
    ibm_cis_ruleset.test: Preparing import... [id=dcdec3fe0cbe41edac08619503da8de5:601b728b86e630c744c81740f72570c3:crn:v1:staging:public:internet-svcs-ci:global:a/01652b251c3ae2787110a995d8db0135:1a9174b6-0106-417a-844b-c8eb43a72f63::]
    ibm_cis_ruleset.test: Refreshing state... [id=dcdec3fe0cbe41edac08619503da8de5:601b728b86e630c744c81740f72570c3:crn:v1:staging:public:internet-svcs-ci:global:a/01652b251c3ae2787110a995d8db0135:1a9174b6-0106-417a-844b-c8eb43a72f63::]

    Terraform will perform the following actions:

      # ibm_cis_ruleset.test will be imported
        resource "ibm_cis_ruleset" "test" {
            cis_id     = "crn:v1:staging:public:internet-svcs-ci:global:a/01652b251c3ae2787110a995d8db0135:1a9174b6-0106-417a-844b-c8eb43a72f63::"
            domain_id  = "601b728b86e630c744c81740f72570c3"
            id         = "dcdec3fe0cbe41edac08619503da8de5"
            ruleset_id = "dcdec3fe0cbe41edac08619503da8de5"

            rulesets_obj {
                description  = "Updating a zone ruleset"
                kind         = "zone"
                last_updated = "2024-04-29T06:04:06.58962Z"
                name         = "default"
                phase        = "http_request_firewall_managed"
                version      = "2"

                rules {
                    categories           = []
                    description          = "deploying a managed rule"
                    enabled              = true
                    expression           = "ip.src ne 1.1.1.2"
                    id                   = "7787447241554207a18404a1b020fe50"
                    rule_action          = "execute"
                    rule_last_updated_at = "2024-04-29T06:04:06.58962Z"
                    rule_logging         = {}
                    rule_ref             = "efb7b8c949ac4650a09736fc376e9aee"
                    rule_version         = "1"

                    action_parameters {
                        id       = "efb7b8c949ac4650a09736fc376e9aee"
                        rulesets = []
                        version  = "latest"

                        overrides {
                            action  = "block"
                            enabled = true

                            categories {
                                action   = "block"
                                category = "wordpress"
                                enabled  = true
                            }

                            rules {
                                action     = "block"
                                enabled    = true
                                ruleset_id = "5de7edfa648c4d6891dc3e7f84534ffa"
                            }
                        }
                    }
                }
            }
        }

    Plan: 1 to import, 0 to add, 0 to change, 0 to destroy.

    Do you want to perform these actions?
      Terraform will perform the actions described above.
      Only 'yes' will be accepted to approve.

      Enter a value: yes

    ibm_cis_ruleset.test: Importing... [id=dcdec3fe0cbe41edac08619503da8de5:601b728b86e630c744c81740f72570c3:crn:v1:staging:public:internet-svcs-ci:global:a/01652b251c3ae2787110a995d8db0135:1a9174b6-0106-417a-844b-c8eb43a72f63::]
    ibm_cis_ruleset.test: Import complete [id=dcdec3fe0cbe41edac08619503da8de5:601b728b86e630c744c81740f72570c3:crn:v1:staging:public:internet-svcs-ci:global:a/01652b251c3ae2787110a995d8db0135:1a9174b6-0106-417a-844b-c8eb43a72f63::]

    Apply complete! Resources: 1 imported, 0 added, 0 changed, 0 destroyed.
    ```
    {: screen}

1. Review the generated file, which should look like the following example:

    ```txt
    # __generated__ by Terraform
    # Please review these resources and move them into your main configuration files.

    # __generated__ by Terraform from "dcdec3fe0cbe41edac08619503da8de5:601b728b86e630c744c81740f72570c3:crn:v1:staging:public:internet-svcs-ci:global:a/01652b251c3ae2787110a995d8db0135:1a9174b6-0106-417a-844b-c8eb43a72f63::"
    resource "ibm_cis_ruleset" "test" {
      cis_id     = "crn:v1:staging:public:internet-svcs-ci:global:a/01652b251c3ae2787110a995d8db0135:1a9174b6-0106-417a-844b-c8eb43a72f63::"
      domain_id  = "601b728b86e630c744c81740f72570c3"
      ruleset_id = "dcdec3fe0cbe41edac08619503da8de5"
      rulesets_obj {
        description  = "Updating a zone ruleset"
        kind         = "zone"
        last_updated = "2024-04-29T06:04:06.58962Z"
        name         = "default"
        phase        = "http_request_firewall_managed"
        ruleset_id   = null
        version      = "2"
        rules {
          categories           = []
          description          = "deploying a managed rule"
          enabled              = true
          expression           = "ip.src ne 1.1.1.2"
          id                   = "7787447241554207a18404a1b020fe50"
          rule_action          = "execute"
          rule_last_updated_at = "2024-04-29T06:04:06.58962Z"
          rule_logging         = {}
          rule_ref             = "efb7b8c949ac4650a09736fc376e9aee"
          rule_version         = "1"
          action_parameters {
            id       = "efb7b8c949ac4650a09736fc376e9aee"
            ruleset  = null
            rulesets = []
            version  = "latest"
            overrides {
              action            = "block"
              enabled           = true
              sensitivity_level = null
              categories {
                action   = "block"
                category = "wordpress"
                enabled  = true
              }
              rules {
                action            = "block"
                enabled           = true
                ruleset_id        = "5de7edfa648c4d6891dc3e7f84534ffa"
                sensitivity_level = null
              }
            }
          }
        }
      }
    }
    ```
    {: screen}
