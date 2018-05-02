---

copyright:
  years: 2018
lastupdated: "2018-03-05"

---

# Concepts d'équilibreur de charge global (GLB)

Ce document présente certains concepts et définitions liés à l'équilibreur de charge global (GLB) et à la façon dont il affecte votre déploiement IBM CIS.

## Equilibreur de charge global

L'équilibreur de charge global (GLB) gère le trafic sur les ressources serveur installées dans différentes régions. Il utilise un pool pour répartir le trafic entre plusieurs origines, ce qui offre les avantages suivants :

  * Un temps de réponse réduit
  * Une plus haute disponibilité via la redondance
  * Une capacité de rendement de trafic optimisée

## Pool

Un pool est un groupe de serveurs d'origine vers lequel est acheminé le trafic lorsqu'il est associé à un GLB. Le nombre minimal de serveurs d'origine disponibles requis pour que le pool soit considéré comme étant sain peut être défini par l'utilisateur, ainsi que le contrôle de santé à utiliser. Le pool d'origine peut être associé à une région spécifique ou peut être disponible pour l'ensemble des régions.

## Contrôle de santé

Le contrôle de santé vous aide à avoir un meilleur aperçu de la disponibilité des pools de manière à pouvoir rediriger le trafic vers les pools qui sont sains. Ces contrôles envoient régulièrement des requêtes HTTP/HTTPS et surveillent les réponses. Ils peuvent être configurés avec des intervalles, délais d'attente, codes d'état personnalisés. Dès qu'un pool est signalé comme étant malsain, le trafic est redirigé vers un autre pool disponible, le cas échéant.
