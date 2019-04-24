---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: global load balancer, global load balancer configuration

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Definisci il programma di bilanciamento del carico globale 
{:#define-the-global-load-balancer}

 Definisci la configurazione del tuo programma di bilanciamento del carico globale specificando un nome host, aggiungendo e modificando i tuoi pool di origini e definendo ulteriori regole per controllare come viene servito il traffico ai client. 

1. Crea il tuo programma di bilanciamento del carico globale facendo clic sul pulsante Create load balancer a destra.   

2. Specifica il nome host del tuo dominio e modifica il valore TTL se lo desideri (il valore predefinito è 60 secondi) e utilizza **Add Pool** per aggiungere i tuoi pool di origini.  

   <img src="images/reliability11.png" alt="immagine" style="width: 300px;"/>
   
   **NOTA:** i nomi host combinati con i nomi del dominio formano i nomi dominio completi (FQDN) della tua applicazione. I tuoi utenti finali si collegano alla tua applicazione utilizzando questo FQDN.  
   
3. Modifica le priorità relative dei tuoi pool di origini facendo clic sulle frecce su e giù alla sinistra del pool. Le richieste dell'applicazione dagli utenti finali vengono gestite in modalità round robin da questi pool di origini.  
   
   <img src="images/reliability12.png" alt="immagine" style="width: 300px;"/>   
   
4. Facoltativamente, puoi definire ulteriori regole per controllare come il traffico viene servito ai client da diverse regioni geografiche. Nel seguente esempio, i client che arrivano dalla regione America del Sud vengono instradati al pool di origini Stati Uniti Costa Ovest. Puoi utilizzare queste regole per indirizzare i client alla regione più vicina. Se una di queste regioni ha un malfunzionamento, le richieste vengono instradate ad altre ubicazioni integre disponibili, in modo che gli utenti finali non siano influenzati dal tempo di inattività.  

   <img src="images/reliability13.png" alt="immagine" style="width: 300px;"/>   
   
5. Fai clic su **Provision Resources** per completare la configurazione del tuo programma di bilanciamento del carico globale.  
6. Infine, verifica la connettività alla tua applicazione immettendo `FQDN URL` in una finestra di un browser mobile. Visualizzerai un messaggio di benvenuto se puoi collegarti. 
