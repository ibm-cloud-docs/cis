---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: global load balancer configuration, glb configuration

subcollection: cis

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}

# Commencer la configuration de l'équilibreur de charge global
{:#begin-global-load-balancer-configuration}

Commencez à configurer votre équilibreur de charge global.

1. Sous la section **Fiabilité**, sélectionnez **Equilibreur de charge global**. 
    
    <img src="images/reliability6.png" alt="dessin" style="width: 300px;"/>

2. Faites défiler l'écran jusqu'à la section Contrôles de santé.  

   Cette configuration est facultative. Si vous ne définissez pas de contrôles de santé personnalisés, le système utilisera “/” comme chemin de contrôle de santé par défaut.
{:note}

3. Cliquez sur le bouton **Créer un contrôle de santé** pour définir un contrôle de santé personnalisé.    

   Indiquez le chemin sur lequel vous souhaitez effectuer vos contrôles de santé. Vous pouvez utiliser des protocoles HTTP ou HTTPS pour vos contrôles de santé.  
   
4. Sous **Options avancées**, vous pouvez personnaliser d'autres paramètres, tels que l'intervalle de contrôle de santé, le nombre de tentatives, la méthode de demande et le corps de réponse.  
   
   <img src="images/reliability7.png" alt="dessin" style="width: 300px;"/>
   
5. Cliquez sur **Mettre à disposition une ressource** pour terminer votre configuration de contrôle de santé.  
