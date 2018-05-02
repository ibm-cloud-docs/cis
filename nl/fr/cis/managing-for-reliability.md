---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Gestion de votre déploiement IBM CIS pour une meilleure fiabilité

Pour atteindre une fiabilité optimale avec votre déploiement IBM CIS, vous pouvez définir une configuration DNS plus poussée, ainsi que des équilibreurs de charge globaux. Pour encore plus de fiabilité, utilisez nos règles de page pour vous assurer que votre contenu Web est bien distribué à vos clients, même si le serveur d'origine ou la mémoire cache rencontre un problème. Ce document présente des informations détaillées sur les meilleures pratiques en matière d'optimisation de la fiabilité de votre déploiement IBM CIS.

En règle générale, nos meilleures pratiques sont les suivantes :

 * Définir votre DNS pour tirer avantage des serveurs proxy IBM CIS et d'autres fonctionnalités
 * Utiliser un ou plusieurs équilibreurs de charge globaux pour répartir uniformément le trafic de votre site
 * Configurer des règles de page appropriées pour gérer vos options de mise en cache et autres

Chacun de ces éléments fournit des fonctionnalités que vous pouvez utiliser pour créer un déploiement CIS plus fiable.

Notez que l'interface CIS s'articule autour des sections de *sécurité*, de *fiabilité* et de *performances*. Le menu de navigation principal est présenté ci-dessous, avec les éléments de menu Equilibreurs de charge globaux et DNS développés :

![DNS navigation de gauche](images/cis-left-navigation.png)


## Configuration d'un DNS
 
 Pour commencer à configurer votre DNS, sélectionnez **/DNS** dans le menu de navigation, comme indiqué précédemment.
 
 Pour plus d'informations sur la configuration et la gestion de votre DNS à des fins de fiabilité, [voir ce document](dns.html#setting-up-your-domain-name-system-dns-for-ibm-cis).


## Configuration des équilibreurs de charge globaux


Pour commencer à configurer vos équilibreurs de charge globaux, sélectionnez **Equilibreurs de charge globaux** dans le menu de navigation.

Pour plus d'informations sur la configuration et la gestion des équilibreurs de charge globaux, [voir ce document](glb.html#global-load-balancer-glb-concepts).

## Utilisation des règles de page pour augmenter la fiabilité

Vous trouverez ci-dessous certains paramètres de règle de page permettant d'atteindre une fiabilité maximale de votre site :

 * Toujours en ligne
 * Contrôle du cache d'origine
 * URL de redirection

 ## Toujours en ligne

Utilisez le paramètre de règle de page **Toujours en ligne** pour qu'une partie de votre site reste en ligne en cas de défaillance de votre serveur.

Avec le paramètre **Toujours en ligne**, si votre serveur tombe en panne, IBM CIS distribue les pages à partir de notre cache, de sorte que vos visiteurs puissent consulter certaines des pages de votre site. Vos visiteurs verront un message en haut de la page les informant qu'ils sont en mode de navigation hors ligne. Toujours en ligne renvoie un statut HTTP 503, qui est également utilisé par un grand nombre d'autres applications. Lorsque votre serveur est à nouveau en ligne, IBM CIS repasse en mode de navigation standard de façon totalement transparente pour les utilisateurs.

Si IBM CIS ne dispose pas de la page demandée en mémoire cache, une page d'erreur s'affiche, informant vos visiteurs que la page du site Web à laquelle ils tentent d'accéder est hors ligne.

### Modalités de configuration du paramètre Toujours en ligne

Pour activer le paramètre **Toujours en ligne**, suivez les étapes ci-dessous :

 * Utilisez le menu de navigation pour sélectionner Règles de page sous Performances.
 * Créez une règle de page avec le masque d'URL de votre domaine.
 * Ajoutez le paramètre **Toujours en ligne** avec le commutateur activé.
 * Sélectionnez Provisionner 1 ressource.

 ### Limitations du paramètre Toujours en ligne

 * **Toujours en ligne** met en cache les 10 premiers liens à partir de votre HTML racine, puis les premiers liens à partir de chacune de ces pages, et enfin les premiers liens à  partir de chacune des pages suivantes. Cela signifie que seules quelques pages de votre site seront visibles si votre serveur d'origine tombe en panne.

 * Les sites récemment ajoutés ne sont pas associés à un cache important de leur site, ce qui signifie que le paramètre **Toujours en ligne** peut ne pas fonctionner si vous avez ajouté le site il y a quelques jours seulement.

 * CIS n'est pas en mesure d'afficher de contenu privé ni de gérer l'envoi de formulaire (POST) en cas de panne de votre serveur. Les visiteurs verront alors un message d'erreur sur les pages de réservation ou sur les éléments nécessitant une connexion.

 * Pour déclencher le paramètre **Toujours en ligne**, votre serveur Web doit renvoyer un code d'erreur HTTP standard 502 ou 504 de dépassement de délai. Ce paramètre fonctionne également lorsque nous ne parvenons pas à contacter votre origine (erreurs 521 & 523), lorsque les délais d'attente sont dépassés (522 & 524), lorsque des erreurs SSL (525 & 526) ou inconnues (520) se produisent. Le paramètre **Toujours en ligne** n'est pas déclenché pour les autres codes réponses HTTP, tels que 404, 500 ou 503, les erreurs de connexion à la base de données, les erreurs de serveur interne ou les réponses vides du serveur.

 * Le paramètre **Toujours en ligne** ne fonctionne pas si une règle de page "Tout mettre en cache" est activée avec une valeur "TTL cache de périphérie" inférieure à la fréquence de mise en cache (clients gratuits : 7 jours, clients professionnels : 3 jours et clients d'entreprise : 1 jour), car l'option "TTL cache de périphérie" entraîne la suppression du cache **Toujours en ligne** dans l'intervalle correspondant.

## Contrôle du cache d'origine

Le paramètre de règle de page **Contrôle du cache d'origine** permet de déterminer le contenu mis en cache à partir de votre origine ainsi que la fréquence de mise à jour du contenu, ce qui a une incidence sur la fiabilité et les performances. Par défaut, si aucun paramètre n'est modifié et qu'aucun en-tête empêchant la mise en cache n'est envoyé depuis votre serveur d'origine, IBM CIS met en cache tout le contenu statique avec certaines extensions. Ces types de contenus incluent les images, les feuilles de style CSS et JavaScript. La mise en cache est alors effectuée principalement pour des raisons de performances.

Pour configurer le paramètre **Contrôle du cache d'origine**, vous allez utiliser les règles de page afin d'activer certains en-têtes spécifiques susceptibles de fournir le comportement désiré à l'égard de chaque ressource de votre contenu. Pour savoir comment utiliser le paramètre **Contrôle du cache d'origine**, vous devez avoir certaines connaissances générales sur les règles de page et le comportement global de mise en cache pour CIS, que vous trouverez dans les sections qui suivent. Il existe généralement trois méthodes pour contrôler la mise en cache et l'option **Contrôle du cache d'origine** constitue la deuxième méthode.

La configuration du paramètre **Contrôle du cache d'origine** appelle des règles en mise en cache qui tendent à respecter rigoureusement les meilleures pratiques Internet et RFC, principalement en ce qui concerne la revalidation. Par exemple, le comportement par défaut de CIS lorsque `max-age=0` consiste à ne rien mettre en cache, alors que le paramètre **Contrôle du cache d'origine** va procéder à la mise en cache, mais toujours avec une revalidation.

### Procédure de configuration du paramètre Contrôle du cache d'origine

 * Utilisez le menu de navigation pour sélectionner Règles de page sous Performances.
 * Créez une règle de page avec le masque d'URL qui fait référence à votre domaine.
 * Ajoutez le paramètre **Contrôle du cache d'origine** avec le commutateur activé.
 * Sélectionnez Provisionner 1 ressource.

### Priorité de règle de page

Deux règles de page spécifiques sont prioritaires pour la mise en cache globale :

 * Si une règle de page a un **niveau de cache** défini sur `Ignorer`, les ressources qui correspondent à cette règle de page ne sont pas mises en cache. IBM CIS agit toujours comme un proxy, et les autres caractéristiques de performances restent actives. Toutefois, votre contenu ne sera pas distribué à partir de notre cache, mais il sera extrait directement à partir de votre serveur d'origine.

 * Si une règle de page a un **niveau de cache** défini sur `Tout mettre en cache`, les ressources qui correspondent à la règle de page sont mises en cache. **L'utilisation de ce paramètre de règle de page est l'unique façon de nous informer des ressources à mettre en cache au-delà de ce que nous considérons comme statique, notamment le langage HTML.**

Si aucune règle de page n'est définie, nous appliquons le mode de mise en cache `Standard`, qui est basé sur l'extension de la ressource. Nous mettons alors uniquement en cache les ressources statiques (comme indiqué précédemment).

### En-têtes de contrôle du cache d'origine

La deuxième façon de modifier le comportement de mise en cache d'IBM CIS consiste à utiliser des en-têtes de mise en cache à partir de l'origine. CIS applique ces paramètres, mais vous pouvez les ignorer en spécifiant le paramètre de règle de page **TTL cache de périphérie**. Les en-têtes à prendre en compte lorsque vous déterminez les ressources à mettre en cache à partir de votre origine sont les suivants :

 * Si l'en-tête **Cache-Control** est défini sur `private`, `no-store`, `no-cache` ou `max-age=0`, ou si la réponse comporte un cookie, IBM CIS ne met pas en cache la ressource. Sachant qu'il est préférable de ne pas mettre en cache les informations confidentielles, vous  pouvez envisager d'utiliser l'un de ces en-têtes si besoin.

 * Si l'en-tête **Cache-Control** est défini sur `public` et que la valeur `max-age` est supérieure à 0, ou si les en-têtes `Expires` doivent être configurés à l'avenir, nous mettrons la ressource en mémoire cache.

**Remarque :** Comme précisé dans les règles RFC, le paramètre `Cache-Control: max-age` prend la priorité sur les en-têtes `Expires`. Si les deux sont définis et qu'ils sont contradictoires, le paramètre `max-age` l'emporte.

### Utilisation de l'en-tête 's-maxage'

La troisième façon de contrôler le comportement de mise en cache, ainsi que le comportement de mise en cache du navigateur consiste à utiliser l'en-tête de contrôle du cache `s-maxage`.

Normalement, nous respectons la directive `max-age` : 

`Cache-Control: max-age=1000`

Mais si vous souhaitez indiquer un délai de mise en mémoire cache différent de celui du navigateur, nous pouvons utiliser `s-maxage`. Vous trouverez ci-dessous un exemple demandant à IBM CIS de mettre l'objet en mémoire cache pendant 200 secondes et au navigateur pendant 60 secondes.

`Cache-Control: s-maxage=200, max-age=60`

Fondamentalement, `s-maxage` est destiné à être suivi UNIQUEMENT par les proxy inverses (pour que le navigateur puisse l'ignorer) alors qu'IBM CIS donne la priorité à `s-maxage` s'il est présent. IBM CIS suivra la valeur la plus élevée : le paramètre de cache du navigateur ou l'en-tête `max-age`.

### Récapitulatif sur les en-têtes de contrôle du cache et les règles de page à des fins de fiabilité

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

 * Pour mettre davantage de contenu en mémoire cache, créez une règle de page avec le paramètre **Niveau de cache** défini sur "Tout mettre en cache" à l'adresse URL souhaitée (si votre serveur Web renvoie une erreur 404 au moment de demander l'URL, le résultat est mis en cache pendant 5 minutes seulement).

 * Pour empêcher la mise en cache sur une adresse URL, créez une règle de page avec le paramètre **Niveau de cache** défini sur "Ignorer".


 ## URL de redirection

Pour garantir la haute disponibilité de votre contenu, vous pouvez créer une règle de page avec le paramètre **URL de redirection** à utiliser en cas d'indisponibilité de votre site.

 **Remarque :** Lorsque vous activez le paramètre **URL de redirection**, tous les autres paramètres sont désactivés, car vous envoyez l'ensemble du trafic vers une autre adresse URL.

### Procédure de configuration du paramètre URL de redirection

 * Utilisez le menu de navigation pour sélectionner Règles de page sous Performances.
 * Créez une règle de page avec le masque d'URL qui fait référence à votre domaine.
 * Ajoutez le paramètre **URL de redirection**.
 * Sélectionnez le type d'acheminement et indiquez l'URL de destination.
 * Sélectionnez Provisionner 1 ressource. 

### Exemples de transfert :

Supposons que vous voulez faciliter l'accès à une URL de type :

    *www.example.com/+

    *example.com/+

Le masque suivant permettra les correspondances suivantes :

    http://example.com/+
    http://www.example.com/+
    https://www.example.com/+
    https://blog.example.com/+
    https://www.blog.example.com/+
    Etc...

En revanche, il ne permettra pas les correspondances suivantes :

    http://www.example.com/blog/+  [répertoire supplémentaire avant le +]
    http://www.example.com+  [pas de barre oblique à la fin]


Une fois que vous avez créé le masque qui correspond à ce que vous souhaitez, ajoutez le paramètre **URL de redirection**, choisissez le type de transfert et indiquez l'URL de destination. Par exemple :

    https://plus.google.com/yourid

Sélectionnez Provisionner 1 ressource. En quelques secondes, toutes les demandes correspondantes au masque seront acheminées vers la nouvelle URL avec la redirection spécifiée.

### Options de transfert avancées :

Si vous utilisez une redirection de base, telle que le transfert du domaine racine vers www.yourdomain.com, vous perdez tous les autres éléments de l'URL. Par exemple, vous définissez le masque :

    example.com

Et vous le transférez vers :

    http://www.example.com

Mais si quelqu'un ajoute :

    example.com/some-particular-page.html

Il sera transféré vers :

    www.example.com

et non vers

    www.example.com/some-particular-page.html

La solution consiste à utiliser des variables. Chaque caractère générique correspond à une variable pouvant être référencée dans l'adresse de réacheminement. Les variables sont représentées par un signe `$` suivi d'un chiffre. Pour faire référence au premier caractère générique, vous utilisez `$1`, au deuxième caractère générique, vous utilisez `$2`, et ainsi de suite. Pour corriger le transfert de la racine vers `www` dans notre exemple précédent, vous pouvez utiliser le même masque :

    example.com/*

Puis configurer l'URL suivante de manière que le trafic soit transféré vers :

    http://www.example.com/$1

Dans ce cas, si une personne accède à :

    example.com/some-particular-page.html

Elle est redirigée vers :

    http://www.example.com/some-particular-page.html
