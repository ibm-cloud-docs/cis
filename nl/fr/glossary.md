---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Glossary, load balancer, pool, health check

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Glossaire
{:#glossary}

Ce glossaire contient les définitions des termes courants que vous pouvez rencontrer lorsque vous travaillez avec l'Equilibreur de charge global (GLB). 

## Equilibreur de charge
{:#glossary-load-balancer}

Un équilibreur de charge est un périphérique qui agit en tant que proxy inverse et répartit le trafic réseau ou applicatif sur plusieurs serveurs. Les équilibreurs de charge permettent d'augmenter la capacité du système (le nombre d'utilisateurs simultanés) et d'améliorer la fiabilité des applications. 

## Pool
{:#glossary-pool}

Un pool est un groupe de serveurs d'origine vers lequel est acheminé le trafic lorsqu'il est associé à un GLB. Le nombre minimal de serveurs d'origine disponibles requis pour que le pool soit considéré comme étant sain peut être défini par l'utilisateur, ainsi que le contrôle de santé à utiliser. Le pool d'origines peut être associé à une région spécifique ou peut être disponible pour l'ensemble des régions.

## Contrôle de santé
{:#glossary-health-check}

Le contrôle de santé vous aide à avoir un meilleur aperçu de la disponibilité des pools de manière à pouvoir rediriger le trafic vers les pools qui sont sains. Ces contrôles envoient régulièrement des requêtes HTTP/HTTPS et surveillent les réponses. Ils peuvent être configurés avec des intervalles, délais d'attente, codes d'état personnalisés. Dès qu'un pool est signalé comme étant malsain, le trafic est redirigé vers un autre pool disponible, le cas échéant.

## Serveurs d'origine
{:#glossary-origin-servers}

Un serveur d'origine traite et répond aux demandes entrantes des clients et est généralement utilisé avec les serveurs de mise en cache. Les serveurs d'origine exécutent un ou plusieurs programmes conçus pour écouter et traiter les demandes Internet entrantes. La distance physique entre le serveur d'origine et le client exécutant une demande ajoute un temps d'attente à la connexion, ce qui augmente le temps de chargement. L'utilisation de serveurs de mise en cache réduit ce temps d'attente. 


