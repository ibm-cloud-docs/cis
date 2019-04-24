---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Page Rules, web content, IBM CIS deployment

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Gestion de votre déploiement IBM CIS pour une meilleure fiabilité
{:manage-your-ibm-cis-deployment-for-optimal-reliability}

Pour atteindre une fiabilité optimale avec votre déploiement IBM CIS, vous pouvez définir une configuration DNS plus poussée, ainsi que des équilibreurs de charge globaux. Pour encore plus de fiabilité, utilisez nos règles de page pour vous assurer que votre contenu Web est bien distribué à vos clients, même si le serveur d'origine ou la mémoire cache rencontre un problème. Ce document présente des informations détaillées sur les meilleures pratiques en matière d'optimisation de la fiabilité de votre déploiement IBM CIS.

En règle générale, nos meilleures pratiques sont les suivantes :

 * Définir votre DNS pour tirer avantage des serveurs proxy IBM CIS et d'autres fonctionnalités
 * Utiliser un ou plusieurs équilibreurs de charge globaux pour répartir uniformément le trafic de votre site
 * Configurer des règles de page appropriées pour gérer vos options de mise en cache et autres

Chacun de ces éléments fournit des fonctionnalités que vous pouvez utiliser pour créer un déploiement CIS plus fiable.

Notez que l'interface CIS s'articule autour des sections de *sécurité*, de *fiabilité* et de *performances*. Le menu de navigation principal est présenté ci-dessous, avec les éléments de menu Equilibreurs de charge globaux et DNS développés :

![DNS navigation de gauche](images/cis-left-navigation.png)


## Configuration d'un DNS
{:#setting-up-dns}
 
 Pour commencer à configurer votre DNS, sélectionnez **/DNS** dans le menu de navigation, comme indiqué précédemment.
 
 Pour plus d'informations sur la configuration et la gestion de votre DNS à des fins de fiabilité, [voir ce document](/docs/infrastructure/cis?topic=cis-set-up-your-domain-name-system-dns-for-ibm-cis).


## Configuration des équilibreurs de charge globaux
{:#setting-up-glb}


Pour commencer à configurer vos équilibreurs de charge globaux, sélectionnez **Equilibreurs de charge globaux** dans le menu de navigation.

Pour plus d'informations sur la configuration et la gestion des équilibreurs de charge globaux, [voir ce document](/docs/infrastructure/cis?topic=cis-global-load-balancer-glb-concepts).

## Utilisation des règles de page pour augmenter la fiabilité
{:#using-page-rules-to-increase-reliability}

Vous trouverez ci-dessous certains paramètres de règle de page permettant d'atteindre une fiabilité maximale de votre site :

 * Serve Stale Content
 * Contrôle du cache d'origine
 * URL de redirection

## Serve Stale Content
{:#serve-stale-content}

Utilisez le paramètre de règle de page **Serve Stale Content** pour qu'une partie de votre site reste en ligne en cas de défaillance de votre serveur.

Avec le paramètre **Serve Stale Content**, lorsque votre serveur tombe en panne, IBM CIS distribue les pages à partir de notre cache, de sorte que vos visiteurs puissent consulter certaines des pages de votre site. Vos visiteurs voient un message en haut de la page les informant qu'ils sont en mode de navigation hors ligne. Le paramètre Serve Stale Content renvoie un statut HTTP 503, qui est également utilisé par un grand nombre d'autres applications. Lorsque votre serveur est à nouveau en ligne, IBM CIS repasse en mode de navigation standard de façon totalement transparente pour les utilisateurs.

Si IBM CIS ne dispose pas de la page demandée en mémoire cache, une page d'erreur s'affiche, informant vos visiteurs que la page du site Web à laquelle ils tentent d'accéder est hors ligne.

### Procédure de configuration du paramètre Serve Stale Content
{:#setting-up-serve-stale-content}
Pour activer le paramètre **Serve Stale Content**, suivez les étapes ci-dessous :

 * Utilisez le menu de navigation pour sélectionner Règles de page sous Performances.
 * Créez une règle de page avec le masque d'URL de votre domaine.
 * Ajoutez le paramètre **Serve Stale Content** avec le commutateur activé.
 * Sélectionnez Provisionner 1 ressource.

### Limitations du paramètre Serve Stale Content
{limitations-serve-stale-content}

 * Le paramètre **Serve Stale Content** met en cache les 10 premiers liens à partir de votre HTML racine, puis les premiers liens à partir de chacune de ces pages, et enfin les premiers liens à partir de chacune des pages suivantes. Cela signifie que seules quelques pages de votre site sont visibles si votre serveur d'origine tombe en panne.

 * Les sites récemment ajoutés ne sont pas associés à un cache important de leur site, ce qui signifie que le paramètre **Serve Stale Content** peut ne pas fonctionner si vous avez ajouté le site il y a quelques jours seulement.

 * CIS n'affiche pas le contenu privé ni ne gère l'envoi de formulaire (POST) en cas de panne de votre serveur. Les visiteurs voient une page `error on checkout` ou `items require a login to view`.

 * Pour déclencher le paramètre **Serve Stale Content**, votre serveur Web doit renvoyer un code d'erreur HTTP standard 502 ou 504 de dépassement de délai. Le paramètre Serve Stale Content fonctionne également lorsque nous ne parvenons pas à contacter votre origine (erreurs 521 & 523), lorsque les délais d'attente sont dépassés (522 & 524), lorsque des erreurs SSL (525 & 526) ou inconnues (520) se produisent. Le paramètre **Serve Stale Content** n'est pas déclenché pour les autres codes réponses HTTP, tels que 404, 500 ou 503, les erreurs de connexion à la base de données, les erreurs de serveur interne ou les réponses vides du serveur.

 * Le paramètre **Serve Stale Content** ne fonctionne pas si une règle de page "Tout mettre en cache" est activée avec une valeur "TTL cache de périphérie" inférieure à la fréquence de mise en cache car l'option "TTL cache de périphérie" entraîne la suppression du cache **Serve Stale Content** dans l'intervalle correspondant.

## Contrôle du cache d'origine
{:#origin-cache-control}
Le paramètre de règle de page **Contrôle du cache d'origine** permet de déterminer le contenu mis en cache à partir de votre origine ainsi que la fréquence de mise à jour du contenu, ce qui a une incidence sur la fiabilité et les performances. Par défaut, si aucun paramètre n'est modifié et qu'aucun en-tête empêchant la mise en cache n'est envoyé depuis votre serveur d'origine, IBM CIS met en cache tout le contenu statique avec certaines extensions. Ces types de contenus incluent les images, les feuilles de style CSS et JavaScript. La mise en cache est alors effectuée principalement pour des raisons de performances.

Pour configurer le paramètre **Contrôle du cache d'origine**, utilisez les règles de page afin d'activer certains en-têtes spécifiques susceptibles de fournir le comportement désiré à l'égard de chaque ressource de votre contenu. Pour savoir comment utiliser le paramètre **Contrôle du cache d'origine**, vous devez avoir certaines connaissances générales sur les règles de page et le comportement global de mise en cache pour CIS, que vous trouverez dans les sections qui suivent. Il existe généralement trois méthodes pour contrôler la mise en cache et l'option **Contrôle du cache d'origine** constitue la deuxième méthode.

La configuration du paramètre **Contrôle du cache d'origine** appelle des règles en mise en cache qui tendent à respecter rigoureusement les meilleures pratiques Internet et RFC, principalement en ce qui concerne la revalidation. Par exemple, le comportement par défaut de CIS lorsque `max-age=0` consiste à ne rien mettre en cache, alors que le paramètre **Contrôle du cache d'origine** va procéder à la mise en cache, mais toujours avec une revalidation.

### Procédure de configuration du paramètre Contrôle du cache d'origine
{:#setting-up-origin-cache-control}

 * Utilisez le menu de navigation pour sélectionner Règles de page sous Performances.
 * Créez une règle de page avec le masque d'URL qui fait référence à votre domaine.
 * Ajoutez le paramètre **Contrôle du cache d'origine** avec le commutateur activé.
 * Sélectionnez Provisionner 1 ressource.

### Priorité de règle de page
{:#page-rule-precedence}

Deux règles de page spécifiques sont prioritaires pour la mise en cache globale :

 * Si une règle de page a un **niveau de cache** défini sur `Ignorer`, les ressources qui correspondent à cette règle de page ne sont pas mises en cache. IBM CIS agit toujours comme un proxy, et les autres caractéristiques de performances restent actives. Cependant, votre contenu est extrait directement de votre serveur d'origine, au lieu d'être servi depuis notre cache. 

 * Si une règle de page a un **niveau de cache** défini sur `Tout mettre en cache`, les ressources qui correspondent à la règle de page sont mises en cache. **L'utilisation de ce paramètre de règle de page est l'unique façon de nous informer des ressources à mettre en cache au-delà de ce que nous considérons comme statique, notamment le langage HTML.**

Si aucune règle de page n'est définie, nous appliquons le mode de mise en cache `Standard`, qui est basé sur l'extension de la ressource. Nous ne mettons en cache que des ressources statiques. 

### En-têtes de contrôle du cache d'origine
{:#origin-cache-control-headers}

La deuxième façon de modifier le comportement de mise en cache d'IBM CIS consiste à utiliser des en-têtes de mise en cache à partir de l'origine. CIS applique ces paramètres, mais vous pouvez les ignorer en spécifiant le paramètre de règle de page **TTL cache de périphérie**. Les en-têtes à prendre en compte lorsque vous déterminez les ressources à mettre en cache à partir de votre origine sont les suivants :

 * Si l'en-tête **Cache-Control** est défini sur `private`, `no-store`, `no-cache` ou `max-age=0`, ou si la réponse comporte un cookie, IBM CIS ne met pas en cache la ressource. Sachant qu'il est préférable de ne pas mettre en cache les informations confidentielles, vous pouvez envisager d'utiliser l'un de ces en-têtes si besoin.

 * Si l'en-tête **Cache-Control** est défini sur `public` et que la valeur `max-age` est supérieure à 0, ou si les en-têtes `Expires` doivent être configurés à l'avenir, nous mettrons la ressource en mémoire cache.

**Remarque :** Comme précisé dans les règles RFC, le paramètre `Cache-Control: max-age` prend la priorité sur les en-têtes `Expires`. Si les deux sont définis et qu'ils sont contradictoires, le paramètre `max-age` l'emporte.

### Utilisation de l'en-tête 's-maxage'
{:#using-the-s-maxage-header}

La troisième façon de contrôler le comportement de mise en cache, ainsi que le comportement de mise en cache du navigateur consiste à utiliser l'en-tête de contrôle du cache `s-maxage`.

Normalement, nous respectons la directive `max-age` :

`Cache-Control: max-age=1000`

Mais si vous souhaitez indiquer un délai de mise en mémoire cache différent de celui du navigateur, nous pouvons utiliser `s-maxage`. Vous trouverez ci-dessous un exemple demandant à IBM CIS de mettre l'objet en mémoire cache pendant 200 secondes et au navigateur pendant 60 secondes.

`Cache-Control: s-maxage=200, max-age=60`

Fondamentalement, `s-maxage` est destiné à être suivi UNIQUEMENT par les proxy inverses (pour que le navigateur puisse l'ignorer) alors qu'IBM CIS donne la priorité à `s-maxage` s'il est présent. IBM CIS suit la valeur la plus élevée : le paramètre de cache du navigateur ou l'en-tête `max-age`.

### Récapitulatif sur les en-têtes de contrôle du cache et les règles de page à des fins de fiabilité
{:#summary-cache-control-headers-page-rules}

Pour résumer, vous trouverez ci-dessous les éléments principaux à prendre en considération pour une mise en cache fiable :

 * Vérifiez les en-têtes de mise en cache de votre origine pour vous assurer qu'il n'existe pas d'en-tête substitutif pour les ressources pouvant être mises en cache (`Cache-Control` et `Expires`).

 * CIS met toujours en cache le contenu statique par défaut, avec la valeur de durée de vie (TTL) suivante en fonction du code retour :

```
200 301    120m;
302 303    20m;
403        5m; for reliability
404        5m;
any        0s;
```

 * Pour mettre davantage de contenu en mémoire cache, créez une règle de page avec le paramètre **Niveau de cache** défini sur `Tout mettre en cache` à l'adresse URL souhaitée (si votre serveur Web renvoie une erreur 404 au moment de demander l'URL, le résultat est mis en cache pendant 5 minutes seulement).

 * Pour empêcher la mise en cache sur une adresse URL, créez une règle de page avec le paramètre **Niveau de cache** défini sur `Ignorer`.


## URL de redirection
{:#forwarding-url}

Pour garantir la haute disponibilité de votre contenu, créez une règle de page avec le paramètre **URL de redirection** utilisé, en cas d'indisponibilité de votre site.

Lorsque vous activez le paramètre **URL de redirection**, tous les autres paramètres sont désactivés, car vous envoyez l'ensemble du trafic vers une autre adresse URL.{:note}

### Procédure de configuration du paramètre URL de redirection
{:#setting-up-forwarding-url}

 * Utilisez le menu de navigation pour sélectionner Règles de page sous Performances.
 * Créez une règle de page avec le masque d'URL qui fait référence à votre domaine.
 * Ajoutez le paramètre **URL de redirection**.
 * Sélectionnez le type d'acheminement et indiquez l'URL de destination.
 * Sélectionnez Provisionner 1 ressource.

### Exemples de réacheminement
{:#forwarding-examples}

Supposons que vous voulez faciliter l'accès à une URL de type :

    *www.example.com/+

    *example.com/+

Ce masque correspond à : 

    http://example.com/+
    http://www.example.com/+
    https://www.example.com/+
    https://blog.example.com/+
    https://www.blog.example.com/+
    Etc...

Il ne correspond pas à :

    http://www.example.com/blog/+  [répertoire supplémentaire avant le +]
    http://www.example.com+  [pas de barre oblique à la fin]


Une fois que vous avez créé le masque qui correspond à ce que vous souhaitez, ajoutez le paramètre **URL de redirection**, choisissez le type de transfert et indiquez l'URL de destination. Exemple :

    https://plus.google.com/yourid

Sélectionnez Provisionner 1 ressource. En quelques secondes, toutes les demandes correspondantes au masque sont acheminées vers la nouvelle URL avec la redirection spécifiée.

### Options de transfert avancées
{:#advanced-forwarding-options}

Si vous utilisez une redirection de base, telle que le transfert du domaine racine vers `www.yourdomain.com`, vous perdez tous les autres éléments de l'URL. Par exemple, vous définissez le masque :

    example.com

Et vous le transférez vers :

    `http://www.example.com`

Mais si quelqu'un ajoute :

    `example.com/some-particular-page.html`

Il est alors redirigé vers :

    `www.example.com`

et non vers

    `www.example.com/some-particular-page.html`

La solution consiste à utiliser des variables. Chaque caractère générique correspond à une variable pouvant être référencée dans l'adresse de réacheminement. Les variables sont représentées par un signe `$` suivi d'un chiffre. Pour faire référence au premier caractère générique, vous utilisez `$1`, au deuxième caractère générique, vous utilisez `$2`, et ainsi de suite. Pour corriger le transfert de la racine vers `www` dans notre exemple précédent, utilisez le même masque :

    `example.com/*`

Configurez ensuite l'URL suivante pour le trafic à transférer : 

    `http://www.example.com/$1`

Dans ce cas, si quelqu'un accède à :

    `example.com/some-particular-page.html`

Il est redirigé vers :

    `http://www.example.com/some-particular-page.html`
