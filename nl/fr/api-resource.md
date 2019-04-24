---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: API Specs, CIS APIs

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Spécifications de l'API
{:#api-specs}

Procédure d'affichage des spécifications de l'API CIS : 

1. Pour afficher les API CIS, accédez à la page [Docs sur les API](/apidocs/). 

2. Dans le menu de navigation de gauche, cochez la case Mise en réseau pour filtrer les API. 

3. Choisissez dans la liste des API Cloud Internet Services disponibles. 


## Notes
{:#api-notes}

1. Noeud final de l'API : `https://api.cis.cloud.ibm.com`.

2. L'en-tête **X-Auth-User-Token** est requis pour chaque appel API. Cet en-tête est le jeton bearer de l'utilisateur qui peut être extrait depuis IAM (par exemple, à l'aide de la commande `ibmcloud iam oauth-tokens`).

3. La zone **crn** est également requise dans le chemin pour chaque appel API. Cette zone contient le nom complet de la ressource Cloud (CRN) pour une instance de ressource CIS en cours de configuration. (Par exemple, le CRN d'une instance de ressource peut être extrait de son nom à l'aide de la commande `ibmcloud resource service-instance <instance-name>`). Le CRN doit être au format URL dans l'appel API.

4. Le nombre d'appels API est limité à 100 par minute. Si cette limite est dépassée, les appels ultérieurs sont bloqués pendant un certain temps.
