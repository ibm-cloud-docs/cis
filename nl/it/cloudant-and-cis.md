---

copyright:
  years: 2019
lastupdated: "2019-03-28"

keywords: Cloudant database, CORS, cross-origin resource sharing, host header

subcollection: cis

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"} 
{:note: .note}


# Accedi al tuo database Cloudant tramite IBM Cloud Internet Services
{: #access-cloudant-through-cis}

Segui questi passi per accedere al tuo database Cloudant tramite IBM Cloud Internet Services (CIS).

## Prima di iniziare
{: #access-cloudant-through-cis-begin}

Queste istruzioni presuppongono che tu abbia già aggiunto un dominio a CIS come descritto nella pagina [Introduzione](/docs/infrastructure/cis?topic=cis-getting-started-with-ibm-cloud-internet-services-cis-).

### Passo 1: aggiungi il tuo dominio CIS a CORS (Cross-Origin Resource Sharing)
{: #access-cloudant-through-cis-step1}

* Vai al tuo database Cloudant e apri la pagina `Acccount` -> `CORS`.
* Aggiungi il tuo dominio CIS al campo di input dei domini di origine. Ad esempio, `https://cloudant.test.foo.com`.

### Passo 2. Configura CIS in modo che punti al tuo database Cloudant
{: #access-cloudant-through-cis-step2}

* Vai al dashboard CIS e crea un programma di bilanciamento del carico o un record DNS che punti al nome host del tuo database Cloudant. Ad esempio, `https://cloudant.test.foo.com` -> `111-222-333-444-555-test.cloudant.com`.
* Abilita `proxy` per il record DNS o per il programma di bilanciamento del carico. 


### Passo 3. Crea una regola della pagina per impostare Host Header Override
{: #access-cloudant-through-cis-step3}

* Nel dashboard CIS, vai a `Performance` -> `Page Rules`.
* Crea una regola della pagina per l'URL desiderato, ad esempio, `https://cloudant.test.foo.com/*`.
* Seleziona l'impostazione Rule Behavior `Host Header Override`.
* Imposta come il nome host database Cloudant, ad esempio, `111-222-333-444-555-test.cloudant.com`.

Per ulteriori informazioni su Cloudant, vedi la [documentazione di Cloudant](/docs/services/Cloudant?topic=cloudant-getting-started-with-cloudant).
