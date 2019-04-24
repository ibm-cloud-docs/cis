---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Use Page Rules, standard cache levels, Custom Caching Sets

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Utilisation des règles de page avec la mise en cache
{:#use-page-rules-with-caching}

Les règles de page vous permettent d'accomplir diverses actions en fonction de l'URL de la page, notamment la création de réacheminements, l'optimisation du comportement de mise en cache, ou l'activation et la désactivation des services.

Une règle de page s'applique à un masque d'URL donné au format suivant :

`<scheme>://<hostname><:port>/<path>`

Exemple :

`https://www.example.com:80/image.png`

Les composants `scheme` et `port` sont facultatifs. Si le composant `scheme` est omis, le format accepte les protocoles `http://` et `https://`. Si le composant `port` n'est pas spécifié, la règle s'applique à tous les ports. Vous pouvez utiliser le caractère de recherche générique `*` dans votre modèle de règle pour renvoyer une série de modèles similaires.

**Points à retenir concernant les règles de page :**

 * Une seule règle de page s'applique par requête.
 * L'ordre de priorité des règles de page est établi de haut en bas. Lorsqu'une adresse URL correspond à une règle, seule cette règle est appliquée. Autrement dit, si une règle de page a déjà déclenché une requête, aucune des règles suivantes n'est appliquée même si elle correspond au masque d'URL. 
 * En règle générale, nous recommandons de classer les règles de la plus spécifique à la moins spécifique.
 * Vous pouvez désactiver les règles de page, auquel cas elles apparaîtront toujours dans la liste et seront toujours modifiables, mais elles ne seront pas actives. Lorsque vous placez le commutateur *Activé* sur la position "Off", une règle de page est créée avec le statut désactivé.


## Transfert (redirection d'URL)
{:#forwarding-url-redirection}

Redirige une adresse URL vers une autre à l'aide de la redirection HTTP 301 ou 302. Vous pouvez référencer le contenu d'une section d'adresse URL pour laquelle une correspondance avec le caractère générique est établie en utilisant la syntaxe `$X`. Le signe `X` indique l'index d'un Glob dans le modèle, et `$1` est remplacé par le premier caractère générique correspondant, `$2` par le deuxième, et ainsi de suite.

Prenons la règle suivante comme exemple :

![image](images/url-redirection-example.png)

Une demande envoyée à `www.example.com/stuff/things` est redirigée vers `http://example.com/stuff/things`.

Veillez à ne pas créer de redirection pour laquelle le domaine pointe vers lui-même. Ceci aurait pour conséquence de générer une erreur de redirection infinie, et les adresses URL ne seraient pas résolues.
{:note}


## Redirection vers HTTPS
{:#redirecting-to-https}

Si vous voulez rediriger vos visiteurs vers HTTPS, utilisez plutôt le paramètre **Toujours utiliser HTTPS** :

![image2](images/url-matching-patterns.png)


## Mise en cache personnalisée
{:#custom-caching}

Définit le comportement de mise en cache pour toutes les adresses URL qui correspondent au modèle de règle de page via nos niveaux de cache standard. La configuration du paramètre **Niveau de cache** sur **Tout mettre en cache** met en cache l'ensemble du contenu, même s'il ne s'agit pas de l'un de nos types de fichiers statiques par défaut. La configuration du paramètre **Niveau de cache** sur **Ignorer** empêche la mise en cache sur cette URL.

Lorsque vous configurez le niveau de mise en cache à l'aide des règles de page, vous pouvez définir une valeur **TTL cache de périphérie**, qui contrôle la durée de conservation des fichiers dans la mémoire cache.

La valeur **TTL cache navigateur** indique la durée de validité des ressources mises en cache par les navigateurs client. Si un navigateur refait une demande de ressource et que la valeur TTL est toujours valide, le navigateur reçoit une réponse `HTTP 304 (Not Modified)`. Vous pouvez définir des valeurs TTL comprises entre 30 minutes et un an.

Tous les comportements de mise en cache par défaut ne sont pas strictement compatibles RFC. La configuration du paramètre **Contrôle du cache d'origine** à l'aide des règles de page fait appel à un nouvel ensemble de règles de mise en cache qui va chercher à mieux respecter les demandes RFC, surtout en ce qui concerne la revalidation. Par exemple, notre comportement par défaut avec `max-age=0` consiste à ne rien mettre en cache, alors que le paramètre **Contrôle du cache d'origine** va procéder à la mise en cache, mais toujours avec une revalidation.

L'exemple suivant définit une règle de page visant à mettre en cache tous les éléments situés dans le dossier `/images`. Les ressources mises en cache expirent dans un délai de 30 minutes dans le navigateur de l'utilisateur, et dans un délai de 1 jour dans les centres de données IBM CIS :

![image3](images/url-example.png)

L'option **Serve Stale Content** sert des pages de notre cache, même lorsque votre serveur tombe en panne. Les visiteurs voient une version limitée de votre site, avec un message indiquant qu'ils sont en mode de navigation hors connexion.  

Cette fonctionnalité renvoie le statut HTTP 503. Lorsque les serveurs sont à nouveau en ligne, CIS permet aux visiteurs de naviguer de manière transparente. 

Si la page demandée ne se trouve pas dans le cache, le visiteur voit une page d'erreur qui l'informe que la page demandée est hors connexion. Si une règle de page **Tout mettre en cache** est activée avec des délais d'expiration définis inférieurs à la fréquence de mise en cache, le contenu **Serve Stale Content** est purgé dans l'intervalle correspondant.{:note}
