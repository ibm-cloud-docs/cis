---
copyright:
  years: 2018
lastupdated: "2018-28-03"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Foire aux questions

## A quoi ai-je droit avec le plan d'accès anticipé ?
La formule du programme d'accès anticipé autorise une seule zone par compte. Nous vous conseillons de créer une seule instance par compte et de vérifier le nom de la zone. Il est essentiel de vérifier le nom de la zone avant de l'ajouter. Si une zone est supprimée, il est impossible d'ajouter une autre zone ou la même zone pendant le programme du plan anticipé.

## Pourquoi mon domaine est-il en attente ? Comment l'activer ?
Lorsque vous ajoutez un domaine à CIS, nous vous fournissons quelques serveurs de noms à configurer au niveau de votre registre (ou de votre fournisseur de DNS si vous ajoutez un sous-domaine). Le domaine ou le sous-domaine reste en attente jusqu'à ce que vous ayez correctement configuré les serveurs de noms. Assurez-vous de bien ajouter les deux serveurs de noms dans votre registre ou votre fournisseur DNS. Nous analysons régulièrement le système DNS public afin de vérifier que les serveurs de noms ont été configurés conformément aux instructions. Dès que nous avons vérifié vos modifications (dans un délai de 24 heures), nous activons votre domaine. Vous pouvez soumettre une nouvelle demande de vérification des serveurs de noms en cliquant sur l'option **Revérifier les serveurs de noms** dans la page de vue d'ensemble.

## Qui est le registre de mon domaine ?
Consultez la page https://whois.icann.org/ pour en savoir plus à ce sujet. **Remarque** : Vous devez disposer de privilèges d'administration pour modifier la configuration de votre domaine au niveau du registre en vue de mettre à jour ou d'ajouter les serveurs de noms fournis pour votre domaine lorsque vous l'ajoutez à CIS. Si vous ne connaissez pas le nom du registre associé au domaine que vous essayez d'ajouter au CIS, il est peu probable que vous disposiez des autorisations requises pour mettre à jour la configuration de votre domaine au niveau du registre. Prenez contact avec le propriétaire du domaine dans votre organisation afin d'effectuer les modifications nécessaires.

## Je souhaite conserver mon fournisseur DNS actuel pour mon domaine (example.com). Puis-je déléguer un sous-domaine (subdomain.example.com) depuis mon fournisseur DNS actuel vers CIS ?
Oui. Le processus est similaire à l'ajout d'un domaine, si ce n'est qu'à la place du registre, vous avez à faire au fournisseur DNS pour le domaine de niveau supérieur. Lorsque vous ajoutez un sous-domaine à CIS, vous devez configurer deux serveurs de noms, comme d'habitude. Vous configurez un enregistrement serveur de noms (NS) pour chaque serveur de noms en tant qu'enregistrement DNS au sein du domaine actuellement géré par l'autre fournisseur DNS. Dès que nous avons vérifié que les enregistrements DNS requis ont été ajoutés, nous activons votre sous-domaine. Si vous ne gérez pas le domaine de niveau supérieur au sein de votre organisation, vous devez prendre contact avec le propriétaire du domaine de niveau supérieur pour bénéficier des enregistrements NS que vous avez ajoutés.

## Qu'est-ce que TLS ?
TLS est un protocole de sécurité standard qui crée un canal sécurisé entre un serveur Web et un navigateur au cours d'une communication en ligne. Un certificat TLS est requis pour créer une connexion TLS avec un site Web, et se compose du nom de domaine, du nom de la société et de données supplémentaires, telles que l'adresse, la ville, le code postal et le pays de la société. En outre, le certificat indique la date d'expiration, ainsi que les détails concernant l'autorité de certification émettrice.

## Comment fonctionne TLS ?
Lorsqu'un navigateur initie une connexion avec un site Web sécurisé TLS, il va d'abord chercher le certificat TLS du site pour vérifier sa validité. Il vérifie que l'autorité de certification est de confiance et que le certificat est bien utilisé pour le site Web pour lequel il a été émis. Si l'une de ces conditions n'est pas vérifiée, un message avertissement s'affiche vous indiquant que le site Web n'est pas sécurisé par un certificat valide.

Lorsqu'un certificat TLS est installé sur un serveur Web, il permet d'établir une connexion sécurisée entre le serveur Web et le navigateur qui s'y connecte. Le préfixe 'https' remplace 'http' dans l'adresse du site Web et un cadenas s'affiche dans la barre d'adresse. Si le site Web utilise un certificat à validation étendue (EV), le navigateur peut également afficher la barre d'adresse en vert.

## Pourquoi un avertissement de confidentialité s'affiche-t-il ?
Les certificats TLS émis par IBM Cloud CIS couvrent le domaine racine (`example.com`) et un niveau du sous-domaine (`*.example.com`). Si vous tentez d'atteindre un second niveau du sous-domaine (`*.*.example.com`), un avertissement de confidentialité s'affiche dans votre navigateur, car les noms d'hôte n'ont pas été ajoutés au SAN.

En outre, veuillez compter jusqu'à 15 minutes pour que l'une de nos autorités de certification partenaires émette un nouveau certificat. Un avertissement de confidentialité s'affichera dans votre navigateur si le nouveau certificat n'a pas encore été émis.

## Qu'est-ce qu'une attaque DDoS ?
Une attaque par déni de service distribué (DDoS) est une tentative de rendre un service en ligne indisponible en le surchargeant d'un important trafic provenant de nombreuses sources. Dans une attaque DDoS, plusieurs systèmes informatiques compromis attaquent une cible, telle qu'un serveur, un site Web ou toute autre ressource réseau, ce qui a des répercussions sur l'utilisation de la ressource cible.

Le flux de messages entrants, requêtes de connexion ou paquets mal formés vers le système cible a pour conséquence de ralentir, voire de bloquer et d'arrêter le système cible, empêchant ainsi les utilisateurs ou systèmes légitimes d'un service de l'utiliser. Les attaques DDoS sont menées par divers auteurs, allant du simple pirate informatique aux réseaux de criminels organisés et agences gouvernementales.

## Que faire en cas d'attaque DDoS ?

**Etape 1 :** Activez le “Mode défense" dans l'écran **Vue d'ensemble**. 

![Mode Défense](images/defense-mode.png)

**Etape 2 :** Paramétrez vos enregistrements DNS sur la sécurité maximale.

**Etape 3 :** N'appliquez pas de limite de débit ni de régulateurs de demandes dans IBM CIS, car vous avez besoin de bande passante pour vous en sortir.

**Etape 4 :** Bloquez certains pays ou visiteurs, si nécessaire.

## J'ai reçu une erreur 522, que dois-je faire ? 

Une erreur 522 signifie que nous n'avons pas pu établir de connexion à votre serveur d'origine (à savoir, votre hôte). Si la connexion n'est pas établie au bout de 15 secondes, la page d'erreur 522 s'affiche.

Ce problème est généralement causé par un pare-feu ou logiciel de sécurité qui bloque accidentellement nos adresses IP. CIS agissant en tant que proxy inverse, les connexions à votre site donneront l'impression de provenir de diverses adresses IP CIS. Ainsi, certains pare-feux peuvent bloquer ces connexions, nous empêchant ainsi d'afficher correctement le contenu du site à vos visiteurs.

Pour corriger ce problème, demandez à votre hôte d'établir une liste blanche de toutes les adresses IP CIS, consultable [ici](whitelisted-ips.html).

Toutes ces adresses IP doivent être répertoriées dans la liste blanche pour éviter les erreurs 522. De même, il convient de vérifier qu'aucune de ces adresses n'est bloquée.

Les erreurs 522 peuvent également être causées par des problèmes de connectivité. Par conséquent, assurez-vous que votre serveur et votre réseau sont sains et qu'ils ne sont pas surchargés.

Si, malgré toutes ces mesures, vous continuez à recevoir des erreurs, contactez le support et confirmez les points suivants :

* Vos adresses IP sont sur liste blanche
* Votre serveur/réseau est en ligne et n'a pas subi d'altération majeure

Si vous contactez notre équipe de support, veuillez fournir le Ray ID d'une erreur 522 récente. Nous l'utiliserons pour déterminer le centre de données CIS concerné et exécuter des tests supplémentaires.

## Qu'est-ce qu'un enregistrement proxy et pourquoi en ai-je besoin ?

Les enregistrements proxy sont des enregistrements qui acheminent leur trafic via le proxy d'IBM CIS. Seuls les enregistrements proxy bénéficient des avantages CIS, à l'instar du masque IP, où une adresse IP CIS remplace l'adresse IP d'origine afin de la protéger :

```
$ whois 104.28.22.57 | grep OrgName
OrgName:        IBM
```

Si vous préférez ignorer CIS sur un domaine (une résolution DNS est quand même appliquée), il est possible de ne pas utiliser l'enregistrement comme proxy.

## J'ai reçu une erreur de validation DNS : 1004, que dois-je faire ?

Pour que les règles de page fonctionnent, le système DNS de votre zone doit être résolu. Par conséquent, vous devez disposer d'un enregistrement DNS proxy pour votre zone. 
