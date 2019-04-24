---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: origin pools, application resources, Origin Pools section

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Identifica le tue risorse dell'applicazione
{:#identify-your-application-resources}

 Identifica le risorse della tua applicazione, come i pool di origini e i meccanismi del controllo di integrità. 
 
1. Passa alla sezione **Origin Pools** e fai clic su **Create pool** per definire un nuovo pool di origini.  

   I pool di origini sono risorse server che forniscono le applicazioni ai tuoi client.  
   
2. Assegna un nome al tuo pool di origini e seleziona il meccanismo di controllo di integrità definito in precedenza. Aggiungi il tuo server dell'applicazione come tua origine. Puoi aggiungere più di un'origine facendo clic su **Add Origin**. 

   Se i tuoi server dell'applicazione si trovano dietro a un programma di bilanciamento del carico locale come un IBM Cloud Load Balancer, aggiungi il FQDN o l'IP virtuale del tuo programma di bilanciamento del carico come tua origine invece di aggiungere i tuoi singoli server.
   {:note}
   
3. Fai clic su **Provision Resource** per completare la creazione del tuo pool di origine.   

   <img src="images/reliability8.png" alt="immagine" style="width: 300px;"/>
   
   Il pool di origine sarà inizialmente visualizzato come **Unhealthy**. Il suo stato sarà modificato con **Healthy** dopo un controllo di integrità riuscito dal sistema. Potresti dover aggiornare il tuo browser per visualizzare la modifica dello stato.  
   
   <img src="images/reliability9.png" alt="immagine" style="width: 300px;"/>
   
   Se hai più origini all'interno del tuo pool di origini, utilizza la soglia di origine di integrità per specificare il numero minimo di origini che devono essere integre prima di dichiarare il pool integro.
   {:note}
   
4. Definisci tanti pool di origini quanto è il numero di farm dell'applicazione di cui disponi. Questi farm possono essere all'interno delle stesse o di differenti
regioni geografiche. Nel nostro esempio, creeremo due pool di origine che rappresentano un farm dell'applicazione negli Stati Uniti costa ovest e est.  

   <img src="images/reliability10.png" alt="immagine" style="width: 300px;"/>
