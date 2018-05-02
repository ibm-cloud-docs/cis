---
copyright:
  years: 2018
lastupdated: "2018-03-13"
---

# Concepts de mise en cache

Ce document présente certains concepts et définitions liés à la mise en cache et à la façon dont elle affecte votre déploiement IBM CIS.

## Qu'est-ce que la mise en cache ?

La mise en cache est le processus de stockage des fichiers sur vos serveurs d'équilibrage de charge, en vue d'améliorer le temps de réponse lié au traitement des fichiers. En conservant les fichiers plus près des clients, nous pouvons réduire le temps nécessaire aux données pour être transmises sur le réseau, communément appelé **temps d'attente**.

Par défaut, nous mettons en cache les **fichiers statiques**, qui incluent un grand nombre de fichiers image et texte (fichiers non HTML). En revanche, nous ne mettons pas en cache les fichiers HTML, car ceux-ci ne sont pas considérés comme étant statiques. Vous pouvez toutefois les mettre en cache en utilisant la fonctionnalité [Règles de page](using-page-rules.html).

Les fichiers mis en cache ont un délai d'expiration spécifique (**durée de vie du cache**), à l'issue duquel ils sont supprimés de la mémoire cache. Vous pouvez également vider les fichiers de la mémoire cache manuellement. Une fois les fichiers supprimés, CIS recontacte votre serveur d'origine pour recharger les fichiers et mettre à jour la mémoire cache avec les versions les plus récentes.

Pour en savoir plus sur les paramètres et les options de mise en cache, voir le tutoriel sur l'[utilisation des règles de page avec la mise en cache](caching-with-page-rules.html).
