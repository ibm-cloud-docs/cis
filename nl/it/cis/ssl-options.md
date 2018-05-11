---
copyright:
  years: 2018
lastupdated: "2018-02-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Opzioni TLS
Le opzioni TLS ti consentono di controllare se i visitatori possono sfogliare il tuo sito web su una connessione sicura e quando lo fanno, come CIS si collegherà al tuo server di origine.

Queste opzioni sono elencate nell'ordine dalla meno sicura (Off) alla più sicura (End-to-End CA signed). 

Modalità di codifica TLS:

 * Off (non consigliata)
 * Client-to-Edge (i certificati edge to origin non sono codificati, i certificati autofirmati non sono supportati) 
 * End-to-End flexible (i certificati edge to origin possono essere autofirmati) 
 * End-to-End CA signed (consigliato)

## Off 
Nessuna connessione protetta tra il tuo visitatore e CIS e tra CIS e il tuo server web. I visitatori possono solo visualizzare il tuo sito web su HTTP e chi tenta di collegarsi utilizzando HTTPS riceverà `HTTP 301 Redirect` che reindirizza alla versione HTTP semplice del tuo sito web.

## Client-to-Edge
Una connessione sicura tra il tuo visitatore e CIS ma non tra CIS e il tuo server web. Non devi disporre di un certificato TLS sul tuo server web, ma i tuoi visitatori vedono ancora il tuo sito come abilitato HTTPS. Questa opzione non è consigliata se hai informazioni sensibili sul tuo sito web. Questa impostazione funzionerà solo per la porta 443->80. Dovrebbe essere utilizzata solo come ultima risorsa se non sei in grado di configurare TLS sul tuo server web. È _meno sicura_ di tutte le altre opzioni (anche di “Off”) e potrebbe causare problemi quando decidi di passare a un'altra opzione.

## End-to-End Flexible
Una connessione sicura tra il tuo visitatore e CIS e (ma non autenticata) tra CIS e il tuo server web. Dovrai avere il tuo server configurato per rispondere alle connessioni HTTPS, con almeno un certificato autofirmato. L'autenticità del certificato non viene verificata: dal punto di vista di CIS (quando ci colleghiamo al tuo server web di origine), è equivalente a ignorare questo messaggio di errore. Finché l'indirizzo del tuo server web di origine è corretto nelle tue impostazioni DNS, sai che ci stiamo collegando noi al tuo server web e non qualcun altro.

## End-to-End CA Signed
Consigliato. Una connessione sicura tra il visitatore e CIS e sicura e autenticata tra CIS e il tuo server web. Dovrai avere il tuo server configurato per rispondere alle connessioni HTTPS, con un certificato TLS valido. Questo certificato deve essere firmato da un'autorità di certificazione, avere una data di scadenza nel futuro e rispondere al nome del dominio della richiesta (nome host).
