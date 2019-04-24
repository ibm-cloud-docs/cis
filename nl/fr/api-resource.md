---

copyright:
  years: 2018
lastupdated: "2018-03-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Spécifications de l'API

Procédure d'affichage des spécifications de l'API CIS : 

1. Pour afficher les API CIS, accédez à la page relative aux [spécifications de l'API CIS](https://console.bluemix.net/apidocs/2640-cloud-internet-services). 

2. Dans le menu de navigation de gauche, choisissez celles de votre choix dans la liste des API disponibles.


## Notes

1. Noeud final de l'API : https://api.cis.cloud.ibm.com.

2. L'en-tête **X-Auth-User-Token** est requis pour chaque appel API. Il s'agit du jeton bearer de l'utilisateur qui peut être extrait depuis IAM (par exemple, en utilisant la commande "bx iam oauth-tokens").

3. La zone **crn** est également requise dans le chemin pour chaque appel API. Il s'agit du nom de ressource de cloud (CRN) d'une instance de ressource CIS en cours de configuration (par exemple, vous pouvez extraire le CRN d'une instance de ressource en utilisant la commande "bx resource service-instance <instance-name>"). Le CRN doit être au format URL dans l'appel API.

4. Le nombre d'appels API est limité à 100 par minute. Si cette limite est dépassée, les appels ultérieurs sont bloqués pendant un certain temps.
