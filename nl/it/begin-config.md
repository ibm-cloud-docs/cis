---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: global load balancer configuration, glb configuration

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}

# Avvio della configurazione del programma di bilanciamento del carico globale
{:#begin-global-load-balancer-configuration}

 Avvia la configurazione del tuo programma di bilanciamento del carico globale. 

1. Nella sezione **Reliability**, seleziona **Global Load Balancer**. 
    
    <img src="images/reliability6.png" alt="immagine" style="width: 300px;"/>

2. Scorri fino alla sezione Health Checks.  

   Questa configurazione è facoltativa. Se non definisci alcun controllo di integrità personalizzato, il sistema utilizzerà “/” come percorso del tuo controllo di integrità predefinito.
   {:note}

3. Fai clic sul pulsante **Create health check** per definire un controllo di integrità personalizzato.    

   Fornisci il percorso in cui desideri eseguire i controlli di integrità. Puoi utilizzare i protocolli HTTP o HTTPS per i tuoi controlli di integrità.  
   
4. In **Advanced options**, puoi personalizzare altri parametri, come l'intervallo del controllo di integrità, il numero di tentativi, il metodo di richiesta e il corpo della risposta, nelle opzioni avanzate.  
   
   <img src="images/reliability7.png" alt="immagine" style="width: 300px;"/>
   
5. Fai clic su **Provision Resource** per completare la configurazione del tuo controllo di integrità.  
