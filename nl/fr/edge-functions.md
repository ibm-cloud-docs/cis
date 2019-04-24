---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: edge functions beta, edge functions

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Fonctions Edge (Bêta) 
{: #edge-functions}

Les fonctions Edge de CIS vous permettent de créer des applications ou de modifier des applications existantes, sans avoir à configurer ou à entretenir une infrastructure, en utilisant un environnement d'exécution sans serveur. Les fonctions Edge peuvent être définies et téléchargées à la périphérie du cloud pour traiter les demandes avant qu'elles n'atteignent l'origine. Les fonctions Edge de CIS peuvent être utilisées pour modifier les demandes et les réponses HTTP, faire des demandes parallèles ou générer des réponses à partir de la périphérie du cloud. 

## Fonctionnement des fonctions Edge
{: #how-edge-functions-work}

Les fonctions Edge associent des **actions** à des URI basés sur un domaine défini. Cette association s'appelle un **déclencheur**. Les demandes entrantes sur votre site seront interceptées à la périphérie du cloud et comparées aux déclencheurs de votre compte ou de votre domaine. Si l'URL de la demande correspond à l'URI du déclencheur, l'action associée au déclencheur est exécutée. 

Les fonctions Edge sont calquées sur les [Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) disponibles dans les navigateurs Web modernes et utilisent la même API chaque fois que cela est possible. 

L'API Service Worker vous permet d'intercepter toute demande adressée à votre site. Une fois que votre JavaScript traite la demande, vous pouvez choisir de créer autant de sous-demandes que vous le souhaitez sur votre site ou sur d’autres sites, et de renvoyer, en fin de compte, à votre visiteur la réponse que vous souhaitez. 

Contrairement aux Service Workers standard, les fonctions Edge s’exécutent sur les serveurs Edge de CIS, et non sur le navigateur de l’utilisateur. Cela signifie que vous pouvez être sûr que votre code sera exécuté dans un environnement sécurisé où les clients malveillants ne pourront pas le contourner. Cela signifie également que l'utilisateur n'a pas besoin d'utiliser un navigateur moderne prenant en charge les Service Workers. Vous pouvez même intercepter les demandes de clients d'API qui ne sont pas du tout des navigateurs. 

En interne, les fonctions Edge utilisent le même moteur JavaScript V8 que celui utilisé dans le navigateur Google Chrome pour exécuter les Service Workers sur notre infrastructure. V8 compile dynamiquement votre code JavaScript en un code machine ultra-rapide, le rendant très performant. Cela permet à votre code de s'exécuter en quelques microsecondes et à notre périphérie d'exécuter plusieurs milliers de scripts par seconde. 

Bien que les fonctions Edge utilisent la version 8, elles n'utilisent pas Node.js. Les API JavaScript dont vous pouvez disposer dans les Service Workers sont implémentées directement par nous. L'utilisation directe de la version 8 permet au code de s'exécuter plus efficacement, avec les contrôles de sécurité nécessaires pour protéger les clients et l’infrastructure. 


## Actions
{: #edge-functions-actions}

Les actions sont écrites en JavaScript et nécessitent un programme d'écoute d'événement pour répondre à un événement déclencheur. Les actions n'affectent pas votre trafic sauf si elles sont utilisées par un déclencheur. 

### Forfait Enterprise et forfait Standard
{: #edge-functions-enterprise-v-standard-plans}

Les forfaits Standard comportent au maximum une action. Un nom identique à celui de votre domaine est attribué à l'action. Vous pouvez remplacer votre action en téléchargeant un autre fichier ou mettre à jour votre action à l'aide de l'éditeur de code. Le téléchargement d'un autre fichier supprime l'action existante. 

Les forfaits Enterprise permettent de télécharger un nombre illimité de scripts. Ces scripts peuvent avoir des noms uniques. 

### Création d'actions
{: #edge-functions-create-actions}

Sélectionnez **Créer** pour ajouter une action à l'aide de l'éditeur de code. Avec les forfaits Enterprise, entrez un nom pour votre action. Avec les forfaits Standard, le nom n'est pas modifiable et est défini d'après le nom de votre domaine. Après avoir ajouté votre code Javascript, sélectionnez **Sauvegarder** pour créer votre action. 

### Téléchargement d'actions
{: #edge-functions-upload-actions}

Utilisez le bouton **Télécharger** pour télécharger un fichier Javascript. Dans les forfaits Enterprise, le nom de l'action est le nom du fichier. Dans les forfaits Standard, le nom de l'action est défini d'après le nom de votre domaine. 

Le téléchargement ou la création d'une action portant le même nom qu'une action existante entraîne le remplacement de l'action existante. Renommez le fichier d'action avant le téléchargement ou entrez un nom unique dans l'entrée de texte lors de la création pour éviter ce problème. {:note}

### Edition d'actions
{: #edge-functions-edit-actions}

La sélection d'une action ouvre l'action dans l'éditeur pour modification. Chaque fois que vous enregistrez vos modifications, l'action est téléchargée à la périphérie du nuage. Après la mise à jour, sélectionnez **Sauvegarder**. Si l'action est utilisée, les modifications prennent effet immédiatement.  

### Suppression d'actions
{: #edge-functions-delete-actions}

Supprimez une action en cliquant sur l'icône de **suppression** dans le tableau **Actions**. Une action ne peut pas être supprimée en cours d'utilisation. Pour supprimer l'action, supprimez-la d'abord des déclencheurs. La colonne **Utilisations** indique le nombre de déclencheurs associés à cette action. La suppression est irréversible.


### Déclencheurs associés
{: #edge-functions-associated-triggers}

Ajoutez un déclencheur et associez-le à une action. 

### Limitations connues des fonctions Edge 
{: #edge-functions-known-limitations}

Chargement d'une action portant le même nom qu'une action existante. L'action existante est écrasée. Renommez le fichier d'action avant le téléchargement pour éviter ce problème. 


## Déclencheurs
{: #triggers}

### A propos des déclencheurs
{: #about-triggers}

Les déclencheurs (itinéraires) déterminent le routage du trafic du domaine vers les actions. Les déclencheurs associent certains masque d'URL, basés sur un domaine du compte, à une action prédéfinie. L'URL doit contenir le domaine, mais il peut contenir des caractères génériques comme préfixe du domaine ou à la fin du chemin. Si aucun chemin n'est indiqué sur le masque, une barre oblique `/` est ajoutée implicitement. Le masque d'URL ne peut pas contenir de caractères génériques infixe ni de paramètres de requête. 

Vous devez ajouter un domaine pour ajouter des déclencheurs. Vous pouvez ajouter des déclencheurs sans avoir d'actions. 

### Ajout de déclencheurs
{: #add-triggers}

Accédez à l'onglet **Déclencheurs** et cliquez sur **Ajouter un déclencheur**. Entrez un masque d'URL et sélectionnez une action dans la liste des actions existantes.  

Pour une action, vous pouvez également sélectionner **Eviter les fonctions Edge**. Cela permet au chemin du déclencheur de rester actif, mais évite d'utiliser des actions de Fonctions Edge. Par exemple, il existe une action appelée `my-function` et un déclencheur avec le chemin `beta.cistest-load.com/*`. Si le chemin d'accès `beta.cistest-load.com/data` ne doit pas utiliser l'action `my-function`, créez un autre déclencheur avec le chemin d'accès `beta.cistest-load.com/data` et l'option **Eviter les fonctions Edge**. Cela permet au chemin `beta.cistest-load.com/data` de rester actif sans utiliser l'action `my-function`.

### Edition de déclencheurs
{: #edit-triggers}

Mettez à jour un déclencheur à l'aide de l'option de menu dans la ligne du tableau correspondant à un déclencheur sélectionné. Après la mise à jour, sélectionnez **Sauvegarder**. 

### Suppression de déclencheurs
{: #delete-triggers}

Supprimez un déclencheur à l'aide de l'option de menu dans la ligne du tableau correspondant à un déclencheur sélectionné. Cette action ne peut pas être annulée.


## Cas d'utilisation
{: #edge-functions-use-cases-examples}

Ces exemples servent uniquement à des fins de démonstration et ne sont pas destinés à être utilisés en production. {:important}
* [Tests A/B](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#ab-testing)
* [Ajout d'un en-tête de réponse](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#add-response-header)
* [Agrégation de plusieurs demandes](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#aggregate-multiple-requests)
* [Routage conditionnel](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#conditional-routing)
* [Protection des liens dynamiques](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#hot-link-protection)
* [Réponses sans origine](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#originless-responses)
* [Demandes POST](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#post-requests)
* [Définition d'un cookie](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#setting-cookies)
* [Demandes signées](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#signed-requests)
* [Réponses en continu](/docs/infrastructure/cis?topic=cis-edge-functions-use-cases-beta-#streaming-responses)
