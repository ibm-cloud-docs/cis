---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: health checks, Free Trial plan, dedicated certificate, known issues

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 
{:note: .note} 
{:important: .important} 
{:deprecated: .deprecated} 
{:generic: data-hd-programlang="generic"}

# Limitazioni note
{:#known-limitations}

 * Ti consigliamo di utilizzare Chrome.
 
 * Il piano Free Trial è limitato a un'istanza per account. Dopo aver creato un'istanza della risorsa e aggiunto un dominio ad essa, non ti è consentito aggiungere nuove istanze della risorsa a IBM CIS. Questa limitazione viene applicata anche se elimini un dominio di prova e poi tenti di aggiungere nuovamente un dominio alla stessa istanza della risorsa. Riceverai un errore se tenti di farlo.

 * Per questo servizio, supportiamo la delega del dominio secondario solo utilizzando i record NS da un altro provider. La delega CNAME non è supportata.
  
 * I record carattere jolly (*) A, AAAA e CNAME non possono essere protetti con proxy.

 * Quando elimini un certificato dedicato, potrebbe comparire di nuovo nell'elenco per un breve periodo di tempo prima del completamento dell'eliminazione. 
 
 * Per modificare i nomi host del tuo certificato dedicato personalizzato dopo l'ordinazione, devi ordinare un nuovo certificato e poi eliminare quello vecchio.  
 
 * Le regole IP create con i codici paese a due lettere possono essere eseguite solo con l'azione `Challenge`. Se desideri bloccare i visitatori di un paese, esegui l'upgrade al piano Enterprise oppure sostituisci le regole sul tuo server per un blocco completo. 

## Programma di bilanciamento del carico globale
{:#known-limitations-glb}

 * CIS (Cloud Internet Services) ti consente di utilizzare il carattere `_` nei nomi host del programma di bilanciamento del carico, tuttavia, i cluster Kubernetes non possono utilizzare `_`. 

 * Il piano Standard consente massimo 5 programmi di bilanciamento del carico, pool e controlli di integrità. Ogni pool può avere un totale di 6 origini, ma sono consentite solo 6 origini univoche in ogni istanza CIS. 

* Gli eventi del controllo di integrità per le origini e i pool eliminati non possono essere filtrati, ma compaiono ancora nella tabella. 

* Se filtri gli eventi del controllo di integrità in base a `Pool Health`, i pool di tipo `Degraded` vengono inclusi perché tecnicamente sono integri, ma possono contenere una o più origini critiche. 

* Quando aggiungi il nome intestazione della richiesta per un controllo di integrità, utilizza `Host`. L'utilizzo di `host` in minuscolo per un controllo di integrità genera un errore. 

## DNS
{:#known-limitations-dns}

 * L'esportazione dei record DNS include i record CNAME Cloudflare che devono essere nascosti. Questi record iniziano con `_` e di solito hanno un secondo record con lo stesso nome ma senza il carattere `_`.
   ```
   Ex.
   _cf.generate.yourdomain.com 0	IN	CNAME address.alias.com
   cf.generate.yourdomain.com 0	IN	CNAME address2.alias.com
   ```
 
   Questi record devono essere rimossi dal file di zona per un'importazione corretta. 
 
 * L'esportazione dei record DNS CAA non funziona correttamente. `<tag>` e `<value>` sono codificati in esadecimale. 
 
    CAA `<flags>` `<tag>` `<value>`
  {:note}
   ```
   Ex.
   Original CAA record
   caa.yourdomain.com.	1	IN	CAA	0 issue "letsencrypt.org"
 
   Exported CAA record
   caa.yourdomain.com.	1	IN	CAA	0 6973737565 "6c657473656e63727970742e6f7267"
   ```
   Questi record devono essere convertiti da esadecimale a stringa oppure rimossi e aggiunti manualmente prima dell'importazione. 

## Regole della pagina
{:#known-limitations-pagerules}

   * L'aggiornamento delle impostazioni delle regole della pagina utilizzando il plugin CIS per la CLI di IBM Cloud potrebbe generare un errore se l'ID della regola della pagina non è incluso nella stringa JSON o nel file JSON per l'aggiornamento. Per risolvere temporaneamente questo problema, inoltra l'aggiornamento utilizzando un file di configurazione JSON completo per la regola della pagina, incluso l'ID.
   * La rimozione delle impostazioni della regola della pagina utilizzando la IU CIS potrebbe non rimuovere l'impostazione anche se la IU riporta uno stato di aggiornamento riuscito. Per risolvere temporaneamente questo problema, utilizza il plugin CIS per la CLI IBM Cloud per rimuovere l'impostazione e includere l'ID della regola della pagina nel documento di aggiornamento JSON:
      ```
      $> ibmcloud cis page-rule-update <domain-id> <rule-id> -j <file>
      ```
      Il file JSON deve includere la configurazione completa della regola della pagina, incluso l'ID, con gli aggiornamenti necessari. 
