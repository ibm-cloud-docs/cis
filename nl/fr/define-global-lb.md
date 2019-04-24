---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: global load balancer, global load balancer configuration

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Définir l'équilibreur de charge global
{:#define-the-global-load-balancer}

Définissez la configuration de votre équilibreur de charge global en spécifiant un nom d'hôte, en ajoutant et en ajustant vos pools d'origines et en définissant des règles supplémentaires pour contrôler la façon dont le trafic est acheminé aux clients.

1. Créez votre équilibreur de charge global en cliquant sur le bouton Créer un équilibreur de charge situé à droite.  

2. Spécifiez un nom d'hôte pour votre domaine et, le cas échéant, ajustez la valeur TTL (la valeur par défaut est 60 secondes). Utilisez ensuite le bouton **Ajouter un pool** pour ajouter vos pools d'origines. 

   <img src="images/reliability11.png" alt="dessin" style="width: 300px;"/>
   
   **Remarque :** les noms d'hôte combinés à des noms de domaine forment des noms de domaine complets pour votre application. Vos utilisateurs finaux se connectent à votre application avec ce nom de domaine complet. 
   
3. Ajustez les priorités relatives de vos pools d'origines en cliquant sur les flèches de déplacement vers le haut et vers le bas situées à gauche du pool. Les demandes d'application émanant des utilisateurs finaux sont traitées de façon circulaire par ces pools d'origines. 
   
   <img src="images/reliability12.png" alt="dessin" style="width: 300px;"/>   
   
4. Vous pouvez éventuellement définir des règles supplémentaires pour contrôler la façon dont le trafic est acheminé aux clients à partir de différentes régions géographiques. Dans l'exemple ci-dessous, les clients qui arrivent du Sud-ouest des Etats-Unis sont acheminés vers le pool d'origines de la Côte Ouest des Etats-Unis. Vous pouvez utiliser ces règles pour diriger les clients vers la région la plus proche. Si l'une de ces régions échoue, les demandes sont acheminées vers d'autres emplacements sains disponibles, de sorte que les utilisateurs finaux ne soient pas affectés par la durée d'indisponibilité. 

   <img src="images/reliability13.png" alt="dessin" style="width: 300px;"/>   
   
5. Cliquez sur **Mettre à disposition les ressources** pour terminer la configuration de votre équilibreur de charge global. 
6. Enfin, vérifiez la connectivité à votre application en tapant `FQDN URL` dans une fenêtre de navigateur mobile. Un message de bienvenue s'affiche si vous parvenez à vous connecter.
