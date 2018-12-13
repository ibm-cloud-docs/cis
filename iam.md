---
copyright:
  years: 2018
lastupdated: "2018-12-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# IAM and CIS

IBM Cloud Internet Services (CIS) leverages IAM to perform authorization and Authentication.

If you do not wish to add anyone to your CIS instance, you may disregard this page.
{:note}

Restrict access by three CIS Functional Scopes, based on the navigation tree: 
* reliability - such as DNS, GLB
* security - such as Certificate, IP Firewall rules and rate limiting
* performance - such as Page rules, caching and routing

This section walks through how to provide fine-grained access control of your instance.

## Roles

Use the following three roles to leverage IAM
* Reader - Able to get information about instance and domain
* Writer - Able to make changes to the existing configuration
* Manager - Able to create or delete instances, domains, configuration

## Access groups and users

A policy can be assigned to a User directly or to an Access Group.
We recommend assigning it to an access group to minimize the number of policies created and to reduce the effort of managing these policies.

## Cache

We cache the authorization results and use the cache to make a decision when the same request arrives again. After the cache reaches its time to live ( 10 min), it expires.

## Best Practices

1. Instead of modifying a policy, delete the existing policy and then create a new one.

## Scenarios
This section walks through the different examples of access policies created through CIS. 

### Domain level with `config` type

#### Access to single domain with `security config` on an Access Group
##### Writer role

Bob has a CIS instance, `cis-test-instance`, and two domains, `bob.com` and `bob-ibm.com`.
Bob wants to provide all security engineers (sec-group) in the company access to the Writer role on only the **security configuration** of **`bob.com`**.

These steps show how to create an IAM policy to make this scenario possible.

After Bob logs into cis-test-instance, he:
1. Clicks on **Account > Access** tab in the nav bar
1. Selects the **access group** - **sec-group** you want to provide access
1. Selects **`bob.com`**
1. Selects **Writer** role
1. Selects the **Security config** option
1. Clicks **create policy**

On the Manage Tab:
The following policies are created for **sec-group**:

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e

Service Instance 
    name: cis-test-instance  
    id: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9 
Domain 
    name: bob.com
    id: 4b23ec772965f672f96f05670e36827e 
Config Type
    cfgType: security
```

Now sec-group has access to see only `bob.com`, and can modify values pertaining to security. 

##### Update from Writer to Manager role for an access group

If Bob wants to update the role of sec-group from Writer to Manager, he needs to delete the existing policy. 
1. Go to **Manage IAM tab > Access groups > sec-group > access policies**
1. Delete the following Policy 
  ```
  Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
  ```

Then, Bob has to create the new policy. 
1. Click on **Account > Access** tab in the nav bar
1. Select the **access group** - **sec-group** you want to provide access
1. Select **`bob.com`**
1. Select **Manager** role
1. Select the **Security config** option
1. Click **create policy**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

If the existing policy (writer) is not deleted, then attempting to create policy for Manager fails.

##### Update the configuration to include Performance along with Security

If Bob wants to give Manager sec-group access to performance configuration on `bob.com` along with security, he:
1. Clicks on **Account > Access** tab in the nav bar
1. Selects the **access group** - **sec-group** you want to provide access
1. Selects **`bob.com`**
1. Selects **Manager** role
1. Selects the **Performance config** option
1. Clicks **create policy**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: performance, domainId: 4b23ec772965f672f96f05670e36827e

```

#### Access to all domains with `security config`

If you want to provide security actions for `bob.com` and `bob-ibm.com` from the previous example, you must create a new policy by repeating the steps for each domain. The only difference is selecting the respective domain for each policy.

1. Click on **Account > Access** tab in the nav bar
1. Select the **access group** - **sec-group** you want to provide access
1. Select **`bob.com`**
1. Select **Manager** role
1. Select the **Security config** option
1. Click **create policy**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

1. Click on **Account > Access** tab in the nav bar
1. Select the **access group** - **sec-group** you want to provide access
1. Select **`bob-ibm.com`**
1. Select **Manager** role
1. Select the **Security config** option
1. Click **create policy**

```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 7ad7341865246f5df482ad9f76aafb5a
```



#### Access to single domain with `security config` and `reliability config`

Bob has a CIS instance cis-test-instance, and 2 domains, `bob.com` and `bob-ibm.com`.
Bob wants to provide Tony access to Writer role for only the **security and reliability actions** of **`bob-ibm.com`**.

After Bob logs into cis-test-instance, he:
1. Clicks on **Account > Access** tab in the nav bar
1. Selects **Tony** to whom he wants to provide access
1. Selects **`bob-ibm.com`**
1. Selects **Writer** role
1. Selects the checkbox for **Security and reliability** option 
1. Clicks **create policy**

This creates two policies on the backend for each config type.

### Domain level with all config types

Bob wants to grant read/write/mange at a the domain level to Tony.

#### Write
After Bob logs into cis-test-instance, he:
1. Clicks on **Account > Access** tab in the nav bar
1. Selects **Tony** to whom he wants to provide access
1. Selects **`bob.com`**
1. Selects **Writer** role
1. Check all boxes for CIS Functional Scope
1. Clicks **create policy**

```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### Manager
After Bob logs into cis-test-instance, he:
1. Clicks on **Account > Access** tab in the nav bar
1. Selects **Tony** to whom he wants to provide access
1. Selects **`bob.com`**
1. Selects **Manager** role
1. Check all boxes for CIS Functional Scope
1. Clicks **create policy**

```
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Manager	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

#### Reader
After Bob logs into cis-test-instance, they:
1. Click on **Account > Access** tab in the nav bar
1. Selects **Tony** to whom he wants to provide access
1. Select **`bob.com`**
1. Select **Reader** Role
  1. All check boxes are pre-ticked to show that the user needs *min* read access to the whole domain, and cannot give partial access to a domain
1. Click **create policy**


```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Viewer	Resource	Only service instance cis-test-instance of CIS 	
```

### Instance level - all your domains

This policy must be created and managed through the IAM manage page.

Instance level access means that Bob can give Tony permission to Instance 1 out of the 10 instances present.
Tony is able to view all the domains in this instance. 

If Bob wants to give Writer or Manager to access the following, he needs to give instance level access:
* Load balancer - pools and healthchecks
* Firewall access rules
* Workers 

In the manage IAM page, create a writer/manger policy on the service instance cis-test-instance.

```
Manager	Resource	Only service instance cis-test-instance of CIS 	
or
Writer	Resource	Only service instance cis-test-instance of CIS 	
```

## Manage IAM policies 

CIS allows users to create IAM policies, but management must be done through the [IAM Page](
https://cloud.ibm.com/iam#/overview).

## Note
For every policy created on the Access page in the CIS instance, 2-3 policies will be created in turn.

1. The service instance Platform viewer role allows the added user to view the instance on the dashboard.

**Example**
```
Viewer	Resource	Only service instance cis-instance-instance of CIS 	
```

2. The domain level read access is the min requirement for fine grained access to work.

**Example**
```
Reader	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
```
3. The policy you created with config type present.

**Example**
```
Writer	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

FAQ
1. How do I get my service instance ID?

   Copy the CRN on the overview page
   ```
   crn:v1:bluemix:public:internet-svcs:global:a/2c38d9a9913332006a27665dab3d26e8:836f33a5-d3e1-4bc6-876a-982a8668b1bb::
   ```
   The last part of the CRN is your service instance: `836f33a5-d3e1-4bc6-876a-982a8668b1bb`.
   
   or
   
   Click the row containing the CIS instance on the resource list main page and copy the GUID for the service instance ID.

2. I deleted a policy but the user I gave the policy to can still perform that action!

   CIS caches authorization results, and the TTL for the cache is 10 minutes.  
   
   When IAM authorizes, it uses the access policies from the access group and the user's own policies before making a decision.

3. What permissions are needed to provision Internet Services?

   If you are unable to create a resource and add it to a resource group, you're most likely dealing with an access issue. You must have at least the Viewer role on the resource group itself and at least the Editor role on the service in the account. You can contact the account administrator to verify your assigned access in the account. See [Managing access to resources](https://cloud.ibm.com/docs/iam/mngiam.html#assignaccess) for more information.
   
 
