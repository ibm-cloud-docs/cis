---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIS Rule Set, WAF settings, WAF CIS Rules

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Impostazioni WAF
{:#waf-settings}

La seguente tabella mostra le azioni che possono essere eseguite da WAF (Web Application Firewall). 


|Azione| Definizione|
|---|---|
|Block | Il blocco di un attacco arresterà qualsiasi azione prima che venga inviata al tuo sito web. |
|Simulate| Per verificare i falsi positivi, imposta WAF sulla modalità Simulate che registra la risposta a possibili attacchi senza eseguire la verifica o il blocco. |
|Challenge | Una pagina di verifica chiede ai visitatori di inoltrare un CAPTCHA per proseguire verso il tuo sito web. |
|Threshold or sensitivity setting | Imposta le regole da attivare, più o meno, a seconda della sensibilità. |

## Serie di regole CIS per WAF
{:#cis-ruleset-for-waf}

Seleziona **View CIS Rules** per vedere le serie di regole di questo pacchetto. Le serie di regole sono:
  * Drupal
  * Flash
  * Joomla
  * Magento
  * Miscellaneous
  * PHP
  * Plone
  * Specials
  * WHMCS
  * Wordpress

**Specials** contiene un numero di regole appropriate per controllare virtualmente tutte le applicazioni e i siti web su internet. Questa serie di regole costituisce il fulcro della sicurezza offerta dal nostro WAF, con regole che fanno fronte ad attacchi comuni come SQLi, XSS e LFI. Ti consigliamo di lasciare sempre abilitato Specials. 

Abilita solo le serie di regole che corrispondono al tuo stack di tecnologie. Ad esempio, se utilizzi Wordpress e nessuna delle altre tecnologie, abilita solo le serie di regole Specials e Wordpress. Evita di abilitare serie di regole che non sono pertinenti al tuo stack di tecnologie. 

Seleziona una qualsiasi delle serie di regole per vedere ulteriori dettagli relativi a ciascuna delle regole incluse. 

La serie di regole CIS ti consente di eseguire quattro azioni su ogni regola: 
  1. **Disable**: disattiva la regola.
  2. **Simulate**: registra l'evento e non blocca o verifica il visitatore (puoi ancora decidere di impostare un blocco o una verifica dopo aver esaminato i tuoi log).
  3. **Block**: Block blocca semplicemente l'intera richiesta, senza possibilità di eludere il blocco per tale richiesta. 
  4. **Challenge**: visualizza una pagina di verifica (CAPTCHA) che deve essere completata prima che alla richiesta in questione venga concesso l'accesso. 

Potresti aver notato che i nomi delle regole non rivelano esattamente come funzionano e che sono per lo più un riepilogo generale della loro funzione. È intenzionale. Per scopi di sicurezza, non riveliamo il codice (oppure altre informazioni esatte) che utilizziamo per filtrare il traffico. Ciò impedisce ad aggressori dolosi di retroingegnerizzarlo per eludere le nostre difese. 
