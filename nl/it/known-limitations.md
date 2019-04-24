---
copyright:
  years: 2018
lastupdated: "2018-03-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Limitazioni note

 * Ti consigliamo di utilizzare Chrome.

 * In Firefox e Safari, le date *uploaded*, *modified* e *expires* di un certificato non possono essere visualizzate.

 * La modifica della corrispondenza dell'URL di una regola della pagina provoca che la regola venga posizionata a una priorità più bassa.
 
 * Senza un dominio configurato, puoi passare a **Reliability > Global Load Balancers** per creare i controlli di integrità e i pool del programma di bilanciamento del carico. Tuttavia, se selezioni **Create load balancer**, configuri il programma di bilanciamento del carico e fai clic su **Provision 1 Resource**, la richiesta sarà rifiutata perché è obbligatorio un dominio. Questa limitazione della funzionalità aiuta gli utenti a comprendere lo scopo dei pool e monitora il flusso di creazione del programma di bilanciamento del carico.
 
 * Il programma Early Access è limitato a una istanza per account. Dopo aver creato un'istanza della risorsa e aggiunto un dominio ad essa, non ti è consentito aggiungere nuove istanze della risorsa a IBM CIS. Questa limitazione viene applicata anche se elimini un dominio di prova e poi tenti di aggiungere nuovamente un dominio alla stessa istanza della risorsa. Riceverai un errore se tenti di farlo.

 * Quando aggiungi un nuovo dominio, il nostro sistema al momento non raccoglie o importa i tuoi record del dominio esistenti.

 * Per questo programma Access Early, supportiamo la delega del dominio secondario solo utilizzando i record NS da un altro provider. La delega CNAME non è supportata.
