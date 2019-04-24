---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: IBM CIS deployment, query strings, HTML files

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Concepts de mise en cache
{:#caching-concepts}

Ce document présente certains concepts et définitions liés à la mise en cache et à la façon dont elle affecte votre déploiement IBM CIS.

## Qu'est-ce que la mise en cache ?
{:#what-is-caching}

La mise en cache est le processus de stockage des fichiers sur vos serveurs d'équilibrage de charge, en vue d'améliorer le temps de réponse lié au traitement des fichiers. En conservant les fichiers plus près des clients, nous pouvons réduire le temps nécessaire aux données pour être transmises sur le réseau, communément appelé **temps d'attente**.

Les fichiers mis en cache ont un délai d'expiration spécifique (**durée de vie du cache**), à l'issue duquel ils sont supprimés de la mémoire cache. Vous pouvez également vider les fichiers de la mémoire cache manuellement. Une fois les fichiers supprimés, CIS recontacte votre serveur d'origine pour recharger les fichiers et mettre à jour la mémoire cache avec les versions les plus récentes.

Pour en savoir plus sur les paramètres de cache et les options de mise en cache, voir le [tutoriel sur la mise en cache et les règles de page](/docs/infrastructure/cis?topic=cis-use-page-rules-with-caching).

### Quel contenu est mis en cache ? 
{:#what-content-is-cached}

Par défaut, nous mettons en cache les **fichiers statiques**, qui incluent un grand nombre de fichiers image et texte (fichiers non HTML). Cela inclut uniquement les fichiers de vos sites Web et non les ressources tierces de sites de réseaux sociaux, etc. De plus, nous ne mettons actuellement pas en cache par type MIME. 

### Comment puis-je mettre en cache des fichiers HTML ? 
{:#how-do-i-cache-html}

Nous ne mettons pas en cache les fichiers HTML par défaut, car nous ne les considérons pas comme statiques ; toutefois, si le code HTML statique peut être clairement distingué du code HTML dynamique, il est possible de mettre en cache les fichiers HTML [à l'aide de la fonctionnalité Règles de page](/docs/infrastructure/cis?topic=cis-use-page-rules).


## Tri des chaînes de requête
{:#query-string-sorting}

**Enterprise Only** CIS traite les URL contenant des chaînes de requête dans différents ordres en tant que fichiers distincts dans le cache. Cela signifie que si un utilisateur demande :

`/video/123456?title=0&byline=0&portrait=0&color=987654`

Et qu'un autre utilisateur demande :

`/video/123456?byline=0&color=987654&portrait=0&title=0`

CIS revient à l'origine, même si le fichier se trouve dans notre cache. 

Le Tri des chaînes de requête trie les chaînes de requête _avant_ qu'elles n'atteignent notre cache, ce qui entraîne un taux de réussite du cache plus élevé. Activez le Tri des chaînes de requête à l'aide de la bascule de la page **Mise en cache**.

## Serve Stale Content
{:#serve-stale-content-caching}

Conserve une version limitée du site en ligne si le serveur tombe en panne. Même si le contenu a expiré, CIS continue de servir le contenu mis en cache aux utilisateurs lorsque les serveurs d'origine sont déconnectés. 
