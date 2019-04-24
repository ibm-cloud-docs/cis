---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Use Page Rules, Page Rule

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Utilisation des règles de page
{:#use-page-rules}

Une règle de page indique certains paramètres et valeurs que vous pouvez appliquer à un masque d'URL spécifique qui fait référence à votre domaine. Les règles de page vous aident à gérer la sécurité, les performances et la fiabilité de votre site sur la base de chaque URL individuelle. Le tableau ci-dessous présente les règles de page disponibles pour tous les clients, leurs comportements associés et les considérations particulières que vous devez garder à l'esprit avant de les utiliser.

## Sécurité
{:#page-rules-security}

| **Paramètre** | **Comportement** | **Considérations** |
|-----------|----------|----------------|
|**Contrôle d'intégrité navigateur**|Recherche les en-têtes HTTP connues pour être la cible des spammeurs, et refuse l'accès à votre page. Il bloque également les visiteurs qui ne possèdent pas d'agent utilisateur ou qui ajoutent un agent utilisateur non standard (technique généralement utilisée par les bots, moteurs d'exploration ou API malveillants). | |
|**Désactiver la sécurité**|Désactive les fonctionnalités suivantes : <ul><li>Brouillage d'e-mail</li> <li>Exclusions côté serveur</li> <li>WAF</li></ul>|Si une règle est définie pour désactiver la sécurité et une autre pour activer le pare-feu d'application Web (WAF), la règle WAF est prioritaire, quel que soit l'ordre dans lequel elles apparaissent.|
|**Brouillage d'e-mail**|Active ou désactive le brouillage d'e-mail. | |
|**En-tête de géolocalisation IP**|Inclut le code pays de l'emplacement géographique du visiteur dans toutes les demandes vers votre site Web. Ces informations sont accessibles dans l'en-tête HTTP `CF-IPCountry`. | |  
|**Niveau de sécurité**|Indique le niveau du score de menace avant lequel afficher une page de demande d'authentification. Ce paramètre peut être utilisé de manière que le **Mode défense** soit toujours activé lorsque les visiteurs accèdent à votre site. | |
|**Exclusions côté serveur **|Active ou désactive les exclusions côté serveur.  | |
|**TLS**|Contrôle le mode TLS utilisé. | |
|**WAF**|Active ou désactive le pare-feu d'application Web (WAF). | |  
|**Réécritures HTTPS automatiques**|Active ou désactive les réécritures HTTPS automatiques.  | |
|**Chiffrement opportuniste**|Active ou désactive le chiffrement opportuniste.  | |
|**Armure tromperie du cache**|Active ou désactive l'armure tromperie du cache.  | |
|**Toujours utiliser HTTPS**|Convertit n'importe quelle adresse URL `http://` en une adresse `https://` en créant une redirection URL `301`.|L'utilisation de ce paramètre désactive la configuration de tous les autres paramètres de la règle, car IBM CIS force la redirection `HTTPS` de la demande, qui devient alors une nouvelle demande qui est ensuite évaluée par rapport aux règles de page. |
|**En-tête IP client réel**|CIS envoie l'adresse IP de l'utilisateur final dans l'en-tête `True-Client-IP`.   |Enterprise uniquement |

## Performances
{:#page-rules-performance}

| **Paramètre** | **Comportement** | **Considérations** |
|-----------|----------|----------------|
|**TTL cache navigateur**|Indique la durée de validité des ressources mises en cache par les navigateurs client. | |
|**Ignorer le cache sur cookie**|Distribue un objet mis en cache sauf si un cookie est spécifique à un nom, par exemple, et distribue une version en mémoire cache de la page d'accueil sauf si un cookie `SessionID` indique que le client est connecté et devrait par conséquent voir du contenu personnalisé. | |
|**Niveau de cache**|**Ignorer** - Les ressources qui correspondent à la règle de page ne sont pas mises en cache.<br>**Aucune chaîne de requête** - Seules sont distribuées les ressources issues du cache lorsqu'il n'y a aucune chaîne de requête.<br>**Ignorer la chaîne de requête** - La même ressource est distribuée peu importe la chaîne de requête.<br>**Standard** - Une ressource différente est distribuée chaque fois que la chaîne de requête est modifiée.<br> **Tout mettre en cache** - Les ressources qui correspondent à la règle de page sont mises en cache.|Par défaut, le contenu HTML n'est pas mis en cache. Une règle de page destinée à mettre en mémoire cache le contenu HTML statique doit être écrite. |
|**TTL cache de périphérie**|Indique la durée de conservation des fichiers dans le cache IBM CIS. |Ce paramètre est facultatif lorsque vous spécifiez le niveau de cache. |
|**Outrepasser la résolution**|Modifiez l'URL ou l'adresse IP que résout la demande correspondant à la règle de page. ||
|**Cache sur cookie**|Appliquez l'option `Tout mettre en cache` (paramètre `Niveau de cache`) en fonction d'une correspondance d'expression régulière avec un nom de cookie. Si vous ajoutez ce paramètre et sélectionnez `Ignorer le cache sur cookie` pour la même règle de page, l'option `Cache sur cookie` est prioritaire sur `Ignorer le cache sur cookie`. |Enterprise uniquement |
|**Désactiver les performances**|Désactiver :<ul><li>`Minimiser le contenu Web`</li><li>`Optimisation du chargement d'image`</li><li>`Optimisation de la taille d'image`</li><li>`Optimisation du chargement de script`</li></ul> |Enterprise uniquement |
|**Minimiser le contenu Web**|Réduisez les fichiers HTML, CSS et/ou JavaScript en supprimant tous les caractères inutiles de ces fichiers. |Enterprise uniquement |
|**Optimisation du chargement d'image**|Améliore le temps de chargement des pages contenant des images basées sur la connexion réseau et le type de périphérique avec : <ul><li>**Virtualisation des images** - Remplace les images avec des images réservées de faible résolution ayant les mêmes dimensions que les images originales (y compris les images tierces). Une fois que la page est entièrement rendue, les images en pleine résolution sont ensuite chargées lentement (définition de la priorité des images dans la fenêtre du navigateur). Ce processus permet un rendu rapide des pages et minimise la redistribution du navigateur. </li><li>**Rationalisation des demandes** - Combine plusieurs demandes d'images individuelles émanant du réseau en une seule demande.</li></ul> |Enterprise uniquement |
|**Optimisation de la taille d'image**|Réduit la taille du fichier d'image en supprimant les métadonnées (date et heure, fabricant et modèle de l'appareil photo, etc.), et en compressant les images lorsque cela est possible. Des tailles de fichier réduites signifient des temps de chargement plus rapides pour les images et les pages Web. |Enterprise uniquement |
|**Tri des chaînes de requête**|Traite les fichiers avec les mêmes chaînes de requête que le même fichier en cache, quel que soit l'ordre des chaînes de requête. |Enterprise uniquement |
|**Mise en tampon des réponses**|Active ou désactive la mise en mémoire tampon des réponses du serveur d'origine. Par défaut, CIS envoie des paquets au client dès que nous les recevons. L'activation de la mise en mémoire tampon des réponses signifie que CIS attend jusqu'à ce qu'il ait l'intégralité du fichier avant de le transférer à l'utilisateur final. |Enterprise uniquement |
|**Optimisation du chargement de script**|Améliore les temps de coloriage en chargeant de manière asynchrone les Javascripts, y compris les scripts tiers, afin qu'ils ne bloquent pas le rendu du contenu de vos pages. |Enterprise uniquement |

## Fiabilité
{:#page-rules-reliability}

| **Paramètre** | **Comportement** | **Considérations** |
|-----------|----------|----------------|
|**Serve Stale Content**|Conserve une version limitée du site en ligne si le serveur tombe en panne. |Pour plus d'informations, voir [Gestion de votre déploiement IBM CIS pour une meilleure fiabilité](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability) |
|**Contrôle du cache d'origine**|Détermine le contenu mis en cache à partir de l'origine, ainsi que la fréquence de mise à jour du contenu. |Pour plus d'informations, voir [Gestion de votre déploiement IBM CIS pour une meilleure fiabilité](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability) |
|**URL de redirection** |Adresse URL à utiliser en cas d'indisponibilité du site. | Cette option désactive la configuration de tous les autres paramètres, puisque vous acheminez la demande ailleurs. Pour plus d'informations, voir [Gestion de votre déploiement IBM CIS pour une meilleure fiabilité](/docs/infrastructure/cis?topic=cis-manage-your-ibm-cis-deployment-for-optimal-reliability)|
|**Outrepasser l'en-tête d'hôte**|Remplace l'en-tête de l'hôte pour l'URI correspondant à la règle de page par la valeur spécifiée. Cette option est couramment utilisée pour le contenu hébergé dans un compartiment S3. |
|**Désactiver les applis**|Désactive toutes les applications CIS. |Enterprise uniquement |
|**Ignorer la page d'erreur d'origine**|Désactive les pages d'erreur CIS qui se déclencheraient pour les problèmes envoyés à partir du serveur d'origine et affiche les pages d'erreur définies à l'origine. |Enterprise uniquement ||

## Masques d'URL de règle de page
{:#page-rule-url-patterns}

Une règle de page sera appliquée à un masque d'URL spécifique, au format suivant :

`<scheme>://<hostname><:port>/<path>`

Un exemple d'utilisation de chaque composant serait :

`https://www.example.com:80/image.png`

Les composants *scheme* et *port* sont facultatifs. Si le schéma est omis, il couvrira à la fois les protocoles `http://` et `https://`. Si le port n'est pas spécifié, la règle s'appliquera à tous les ports. Vous pouvez utiliser le caractère de recherche générique ‘*’ dans votre modèle de règle pour renvoyer une série de modèles similaires et non pas un seul modèle.

Les trois points importants à retenir concernant les règles de page sont les suivants :

 * Une seule règle de page prendra effet sur une requête donnée.
 * L'ordre de priorité des règles de page est établi de haut en bas.
 * Lorsqu'une adresse URL correspond à une règle, seule cette règle sera appliquée. Autrement dit, si une règle de page a déjà été déclenchée sur une requête, aucune des règles suivantes ne sera appliquée même si elle correspond au masque d'URL. D'une manière générale, nous recommandons de classer les règles de la _plus spécifique_ à la _moins spécifique_.

Vous pouvez désactiver les règles de page, auquel cas elles seront sans effet. Toutefois, elles figureront toujours dans la liste et pourront toujours être modifiées. Lorsque vous placez le commutateur sur **Désactivé**, une règle de page est créée avec le statut désactivé.

Pour plus d'informations, voir [Utilisation des règles de page avec la mise en cache](/docs/infrastructure/cis?topic=cis-use-page-rules-with-caching).
