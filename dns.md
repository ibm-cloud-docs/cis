---

copyright:
  years: 2018, 2025
lastupdated: "2025-05-08"

keywords:

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Setting up your Domain Name System for {{site.data.keyword.cis_short_notm}}
{: #set-up-your-dns-for-cis}

Read some specific instructions about how to configure your {{site.data.keyword.cis_full}} Domain Name System (DNS) records, including how to configure Secure DNS.
{: shortdesc}



## Adding DNS records
{: #adding-dns-records}

You can use the **Type** list menu to select the type of record you want to create. Each DNS record type has a Name and Time-To-Live (TTL) associated with it.

Anything that is entered into the Name field has the domain name appended, unless the domain name is manually appended in the field already. For example, if `www` or `www.example.com` is typed into the field, the API handles both as `www.example.com`. If the exact domain name is typed into the name field, then it isn't appended on itself (for example, `example.com` is handled as `example.com`). However, the list of DNS records shows only the names without the domain name added, so `www.example.com` is shown as `www` and `example.com` is shown as `example.com`. The TTL has a default value of `Automatic`, but can be changed by the user. A proxied DNS record always has a TTL of `Automatic`, so a newly proxied record adopts this configuration during this change.

For records such as A record and CNAME, the automatic TTL is 300s.
{: tip}

### A Type record
{: #a-type-record}

To add this record type, valid values must exist in the **Name** and **IPv4 Address** fields. A **TTL** can also be specified from the list menu, with a default value of `Automatic`.

   Required Fields: Name, IPv4 Address
   Optional Field: TTL (default value is `Automatic`)

### AAAA Type record
{: #aaaa-type-record}

To add this record type, valid values must exist in the **Name** and **IPv6 Address** fields. A **TTL** can also be specified from the list menu, with the default value of `Automatic`.

   Required Fields: Name, IPv6 Address
   Optional Field: TTL (default value is `Automatic`)

### CNAME Type record
{: #cname-type-record}

To add this record type, a valid value must exist in the **Name** field and a fully qualified domain name must be in the **Domain Name** (FQDN) field. A **TTL** can also be specified from the list menu, with the default value of `Automatic`.

   Required Fields: Name, Domain Name (for CNAME)
   Optional Field: TTL (default value is `Automatic`)

Enterprise plans are able to CNAME another domain provided that the domain is configured within {{site.data.keyword.cis_short_notm}}.
{: tip}

```sh
Ex.
Configured CIS Domains:
  - example.com
  - different.com

test.example.com -CNAME-> test.different.com
```
{: pre}

The CNAME flattening feature is enabled by default, and can't be turned off.
{: note}

{{site.data.keyword.cis_short_notm}} does not support Cloudflare's CNAME setup. The only way to activate your domain in {{site.data.keyword.cis_short_notm}} is to delegate your NS Records management to {{site.data.keyword.cis_short_notm}}.
{: important}

### MX Type record
{: #mx-type-record}

To add this record type, a valid value must exist in the **Name** field and a valid address must exist in the **Mail Server** field. A **TTL** can also be specified from the list menu, with the default value of `Automatic`.

* Required Fields: Name, Mail Server
* Optional Fields: TTL (default value is `Automatic`), Priority (default value is 1)

### LOC Type record
{: #loc-type-record}

To add this record type, a valid value must exist in the **Name** field. If you need more specific information, select **Configure LOC options**. A **TTL** can also be specified from the list menu, with the default value of `Automatic`.

* Required Fields: Name
* Optional Fields: LOC options (click **Configure LOC options** to configure)

### CAA Type record
{: #caa-type-record}

To add this record type, valid values must exist in the **Name** and **Value** fields. The Value field correlates to the value of the **Tag** list field, which defaults to "Send violation reports to URL". A **TTL** can can also be specified from the list, with the default value of `Automatic`.

* Required Fields: Name, Value (associated to tag)
* Optional Fields: TTL (default value is `Automatic`), Tag (default is to send violation reports to URL)

### SRV Type record
{: #srv-type-record}

To add this record type, valid values must exist in the **Name**, **Service Name** and **Target** fields. Use the list menu to select a **protocol**, which defaults to the UDP protocol. Additionally, you can specify **Priority**, **Weight** and **Port**. These three fields default to a value of 1. A **TTL** can also be specified from the list menu, with the default value of `Automatic`.

* Required Fields: Name, Service Name, Target
* Optional Fields: TTL (default value is `Automatic`), Protocol (defaulted to UDP), Priority (defaulted to 1), Weight (defaulted to 1), Port (defaulted to 1)

### TXT Type record
{: #txt-type-record}

To add this record type, valid values must exist in the **Name** and **Content** fields. A **TTL** can also be specified from the list menu, with the default value of `Automatic`.

* Required Fields: Name, Content
* Optional Field: TTL (default value is `Automatic`)

The first time that you order a dedicated certificate Domain Control Validation (DCV) process occurs, which generates a corresponding TXT record. If you delete the TXT record, the DCV process happens again when you order another dedicated certificate. If you delete a dedicated certificate, the TXT record corresponding to the DCV process is not deleted.
{: note}

### NS Type record
{: #ns-type-record}

To add this record type, valid values must exist in the **Name** and **Name Server** fields. A **TTL** can also be specified from the list menu, with the default value of `Automatic`.

* Required Fields: Name, Name Server
* Optional Field: TTL (default value is `Automatic`)

### PTR type record
{: #ptr-type-record}

The PTR record option that is shown in the DNS Records list menu is not for adding PTR records for Reverse DNS resolution. The purpose is to add a PTR Record to the Forward DNS resolution for the domain. PTR in Forward DNS is allowed under the [DNS specification](https://datatracker.ietf.org/doc/html/rfc1035#section-3.3.12){: external}.
{: note}

PTR records primarily prevent emails from going to spam folders. Because CIS doesn't support email traffic by default, you must set the PTR record to the location of your email server. Contact your email provider for assistance.

## Updating DNS records
{: #updating-dns-records}

In each record row, you can click the **Edit record** option from the menu, which opens a dialog box that you can use to update the record.

After you are finished making your changes, select **Update record** to save them, or **Cancel** to abort the changes.

## Deleting DNS records
{: #deleting-dns-records}

In each record row, you can select the **Delete record** option from the menu, which opens a dialog box to confirm the deletion process.

You can select the **Delete** button to confirm your delete action. Select **Cancel** if you don't want to delete.

## Importing and exporting DNS records
{: #import-export-records}

DNS records can be imported into and exported from {{site.data.keyword.cis_short_notm}}. All files are imported and exported as .txt files in BIND format. Learn more about [BIND format](https://en.wikipedia.org/wiki/Zone_file){: external}.
Click the Actions menu and select to import or export records.

**Import records** - By default, a total of 3500 DNS records are allowed (imported and created on {{site.data.keyword.cis_short_notm}}). You can import multiple files, one at a time, as long as the total number of records is under the max limit. After you import, you are shown a summary with the number of records that were successfully added and the number that failed, along with the reason why each record failed.

**Export records** - Use `Export records` to create a backup of your zone file, or export it to use with another DNS provider. When this menu option is clicked, the records are downloaded to the location specified by your browser settings (typically the Downloads folder). To select another folder location, change your browser's settings to prompt you for a location with each download.

## Configuring and managing your secure DNS
{: #configuring-and-managing-your-secure-dns}

**DNSSec** is a technology to digitally sign DNS data so you can know it is valid. To eliminate vulnerability from the internet, DNSSec must be deployed at each step in the lookup, from root zone to final domain name (for example, `www.icann.org`).

DNSSec adds a layer of authentication to the internet's DNS infrastructure, which otherwise is not secure. Secure DNS guarantees that visitors are directed to **your** web server when they type your domain name into a web browser. All that you need to do is enable DNSSec in your DNS page from your IBM {{site.data.keyword.cis_short_notm}} account and add the DS record to your registrar.

You can select **View DS records** to display the information that is needed to add the DS record to your registrar. You must copy parts of the DS record and paste them into your registrar’s dashboard. Every registrar is different, and your registrar might only require you to enter information for some of the available fields.
