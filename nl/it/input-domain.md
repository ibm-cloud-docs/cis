---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: domain Input information, IBM Cloud Internet Service, Domain Name

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Immetti le informazioni sul tuo dominio
{:#input-information-about-your-domain}

Immetti le informazioni sul dominio che vuoi proteggere e per cui vuoi fornire il bilanciamento del carico globale. 

1. Fai clic su **Overview** a sinistra della schermata Getting Started. Immetti il tuo nome dominio (o il nome del dominio secondario) e fai clic su **Add domain**. 
    
    <img src="images/reliability3.png" alt="immagine" style="width: 300px;"/>
    
    IBM Cloud Internet Service non è una funzione di registrazione DNS, per cui questo dominio (o dominio secondario) deve essere stato precedentemente creato.
    {:note}

    Nella sezione Service Details, noterai che il dominio appena aggiunto sarà visualizzato inizialmente nello stato Pending.  

    <img src="images/reliability4.png" alt="immagine" style="width: 300px;"/>    

2. Passa alla pagina di gestione del tuo dominio con la tua rispettiva funzione di registrazione DNS e delega il tuo dominio/dominio secondario ai server dei nomi IBM definendo i record NS. 

Potresti dover attendere fino a 24 ore perché le tue informazioni vengano replicate nel database DNS. Come terminato, lo stato del tuo dominio sarà modificato con Active.  

<img src="images/reliability5.png" alt="immagine" style="width: 300px;"/>    
