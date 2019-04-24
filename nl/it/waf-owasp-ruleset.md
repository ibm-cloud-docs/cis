---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: OWASP Rule Set, Rule Set

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Serie di regole OWASP per WAF
{:#owasp-rule-set-for-waf}

La serie di regole OWASP contiene regole generiche di rilevamento degli attacchi. Le regole OWASP proteggono da molte categorie comuni di attacchi, tra cui SQL Injection, Cross-Site Scripting e Locale File Inclusion, tra le altre. IBM CIS fornisce queste regole ma non se ne occupa. OWASP è uno standard del settore che fornisce una buona baseline di sicurezza. Per ulteriori informazioni, vedi i seguenti link: 
  * [OWASP on Github](https://github.com/SpiderLabs/owasp-modsecurity-crs)
  * [OWASP.org](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project)

## Gestione di OWASP
{:#managing-owasp}

A differenza della [serie di regole CIS](/docs/infrastructure/cis?topic=cis-cis-rule-set-for-waf), OWASP ti consente di impostare la sensibilità.
Una richiesta può attivare una serie di regole OWASP che hanno un punteggio di severità, che va da alto a basso, associato ad esse. Il punteggio finale viene calcolato in base a tutte le regole attivate. Una volta calcolato il punteggio finale, CIS lo confronta con la soglia di sensibilità selezionata al principio e quindi blocca o consente la richiesta. 

|Punteggio sensibilità| Soglia di attivazione|
|------|---------------|
|Basso   |  60 e oltre|
|Medio|  40 e oltre|
|Alto  |  25 e oltre|

Ti suggeriamo di impostare la sensibilità OWASP su basso (`low`). Se la imposti su alto (`high`), controlla i log su CIS e ottimizza la serie di regole OWASP affinché funzioni per la tua applicazione. 

Tieni presente che le regole OWASP possono essere solo _attivate_ o _disattivate_, a differenza delle regole nelle serie di regole CIS che possono essere impostate su _Disable_, _Simulate_, _Challenge_ o _Block_.

## Come posso gestire i falsi positivi?
{:#owasp-false-positives}

I falsi positivi possono verificarsi quando una variabile o un valore viene valutato come _true_ o _positivo_ ma è effettivamente negativo. Nel contesto del nostro WAF, un falso positivo significa che una richiesta è bloccata perché è stata erroneamente valutata come dolosa. 

Per gestire i falsi positivi e assicurarti di evitarli in futuro, devi sapere come individuarli e correggerli. Esamina i log delle richieste bloccate e poi valuta se queste richieste sono state ragionevolmente bloccate all'interno del contesto del traffico normale e previsto del tuo sito web. 
