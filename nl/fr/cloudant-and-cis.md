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


# Accès à votre base de données Cloudant via IBM Cloud Internet Services 
{: #access-cloudant-through-cis}

Procédez comme suit pour accéder à votre base de données Cloudant via IBM Cloud Internet Services (CIS). 

## Avant de commencer
{: #access-cloudant-through-cis-begin}

Ces instructions supposent que vous avez déjà ajouté un domaine à CIS, comme indiqué dans la page [Démarrage](/docs/infrastructure/cis?topic=cis-getting-started-with-ibm-cloud-internet-services-cis-).

### Etape 1 : Ajout de votre domaine CIS au partage de ressources d'origine croisée (CORS) 
{: #access-cloudant-through-cis-step1}

* Accédez à votre base de données Cloudant et ouvrez la page `Compte` -> `CORS`.
* Ajoutez votre domaine CIS à la zone de saisie des domaines d'origine. Par exemple, `https://cloudant.test.foo.com`.

### Etape 2. Configuration de CIS pour qu'il pointe vers votre base de données Cloudant 
{: #access-cloudant-through-cis-step2}

* Accédez au tableau de bord CIS et créez un équilibreur de charge ou un enregistrement DNS qui pointe vers le nom d'hôte de votre base de données Cloudant. Par exemple, `https://cloudant.test.foo.com` -> `111-222-333-444-555-test.cloudant.com`.
* Activez le `proxy` pour l’enregistrement DNS ou l’équilibreur de charge.


### Etape 3. Création d'une règle de page pour définir la zone Outrepasser l'en-tête d'hôte 
{: #access-cloudant-through-cis-step3}

* Dans le tableau de bord CIS, accédez à `Performances` -> `Règles de page`.
* Créez une règle de page pour l'URL souhaitée, par exemple, `https://cloudant.test.foo.com/*`.
* Sélectionnez le paramètre Comportement de la règle, `Outrepasser l'en-tête d'hôte`.
* Définissez le nom d'hôte de la base de données Cloudant, par exemple, `111-222-333-444-555-test.cloudant.com`.

Pour plus d'informations sur Cloudant, voir la [documentation Coudant](/docs/services/Cloudant?topic=cloudant-getting-started-with-cloudant).
