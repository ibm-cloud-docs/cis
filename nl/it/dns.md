---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM CIS DNS records, parts of the DS record, Type

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:DomainName: data-hd-keyref="DomainName"} 
{:note: .note} 
{:important: .important} 
{:deprecated: .deprecated} 
{:generic: data-hd-programlang="generic"}

# Configura il tuo DNS (Domain Name System) per IBM CIS
{:#set-up-your-dns-for-cis}

Questo documento contiene alcune istruzioni specifiche su come configurare i tuoi record DNS IBM CIS, incluso come configurare il DNS protetto.

## DNS protetto
{:#secure-dns}

**DNSSec** è una tecnologia per "firmare" digitalmente i dati DNS in modo da assicurarti che siano validi. Per eliminare la vulnerabilità da internet, DNSSec deve essere distribuito in ogni fase della ricerca, dalla zona root al nome del dominio finale (ad esempio, www.icann.org).

## Configurazione e gestione del DNS protetto 
{:#configuring-and-managing-your-secure-dns}

DNSSec aggiunge un livello di autenticazione all'infrastruttura DNS di internet, che altrimenti non è sicura. Il DNS protetto garantisce che i visitatori siano indirizzati al **tuo** server web quando immettono il tuo nome del dominio in un browser web.  Tutto quello che devi fare è abilitare DNSSec nella tua pagina DNS dal tuo account IBM CIS e aggiungere il record DNS alla tua funzione di registrazione.

![DNS protetto](images/dns/secure-dns.png)

Puoi selezionare il pulsante **View DS records** per aprire una finestra di dialogo che illustra come aggiungere il record DS alla tua funzione di registrazione. Devi copiare le parti del record DS e incollarle nel dashboard della tua funzione di registrazione. Ogni funzione di registrazione è diversa e la tua può richiedere solo di immettere le informazioni di alcuni dei campi disponibili.

## Aggiunta dei record DNS
{:#adding-dns-records}

Puoi utilizzare il menu a discesa **Type** per selezionare il tipo di record che vuoi creare. Ogni tipo di record DNS ha un nome e un TTL (Time-To-Live) associati ad esso. 

Qualsiasi valore immesso nel campo del nome avrà il nome del dominio accodato ad esso a meno che non sia stato già accodato manualmente al campo (ad esempio se viene immesso `www` o `www.example.com` nel campo, l'API gestirà entrambi come `www.example.com`). Se viene immesso il nome del dominio esatto nel campo del nome, allora non sarà accodato a se stesso (ad esempio `example.com` sarà gestito come `example.com`). Tuttavia, l'elenco dei record DNS mostrerà solo i nomi senza il nome del dominio che gli viene aggiunto, per cui `www.example.com` viene mostrato come `www` e `example.com` sarà mostrato come `example.com`. Il TTL avrà un valore predefinito di `Automatic`, ma può essere modificato dall'utente. Un record DNS con proxy avrà sempre un TTL di `Automatic`, quindi un nuovo record con proxy sarà modificato con questa configurazione durante questa modifica.

### Un tipo di record
{:#a-type-record}

Per aggiungere questo tipo di record, devono essere presenti dei valori validi nei campi **Name** e **IPv4 Address**. Può inoltre essere specificato un **TTL** dal menu a discesa, con un valore predefinito di `Automatic`.

![Crea un tipo di record](images/dns/create-a-type-record.png)

    Required Fields: Name, IPv4 Address
    Optional Field: TTL (Default value is Automatic)

### Tipo di record AAAA
{:#aaaa-type-record}

Per aggiungere questo tipo di record, devono essere presenti dei valori validi nei campi **Name** e **IPv6 Address**. Può inoltre essere specificato un **TTL** dal menu a discesa, con il valore predefinito di `Automatic`.

![Crea tipo di record AAAA](images/dns/create-aaaa-type-record.png)

    Required Fields: Name, IPv6 Address
    Optional Field: TTL (Default value is Automatic)

### Tipo di record CNAME
{:#cname-type-record}

Per aggiungere questo tipo di record deve essere presente un valore valido nel campo **Name** e un nome del dominio completo nel campo **Domain Name** (FQDN). Può inoltre essere specificato un **TTL** dal menu a discesa, con il valore predefinito di `Automatic`.


![Crea tipo di record CNAME](images/dns/create-cname-type-record.png)

    Required Fields: Name, Domain Name (for CNAME)
    Optional Field: TTL (Default value is Automatic)

I piani Enterprise sono in grado di fornire un CNAME a un altro dominio fino a quando tale dominio è configurato all'interno di CIS.
{:note}

```
Ex.
Configured CIS Domains:
  - example.com
  - different.com

test.example.com -CNAME-> test.different.com
```

### Tipo di record MX
{:#mx-type-record}

Per aggiungere questo tipo di record deve essere presente un valore valido nel campo **Name** e un indirizzo valido nel campo **Mail Server**. Può inoltre essere specificato un **TTL** dal menu a discesa, con il valore predefinito di `Automatic`.

![Crea tipo di record MX](images/dns/create-mx-type-record.png)

    Required Fields: Name, Mail Server
    Optional Fields: TTL (Default value is Automatic), Priority (Default value is 1)

### Tipo di record LOC
{:#loc-type-record}

Per aggiungere questo tipo di record, un valore valido deve essere presente nel campo **Name**. Se hai bisogno di ulteriori informazioni specifiche, seleziona il pulsante **Configure LOC options**. Può inoltre essere specificato un **TTL** dal menu a discesa, con il valore predefinito di `Automatic`.

![Crea tipo di record LOC](images/dns/create-loc-type-record-1.png)

    Required Fields: Name
    Optional Fields: LOC options (click the button to configure)

![Crea tipo di record LOC](images/dns/create-loc-type-record-2.png)

### Tipo di record CAA
{:#caa-type-record}

Per aggiungere questo tipo di record, devono essere presenti dei valori validi nei campi **Name** e **Value**. Il campo Value sarà correlato al valore del campo a discesa **Tag**, che per impostazione predefinita è "Send violation reports to URL". Può anche essere specificato un **TTL** dal menu a discesa, con il valore predefinito `Automatic`.

![Crea tipo di record CAA](images/dns/create-caa-type-record.png)

    Required Fields: Name, Value (associated to tag)
    Optional Fields: TTL (Default value is Automatic), Tag (default is to send violation reports to URL)

### Tipo di record SRV
{:#srv-type-record}

Per aggiungere questo tipo di record, devono essere presenti dei valori validi nei campi **Name**, **Service Name** e **Target**. Utilizza il menu a discesa per selezionare un **protocollo**, che per impostazione predefinita è UDP. Inoltre, puoi specificare **Priority**, **Weight** e **Port**. Questi tre campi sono impostati sul valore predefinito 1. Può essere specificato anche un **TTL** dal menu a discesa, con il valore predefinito di `Automatic`.

![Crea tipo di record SRV](images/dns/create-srv-type-record.png)

    Required Fields: Name, Service Name, Target
    Optional Fields: TTL (Default value is Automatic), Protocol (Defaulted to UDP), Priority (Defaulted to 1), Weight (Defaulted to 1), Port (Defaulted to 1)

### Tipo di record SPF
{:#spf-type-record}

Per aggiungere questo tipo di record, devono essere presenti dei valori validi nei campi **Name** e **Content**. Può inoltre essere specificato un **TTL** dal menu a discesa, con il valore predefinito di `Automatic`.

![Crea tipo di record SPF](images/dns/create-spf-type-record.png)

    Required Fields: Name, Content
    Optional Field: TTL (Default value is Automatic)

### Tipo di record TXT
{:#txt-type-record}

Per aggiungere questo tipo di record, devono essere presenti dei valori validi nei campi **Name** e **Content**. Può inoltre essere specificato un **TTL** dal menu a discesa, con il valore predefinito di `Automatic`.

![Crea tipo di record TXT](images/dns/create-txt-type-record.png)

    Required Fields: Name, Content
    Optional Field: TTL (Default value is Automatic)

La prima volta che ordini un certificato dedicato, viene eseguito il processo DCV (Domain Control Validation) che genera un record TXT corrispondente. Se elimini il record TXT, il processo DCV viene eseguito nuovamente quando ordini un altro certificato dedicato. Se elimini un certificato dedicato, il record TXT corrispondente al processo DCV non viene eliminato.
{:note}

### Tipo di record NS
{:#ns-type-record}

Per aggiungere questo tipo di record, devono essere presenti dei valori validi nei campi **Name** e **Name Server**. Può inoltre essere specificato un **TTL** dal menu a discesa, con il valore predefinito di `Automatic`.

![Crea tipo di record NS](images/dns/create-ns-type-record.png)

    Required Fields: Name, Name Server
    Optional Field: TTL (Default value is Automatic)

## Aggiornamento dei record DNS
{:#updating-dns-records}

In ogni riga del record, puoi fare clic sull'opzione **Edit record** dal menu, che aprirà una finestra di dialogo che puoi utilizzare per aggiornare il record.

![Modifica record DNS](images/dns/edit-dns-record.png)

Ad esempio, questa è la finestra di dialogo di aggiornamento del tipo di record **A**. Quando hai finito di apportare le tue modifiche, seleziona **Update record** per salvarle.

![Finestra di dialogo Modifica record DNS](images/dns/update-dns-dialog.png)

## Eliminazione dei record
{:#deleting-dns-records}

In ogni riga del record, puoi selezionare l'opzione **Delete record** dal menu, che aprirà una finestra di dialogo per confermare il processo di eliminazione.

![Elimina record DNS](images/dns/delete-record.png)

Puoi selezionare il pulsante **Delete** per confermare la tua azione di eliminazione. Seleziona **Cancel** se non vuoi eseguire l'eliminazione.

![Finestra di dialogo Elimina record DNS](images/dns/delete-record-dialog.png)

## Importa ed esporta i record
{:#import-export-records}

I record DNS possono essere importati ed esportati da CIS. Tutti i file vengono importati ed esportati come file .txt in formato BIND. Ulteriori informazioni sul [formato BIND](https://en.wikipedia.org/wiki/Zone_file).
Fai clic sul menu di overflow e seleziona l'importazione o l'esportazione dei record.
![Opzione record DNS](images/dns/import-export-records.png)

### Importa i record
{:#import-dns-records}

Per impostazione predefinita, è consentito un massimo di 3500 record DNS totali (importati e creati su CIS). Puoi importare più file, uno alla volta, fino a quando il numero totale dei record rimane sotto il limite massimo. Dopo l'importazione, viene visualizzato un riepilogo con il numero di record aggiunti correttamente e con il numero di quelli non riusciti insieme al motivo per cui ogni record ha avuto esito negativo.
![Riepilogo importazione record DNS](images/dns/import-records-summary.png)

### Esporta i record
{:#export-dns-records}

Utilizza `Export records` per creare un backup del tuo file di zona oppure esportalo per utilizzarlo con un altro provider DNS. Quando fai clic su questa opzione di menu, i record vengono scaricati nell'ubicazione specificata dalle impostazioni del tuo browser (di norma la cartella Download). Per selezionare un'altra ubicazione, modifica le impostazioni del tuo browser in modo che ti venga richiesta l'ubicazione ogni volta che scarichi un file. 
