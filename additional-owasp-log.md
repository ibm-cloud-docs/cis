---

copyright:
  years: 2020, 2025
lastupdated: "2025-07-07"

keywords: OWASP logging

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# Enabling enhanced OWASP event logging
{: #additional-owasp-logging}

To gain deeper insight into potential threats, you can enable logging for all OWASP events that contribute to the overall threat score, not just those events that exceed the configured sensitivity threshold. Enabling enhanced OWASP logging gives you a more complete view of security activity, which helps with analysis, tuning, and audits.
{: shortdesc} 

By default (when disabled), only OWASP events that cross the configured sensitivity threshold are logged. 

To enable additional OWASP event logging in the console, follow these steps:

1. In the CIS console, navigate to the **Account** section.
1. In the **Logs** view, enable the **Enhanced OWASP logging** toggle.

   When you enable this toggle, the volume of logs generated increases, which can lead to higher storage and processing costs depending on your log retention and usage. For help estimating the impact, see [Estimating daily log volume](/docs/cis?topic=cis-volume-estimate).
   {: note}

After you enable this toggle, all OWASP-triggered events appear in both Logpush jobs (Dataset Firewall Events) and Security Events.
   
