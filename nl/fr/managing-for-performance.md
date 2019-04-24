---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Page Rule Use, Cache-Tag Purge, web content

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Gestion de votre déploiement CIS pour de meilleures performances
{:#manage-your-cis-deployment-for-best-performance}

IBM Cloud Internet Services (CIS) peut offrir la meilleure expérience possible à vos clients en optimisant vos images et en stockant votre contenu Web le plus près possible de vos utilisateurs finaux. Votre contenu est chargé à partir de serveurs d'équilibrage des charges avec proxy (ce qui permet de réduire le temps d'attente).

Grâce à IBM CIS, vous pouvez améliorer encore les performances de votre site en suivant les meilleures pratiques pour accélérer le temps de chargement de votre contenu Web. Vous trouverez ci-dessous certaines valeurs recommandées pour l'amélioration des performances de votre contenu Web dans CIS.

**Recommandations et meilleures pratiques :**

 * Mettez le plus de contenu Web statique et semi-statique en cache
 * Pour le contenu géré par des événements, purgez le cache à l'aide de l'API
 
## Meilleure pratique 1 : Mettez le plus de contenu statique et semi-statique en cache
{:#best-practice-cache-static-content}

  * Activez la case **Tout mettre en cache** pour les pages Web HTML statiques.
  * Utilisez avec modération la valeur de **durée de vie (TTL)** pour le contenu modifié occasionnellement

### Utiliser avec modération les valeurs TTL pour le contenu modifié occasionnellement
{:#utilize-conservative-ttl}

Si le contenu est rarement modifié, définissez une valeur TTL modérée de manière à utiliser le plus possible notre cache. S'il existe un pourcentage élevé de demandes de revalidation , vous pouvez augmenter les valeurs de durée de vie de votre contenu sans affecter négativement vos clients. En utilisant plus efficacement le cache, vous augmentez les performances grâce à des revalidations moins fréquentes.

### Comment savoir si des éléments sont mis en cache ?
{:#how-do-i-tell-if-items-are-being-cached}

IBM CIS ajoute l'en-tête de réponse `CF-Cache-Status` lorsqu'il tente de mettre un objet en cache. Si la mise en cache est réussie, la valeur de cet en-tête indique son statut avec l'un des mots-clés suivants :

* **MISS :** L'actif n'est pas encore en mémoire cache ou la valeur de durée de vie a expiré (à savoir, elle a atteint l'âge maximum de contrôle du cache 0).
* **HIT :** L'actif a été distribué à partir du cache.
* **EXPIRED :** Cet actif a été distribué à partir du cache, mais la prochaine demande nécessitera une revalidation.
* **REVALIDATED :** L'actif a été distribué à partir du cache. La valeur de durée de vie (TTL) a expiré, mais une demande `If-Modified-Since` envoyée à l'origine indique que l'actif n'a pas subi de modification. Par conséquent, la version placée en cache est considérée comme étant toujours valide.

## Meilleure pratique 2 : Pour le contenu géré par des événements, utilisez l'API pour purger votre cache
{:#best-practice-api-purge-cache}

Par exemple, chaque fois qu'un nouveau billet est publié sur votre blog, vous pouvez facilement purger le cache CIS en utilisant une commande API. Il est fréquent d'avoir du contenu géré par des événements, c'est pourquoi notre solution permet de vérifier facilement qu'aucun contenu obsolète n'atteint vos utilisateurs. Les commandes permettant de purger le cache immédiatement sur l'ensemble de notre réseau mondial sont répertoriées ci-dessous. Vous pouvez soit utiliser notre application de mise en cache, soit utiliser l'API.

  * Purger le cache à l'aide d'une balise cache
  * Purger la totalité du cache
  * Purger le cache par règle de page
  * Utiliser les fonctions de mise en cache avancées

### Purger le cache à l'aide d'une balise cache
{:#purge-cache-by-cache-tag}

Les balises cache vous permettent de définir les compartiments de contenu que vous souhaitez purger. C'est une excellente façon de combiner les objets qui sont généralement modifiés ensemble. Par exemple, un article de blog HTML et son contenu d'image peuvent être balisés ensemble. Le contenu mobile uniquement peut également être regroupé à l'aide des balises cache, de sorte que vous puissiez tout purger lorsque vous envoyez une nouvelle mise à jour par commande push vers votre domaine mobile.

### Purger la totalité du cache
{:#purge-cache-globally}

Vous avez également la possibilité de forcer la totalité du cache à revalider. Vous pouvez réinitialiser tous les objets stockés dans notre cache de sorte que chaque demande soit acheminée vers le serveur d'origine.

### Purger le cache par règle de page
{:#purge-cache-by-page-rule}

Les règles de page vous permettent de vider complètement le cache basé sur une expression régulière. Vous pouvez utiliser une règle de page prédéfinie et revalider l'ensemble des résultats en fonction de cette règle de page. Vous pouvez créer jusqu'à 50 règles de page par page.

### Utiliser les fonctions de mise en cache avancées
{:#use-advanced-caching-features}

**Ignorer le cache sur cookie :** Configurée dans une règle de page, cette fonctionnalité vous permet de distribuer un objet mis en cache sauf si un cookie existe pour un nom spécifique. Par exemple, vous pouvez distribuer une version en mémoire cache de la page d'accueil sauf si un cookie `SessionID` indique que le client est connecté et devrait par conséquent être présenté avec du contenu personnalisé.
