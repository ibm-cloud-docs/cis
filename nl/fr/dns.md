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

# Configuration de votre DNS pour IBM CIS
{:#set-up-your-dns-for-cis}

Le présent document comporte des instructions spécifiques concernant les modalités de configuration de vos enregistrements DNS IBM CIS, y compris concernant la configuration d'un DNS sécurisé.

## DNS sécurisé
{:#secure-dns}

La technologie **DNSSec** permet d'apposer une "signature" numérique aux données DNS et garantit ainsi à l'utilisateur la validité de ces données. Afin d’éliminer cette vulnérabilité de l'Internet, il faut déployer DNSSec à chaque étape de consultation, de la consultation de la zone racine à celle du nom de domaine final, comme www.icann.org.

## Configuration et gestion de votre DNS sécurisé 
{:#configuring-and-managing-your-secure-dns}

DNSSec ajoute une couche d'authentification à l'infrastructure DNS Internet, qui autrement n'est pas sécurisée. Le DNS sécurisé garantit que les visiteurs sont dirigés vers **votre** serveur Web lorsqu'ils tapent votre nom de domaine dans un navigateur Web.  Tout ce dont vous avez besoin de faire est d'activer DNSSec sur la page DNS de votre compte IBM CIS et d'ajouter l'enregistrement DS à votre registre.

![DNS sécurisé](images/dns/secure-dns.png)

Vous pouvez cliquer sur le bouton **Afficher les enregistrements DS** pour ouvrir une boîte de dialogue expliquant comment ajouter l'enregistrement DS à votre registre. Vous devez copier des parties de l'enregistrement DS et les coller dans le tableau de bord de votre registre. Chaque registre est différent, et il se peut que le vôtre nécessite seulement que vous saisissiez des informations concernant certaines zones disponibles.

## Ajout d'enregistrements DNS
{:#adding-dns-records}

Vous pouvez utiliser la liste déroulante **Type** pour sélectionner le type d'enregistrement que vous souhaitez créer. Chaque type d'enregistrement DNS est associé à une zone de durée de vie (TTL). 

Les données saisies dans la zone Nom contiennent le nom de domaine à moins que le nom de domaine ne soit ajouté manuellement à la zone (par exemple, si `www` ou `www.example.com` est saisi dans la zone, l'API gère les deux formats comme `www.example.com`). Si le nom de domaine exact est indiqué dans la zone de nom, il n'est pas ajouté une nouvelle fois (par exemple, `example.com` sera géré comme `example.com`). Toutefois, la liste des enregistrements DNS affiche uniquement les noms sans le nom de domaine ajouté, autrement dit `www.example.com` s'affiche comme `www` et `example.com` s'affiche comme `example.com`. La durée de vie (TTL) prend la valeur par défaut `Automatique`, mais celle-ci peut être modifiée par l'utilisateur. Un enregistrement DNS qui agit comme un proxy aura toujours une valeur TTL `Automatique`, ce qui signifie qu'un nouvel enregistrement agissant comme un proxy reflétera cette configuration pendant la modification.

### Enregistrement de type A
{:#a-type-record}

Pour ajouter ce type d'enregistrement, les zones **Nom** et **Adresse IPv4** doivent posséder des valeurs valides. Une valeur **TTL** peut également être définie à partir du menu déroulant, dont la valeur par défaut est `Automatique`.

![Création d'un enregistrement de type A](images/dns/create-a-type-record.png)

    Zones obligatoires : Nom, Adresse IPv4
    Zone facultative : TTL (valeur par défaut 'Automatique')

### Enregistrement de type AAAA
{:#aaaa-type-record}

Pour ajouter ce type d'enregistrement, les zones **Nom** et **Adresse IPv6** doivent posséder valeurs valides. Une valeur **TTL** peut également être définie à partir du menu déroulant, dont la valeur par défaut est `Automatique`.

![Création d'un enregistrement de type AAAA](images/dns/create-aaaa-type-record.png)

    Zones obligatoires : Nom, Adresse IPv6
    Zone facultative : TTL (valeur par défaut 'Automatique')

### Enregistrement de type CNAME
{:#cname-type-record}

Pour ajouter ce type d'enregistrement, la zone **Nom** doit posséder une valeur valide et la zone **Nom de domaine** doit posséder un nom de domaine complet (FQDN). Une valeur **TTL** peut également être définie à partir du menu déroulant, dont la valeur par défaut est `Automatique`.


![Création d'un enregistrement de type CNAME](images/dns/create-cname-type-record.png)

    Zones obligatoires : Nom, Nom de domaine (pour CNAME)
    Zone facultative : TTL (valeur par défaut 'Automatique')

Les forfaits Enterprise peuvent nommer un autre domaine CNAME tant que ce domaine est configuré dans CIS.
{:note}

```
Ex.
Domaines CIS configurés :
  - example.com
  - different.com

test.example.com -CNAME-> test.different.com
```

### Enregistrement de type MX
{:#mx-type-record}

Pour ajouter ce type d'enregistrement, la zone **Nom** doit posséder une valeur valide et la zone **Serveur de courrier** doit posséder une adresse valide. Une valeur **TTL** peut également être définie à partir du menu déroulant, dont la valeur par défaut est `Automatique`.

![Création d'un enregistrement de type MX](images/dns/create-mx-type-record.png)

    Zones obligatoires : Nom, Serveur de courrier
    Zones facultatives : TTL (valeur par défaut 'Automatique'), Priorité (valeur par défaut '1')

### Enregistrement de type LOC
{:#loc-type-record}

Pour ajouter ce type d'enregistrement, la zone **Nom** doit posséder une valeur valide. Si vous avez besoin de plus amples informations, cliquez sur le bouton **Configurer les options LOC**. Une valeur **TTL** peut également être définie à partir du menu déroulant, dont la valeur par défaut est `Automatique`.

![Création d'un enregistrement de type LOC](images/dns/create-loc-type-record-1.png)

    Zones obligatoires : Nom
    Zones facultatives : Options LOC (cliquez sur le bouton pour procéder à la configuration)

![Création d'un enregistrement de type LOC](images/dns/create-loc-type-record-2.png)

### Enregistrement de type CAA
{:#caa-type-record}

Pour ajouter ce type d'enregistrement, les zones **Nom** et **Valeur** doivent posséder des valeurs valides. La zone Valeur tiendra compte de la valeur de la zone déroulante **Etiquette**, qui correspond par défaut à "Envoyer les rapports de violation à l'URL". Une valeur **TTL** peut également être définie à partir du menu déroulant, dont la valeur par défaut est `Automatique`.

![Création d'un enregistrement de type CAA](images/dns/create-caa-type-record.png)

    Zones obligatoires : Nom, Valeur (associés à des étiquettes)
    Zones facultatives : TTL (valeur par défaut est Automatique), Etiquette (valeur par défaut est l'envoi de rapports de violation à l'URL)

### Enregistrement de type SRV
{:#srv-type-record}

Pour ajouter ce type d'enregistrement, les zones **Nom**, **Nom de service** et **Cible** doivent posséder des valeurs valides. Utilisez le menu déroulant pour sélectionner un **protocole** (la valeur par défaut est UDP). Vous pouvez également indiquer une **priorité**, un **poids** et un **port**. La valeur par défaut de ces trois zones est 1. La valeur **TTL** peut également être définie à partir du menu déroulant, dont la valeur par défaut est `Automatique`.

![Création d'un enregistrement de type SRV](images/dns/create-srv-type-record.png)

    Zones obligatoires : Nom, Nom de service, Cible
    Zones facultatives : TTL (valeur par défaut Automatique), Protocole (valeur par défaut UDP), Priorité (valeur par défaut 1), Poids (valeur par défaut 1), Port (valeur par défaut 1)

### Enregistrement de type SPF
{:#spf-type-record}

Pour ajouter ce type d'enregistrement, les zones **Nom** et **Contenu** doivent posséder des valeurs valides. Une valeur **TTL** peut également être définie à partir du menu déroulant, dont la valeur par défaut est `Automatique`.

![Création d'un enregistrement de type SPF](images/dns/create-spf-type-record.png)

    Zones obligatoires : Nom, Contenu
    Zone facultative : TTL (valeur par défaut 'Automatique')

### Enregistrement de type TXT
{:#txt-type-record}

Pour ajouter ce type d'enregistrement, les zones **Nom** et **Contenu** doivent posséder des valeurs valides. Une valeur **TTL** peut également être définie à partir du menu déroulant, dont la valeur par défaut est `Automatique`.

![Création d'un enregistrement de type TXT](images/dns/create-txt-type-record.png)

    Zones obligatoires : Nom, Contenu
    Zone facultative : TTL (valeur par défaut 'Automatique')

La première fois que vous commandez un certificat dédié, un processus de validation de contrôle de domaine (DCV) se produit, ce qui génère un enregistrement TXT correspondant. Si vous supprimez l'enregistrement TXT, le processus DCV se répète lorsque vous commandez un autre certificat dédié. Si vous supprimez un certificat dédié, l'enregistrement TXT correspondant au processus DCV n'est pas supprimé. {:note}

### Enregistrement de type NS
{:#ns-type-record}

Pour ajouter ce type d'enregistrement, les zones **Nom** et **Serveur de noms** doivent posséder des valeurs valides. Une valeur **TTL** peut également être définie à partir du menu déroulant, dont la valeur par défaut est `Automatique`.

![Création d'un enregistrement de type NS](images/dns/create-ns-type-record.png)

    Zones obligatoires : Nom, Serveur de noms
    Zone facultative : TTL (valeur par défaut 'Automatique')

## Mise à jour des enregistrements DNS
{:#updating-dns-records}

Pour chaque ligne de l'enregistrement, vous pouvez cliquer sur l'option de menu **Modifier l'enregistrement** afin d'ouvrir une boîte de dialogue dans laquelle mettre à jour l'enregistrement.

![Modification d'un enregistrement DNS](images/dns/edit-dns-record.png)

L'exemple ci-dessus affiche la boîte de dialogue de mise à jour d'un enregistrement de type **A**. Une fois les modifications effectuées, cliquez sur le bouton **Mettre à jour l'enregistrement** pour les enregistrer.

![Boîte de dialogue de modification d'un enregistrement DNS](images/dns/update-dns-dialog.png)

## Suppression des enregistrements
{:#deleting-dns-records}

Sur chaque ligne d'enregistrement, cliquez sur l'option de menu **Supprimer l'enregistrement** afin d'ouvrir une boîte de dialogue dans laquelle confirmer la suppression.

![Suppression d'un enregistrement DNS](images/dns/delete-record.png)

Cliquez sur le bouton **Supprimer** pour confirmer la suppression. Sinon, cliquez sur **Annuler**.

![Boîte de dialogue de suppression d'un enregistrement DNS](images/dns/delete-record-dialog.png)

## Importation et exportation d'enregistrements
{:#import-export-records}

Les enregistrements DNS peuvent être importés et exportés de CIS. Tous les fichiers sont importés et exportés sous forme de fichiers .txt au format BIND. Consultez plus d'informations sur le [format BIND](https://en.wikipedia.org/wiki/Zone_file). Cliquez sur le menu déroulant dynamique et sélectionnez l'importation et l'exportation d'enregistrements.
![Option d'enregistrement DNS](images/dns/import-export-records.png)

### Importation d'enregistrements
{:#import-dns-records}

Par défaut, 3 500 enregistrements DNS sont autorisés (importés et créés sur CIS). Vous pouvez importer plusieurs fichiers, un à la fois, à condition que le nombre total d'enregistrements soit inférieur à la limite maximale. Après l'importation, un récapitulatif s'affiche avec le nombre d'enregistrements ajoutés avec succès et le nombre d'échecs, ainsi que la raison pour laquelle chaque enregistrement a échoué.
![Récapitulatif des enregistrements DNS importés](images/dns/import-records-summary.png)

### Exportation d'enregistrements
{:#export-dns-records}

Utilisez `Exportation d'enregistrements` pour créer une sauvegarde de votre fichier de zone ou exportez ce dernier pour l’utiliser avec un autre fournisseur DNS. Lorsque vous cliquez sur cette option de menu, les enregistrements sont téléchargés à l'emplacement spécifié par les paramètres de votre navigateur (généralement le dossier Téléchargements). Pour sélectionner un autre emplacement de dossier, modifiez les paramètres de votre navigateur afin qu'il vous invite à indiquer un emplacement pour chaque téléchargement. 
