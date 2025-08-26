---

copyright:
  years: 2025
lastupdated: "2025-08-26"

keywords: graphql, metrics, sampling

subcollection: cis

---

{{site.data.keyword.attribute-definition-list}}

# OWASP evaluation example
{: #owasp-evaluation-example}

The following example calculates the OWASP request threat score for an incoming request.
{: shortdesc}

 The OWASP managed ruleset configuration is as follows:
 
* OWASP Anomaly Score Threshold: `High - 25 and higher`
* OWASP Paranoia Level: `PL3`
* OWASP Action: **Managed Challenge**

This table shows the progress of the OWASP ruleset evaluation:

| Rule ID | Paranoia level | Rule matched? | Rule score | Cumulative threat score |
| - | - | - | - | - |
| – | – | – | – | 0 |
| `...1813a269` | PL3 | Yes | +5 | 5 |
| `...ccc02be6` | PL3 | No | – | 5 |
| `...96bfe867` | PL2 | Yes | +5 | 10 |
| `...48b74690` | PL1 | Yes | +5 | 15 |
| `...3297003f` | PL2 | Yes | +3 | 18 |
| `...317f28e1` | PL1 | No | – | 18 |
| `...682bb405` | PL2 | Yes | +5 | 23 |
| `...56bb8946` | PL2 | No | – | 23 |
| `...e5f94216` | PL3 | Yes | +3 | 26 |
| (...) | (...) | (...) | (...) | (...) |
| `...f3b37cb1` | PL4 | (not evaluated) | – | 26 |
{: caption="Progress of the OWASP ruleset evaluation" caption-side="bottom"}

Final request threat score: `26`

Since `26` >= `25` — that is, the threat score is greater than the configured score threshold — CIS will apply the configured action (**Managed Challenge**). If you had configured a score threshold of `Medium - 40 and higher`, CIS wouldn't apply the action, since the request threat score would be lower than the score threshold (`26` < `40`).

[Sampled logs in Security Events](/docs/cis?topic=cis-sampling) would display the following details for the example incoming request handled by the OWASP Core Ruleset.
 
In sampled logs, the rule associated with requests mitigated by the CIS OWASP Core Ruleset is the last rule in this managed ruleset: `949110: Inbound Anomaly Score Exceeded`, with rule ID `6179ae15870a4bb7b2d480d4843b323c`. To get the scores of individual rules contributing to the final request threat score, expand **Additional logs** in the event details.
