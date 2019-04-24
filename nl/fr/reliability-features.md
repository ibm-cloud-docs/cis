---
copyright:
  years: 2018
lastupdated: "2018-03-06"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Comment IBM Cloud Internet Services (CIS) fiabilise-t-il vos activités ?

IBM Cloud Internet Services (CIS) vous aide à améliorer la fiabilité de vos applications et services Web en réduisant la durée d'immobilisation causée par l'indisponibilité de l'application et de l'infrastructure. Par exemple, l'équilibrage de charge global vous permet de déployer vos applications et services Web dans plusieurs régions. Lorsque l'équilibrage de charge global est activé, IBM CIS achemine les demandes de vos clients vers les régions disponibles les plus proches. Si une région est défaillante, les demandes sont transférées vers le prochain emplacement le plus proche, afin que les clients ne soient pas affectés par la durée d'immobilisation. Si votre site Web ou votre API tombe en panne, IBM CIS vous envoie une notification automatique et vous informe également de son rétablissement.


![reliability-graphic.png](images/reliability-graphic.png)

Voici un bref aperçu des fonctionnalités :

## Caractéristiques de fiabilité

 * Equilibrage de charge global 
 * Options de traitement par proxy ou non pour l'équilibrage de charge
 * Pools d'origine et moniteurs de santé
 * Gestion DNS
 
### Récapitulatif
 
  * Les moniteurs de santé vérifient si vos pools d'origine sont intègres.
  * En cas de défaillance d'un moniteur, les demandes sont acheminées vers des origines saines.
  * Vous êtes informé de la défaillance de votre service Web ou API, ainsi que de leur restauration.
