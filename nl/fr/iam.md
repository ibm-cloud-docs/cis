---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Access Group Writer role, CIS instance, IAM

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# IAM et CIS
{:#iam-and-cis}

IBM Cloud Internet Services (CIS) utilise IAM pour effectuer l'autorisation et l'authentification. 

Si vous ne souhaitez ajouter personne à votre instance CIS, vous pouvez ignorer cette page.
{:note}

Limitez l'accès à trois portées fonctionnelles du CIS, en fonction de l'arborescence de navigation : 
* fiabilité - tels que DNS, GLB
* sécurité - tels que certificat, règles de pare-feu IP et limitation de débit
* performances - tels que règles de page, mise en cache et routage 

Cette section explique comment fournir un contrôle d'accès détaillé de votre instance. 

## Rôles
{:#iam-and-cis-roles}

Utilisez les trois rôles suivants pour exploiter IAM
* Lecteur - Capable d'obtenir des informations sur l'instance et le domaine 
* Auteur - Capable d'apporter des modifications à la configuration existante 
* Responsable - Capable de créer ou de supprimer des instances, des domaines, de la configuration

## Groupes d'accès et utilisateurs 
{:#iam-and-cis-access-groups-users}

Une règle peut être attribuée à un utilisateur directement ou à un groupe d'accès. Nous vous recommandons de l'affecter à un groupe d'accès afin de réduire le nombre de règles créées et de réduire les efforts de gestion de ces règles. 

## Cache
{:#iam-and-cis-cache}

Nous mettons en cache les résultats des autorisations et utilisons le cache pour prendre une décision lorsque la même demande arrive à nouveau. Une fois que le cache atteint sa durée de vie (10 minutes), il arrive à expiration.

## Bonnes pratiques
{:#iam-and-cis-best-practices}

1. Au lieu de modifier une règle, supprimez la règle existante, puis créez-en une nouvelle. 

## Scénarios
{:#iam-and-cis-scenarios}

Cette section présente les différents exemples de règles d'accès créées via CIS.  

### Niveau de domaine avec le type `config`
{:#iam-and-cis-scenarios-domain-level}

#### Accès à un domaine unique avec `configuration de la sécurité` sur un groupe d'accès 
##### Rôle d'auteur

Bob a une instance CIS, `cis-test-instance`, et deux domaines `bob.com` et `bob-ibm.com`.
Bob souhaite fournir à tous les ingénieurs en sécurité (sec-group) de l'entreprise accès au rôle Auteur uniquement sur la **configuration de sécurité** de **`bob.com`**.

Ces étapes montrent comment créer une règle IAM pour concrétiser ce scénario. 

Une fois que Bob s'est connecté à cis-test-instance, il :
1. Clique sur l'onglet **Compte > Accès** dans la barre de navigation
1. Sélectionne le **groupe d'accès** - **sec-group** auquel il souhaite donner accès
1. Sélectionne **`bob.com`**
1. Sélectionne le rôle **Auteur** 
1. Sélectionne l'option **Configuration de sécurité**
1. Clique sur **créer une règle**

Dans l'onglet Gérer :
les règles suivantes sont créées pour **sec-group** :

```
Lecteur	Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Afficheur Resource	Only service instance cis-test-instance of CIS 	
Auteur Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e

Instance de service
    name: cis-test-instance
    id: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9
Domaine
    name: bob.com
    id: 4b23ec772965f672f96f05670e36827e
Type de configuration
    cfgType: security
```

Désormais, sec-group a uniquement accès à `bob.com` et peut modifier les valeurs relatives à la sécurité.  

##### Mise à jour du rôle Auteur vers le rôle Responsable pour un groupe d'accès

Si Bob souhaite mettre à jour le rôle Auteur vers le rôle Responsable pour sec-group, il doit supprimer la règle existante.  
1. Accédez à l'onglet **Gérer IAM > Groupes d'accès > sec-group > règles d'accès**
1. Supprimez la règle suivante  
  ```
  Auteur Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
  ```

Ensuite, Bob doit créer la nouvelle règle.  
1. Cliquez sur l'onglet **Compte > Accès** dans la barre de navigation
1. Sélectionnez le **groupe d'accès** - **sec-group** auquel il souhaite donner accès
1. Sélectionnez **`bob.com`**
1. Sélectionnez le rôle **Responsable**
1. Sélectionnez l'option **Configuration de sécurité**
1. Cliquez sur **créer une règle**

```
Lecteur Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Afficheur Resource	Only service instance cis-test-instance of CIS 	
Responsable Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

Si la règle existante (auteur) n'est pas supprimée, la tentative de création de la règle pour Responsable échoue. 

##### Mise à jour de la configuration pour inclure les performances avec la sécurité 

Si Bob souhaite octroyer un accès Responsable à sec-group pour la configuration des performances sur `bob.com` et de la sécurité, il : 
1. Clique sur l'onglet **Compte > Accès** dans la barre de navigation
1. Sélectionne le **groupe d'accès** - **sec-group** auquel il souhaite donner accès
1. Sélectionne **`bob.com`**
1. Sélectionne le rôle **Responsable**
1. Sélectionne l'option **Configuration de performance**
1. Clique sur **créer une règle**

```
Lecteur Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Afficheur Resource	Only service instance cis-test-instance of CIS 	
Responsable Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
Responsable Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: performance, domainId: 4b23ec772965f672f96f05670e36827e

```

#### Accès à tous les domaines avec `configuration de la sécurité`

Si vous souhaitez fournir des actions de sécurité pour `bob.com` et `bob-ibm.com` dans l'exemple précédent, vous devez créer une nouvelle règle en répétant les étapes pour chaque domaine. La seule différence est la sélection du domaine respectif pour chaque règle.

1. Cliquez sur l'onglet **Compte > Accès** dans la barre de navigation
1. Sélectionnez le **groupe d'accès** - **sec-group** auquel il souhaite donner accès
1. Sélectionnez **`bob.com`**
1. Sélectionnez le rôle **Responsable**
1. Sélectionnez l'option **Configuration de sécurité**
1. Cliquez sur **créer une règle**

```
Lecteur Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
Afficheur Resource	Only service instance cis-test-instance of CIS 	
Responsable Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
```

1. Cliquez sur l'onglet **Compte > Accès** dans la barre de navigation
1. Sélectionnez le **groupe d'accès** - **sec-group** auquel il souhaite donner accès
1. Sélectionnez **`bob-ibm.com`**
1. Sélectionnez le rôle **Responsable**
1. Sélectionnez l'option **Configuration de sécurité**
1. Cliquez sur **créer une règle**

```
Lecteur Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Afficheur Resource	Only service instance cis-test-instance of CIS 	
Responsable Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 7ad7341865246f5df482ad9f76aafb5a
```



#### Accès à un domaine unique avec `configuration de la sécurité` et `configuration de la fiabilité` 

Bob possède une instance CIS, cis-test-instance, et deux domaines `bob.com` et `bob-ibm.com`.
Bob souhaite fournir à Tony un accès au rôle Auteur uniquement pour les **actions de sécurité et de fiabilité** de **`bob-ibm.com`**.

Une fois que Bob s'est connecté à cis-test-instance, il :
1. Clique sur l'onglet **Compte > Accès** dans la barre de navigation
1. Sélectionne **Tony** auquel il souhaite fournir un accès
1. Sélectionne **`bob-ibm.com`**
1. Sélectionne le rôle **Auteur** 
1. Sélectionne l'option **Sécurité et fiabilité** 
1. Clique sur **créer une règle**

Deux règles sont ainsi créées sur le serveur de back end pour chaque type de configuration. 

### Niveau de domaine avec tous les types de configuration 
{:#iam-and-cis-scenarios-domain-level-all-config-types}

Bob veut accorder des droits en lecture/écriture/gestion au niveau du domaine à Tony.

#### Ecriture
Une fois que Bob s'est connecté à cis-test-instance, il :
1. Clique sur l'onglet **Compte > Accès** dans la barre de navigation
1. Sélectionne **Tony** auquel il souhaite fournir un accès
1. Sélectionne **`bob.com`**
1. Sélectionne le rôle **Auteur** 
1. Coche toutes les cases correspondant à la portée fonctionnelle de CIS 
1. Clique sur **créer une règle**

```
Auteur Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Auteur Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Auteur Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Lecteur Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Afficheur Resource	Only service instance cis-test-instance of CIS 	
```

#### Responsable
Une fois que Bob s'est connecté à cis-test-instance, il :
1. Clique sur l'onglet **Compte > Accès** dans la barre de navigation
1. Sélectionne **Tony** auquel il souhaite fournir un accès
1. Sélectionne **`bob.com`**
1. Sélectionne le rôle **Responsable**
1. Coche toutes les cases correspondant à la portée fonctionnelle de CIS 
1. Clique sur **créer une règle**

```
Responsable Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: security	
Responsable Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: performance	
Responsable Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a, cfgType: reliability	
Lecteur Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Afficheur Resource	Only service instance cis-test-instance of CIS 	
```

#### Lecteur
Une fois que Bob s'est connecté à cis-test-instance, il :
1. Clique sur l'onglet **Compte > Accès** dans la barre de navigation
1. Sélectionne **Tony** auquel il souhaite fournir un accès
1. Sélectionne **`bob.com`**
1. Sélectionne le rôle **Lecteur**
  1. Toutes les cases sont cochées pour indiquer que l'utilisateur nécessite un accès en lecture *min* à l'ensemble du domaine et ne peut pas donner un accès partiel à un domaine
1. Clique sur **créer une règle**


```
Lecteur Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 7ad7341865246f5df482ad9f76aafb5a	
Afficheur Resource	Only service instance cis-test-instance of CIS 	
```

### Niveau d'instance - tous vos domaines
{:#iam-and-cis-scenarios-instance-level}

Cette règle doit être créée et gérée via la page de gestion IAM. 

L'accès au niveau de l'instance signifie que Bob peut donner à Tony une autorisation sur l'instance 1 parmi toutes les 10 instances existantes. Tony est capable de voir tous les domaines dans cette instance.  

Si Bob souhaite autoriser Auteur ou Responsable à accéder aux éléments suivants, il doit accorder un accès au niveau instance : 
* Equilibreur de charge - pools et contrôles de santé
* Règles d'accès du pare-feu 
* Agents 

Dans la page de gestion IAM, créez une règle auteur/responsable sur l'instance de service cis-test-instance. 

```
Responsable Resource	Only service instance cis-test-instance of CIS 	
ou
Auteur Resource	Only service instance cis-test-instance of CIS 	
```

## Gestion des règles IAM  
{:#manage-iam-policies}

CIS permet aux utilisateurs de créer des règles IAM, mais la gestion doit être effectuée via la [Page IAM](
https://{DomainName}/iam#/overview).

## Important
{:#iam-note}
Pour chaque règle créée sur la page Accès de l'instance CIS, 2 à 3 règles sont créées à tour de rôle. 

1. Le rôle Afficheur de plateforme d'instance de service permet à l'utilisateur ajouté d'afficher l'instance sur le tableau de bord. 

**Exemple **
```
Afficheur Resource	Only service instance cis-instance-instance of CIS 	
```

2. L'accès en lecture au niveau du domaine est l'exigence minimale pour un accès précis au travail. 

**Exemple **
```
Lecteur Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, domainId: 4b23ec772965f672f96f05670e36827e	
```
3. La règle que vous avez créée avec le type de configuration est présente. 

**Exemple **
```
  Auteur Resource	serviceName: internet-svcs, serviceInstance: 8571763b-a0c2-40f4-af5e-e87f9b1e16b9, cfgType: security, domainId: 4b23ec772965f672f96f05670e36827e
  ```

**Foire aux questions**
1. Comment puis-je obtenir mon ID d'instance service ? 

   Copiez le CRN sur la page Vue d'ensemble 
   ```
   crn:v1:test:public:internet-svcs:global:a/2c38d9a9913332006a27665dab3d26e8:836f33a5-d3e1-4bc6-876a-982a8668b1bb::
   ```
   La dernière partie du CRN est votre instance de service : `836f33a5-d3e1-4bc6-876a-982a8668b1bb`.
   
   ou
   
   Cliquez sur la ligne contenant l'instance CIS sur la page principale de la liste de ressources et copiez l'identificateur global unique pour l'ID d'instance de service. 

2. J'ai supprimé une règle, mais l'utilisateur à qui j'ai accordé cette règle peut toujours effectuer l'action. 

   CIS met en cache les résultats de l'autorisation et la durée de vie du cache est de 10 minutes.   
   
   Lorsque IAM l'autorise, il utilise les règles d'accès du groupe d'accès et les propres règles de l'utilisateur avant de prendre une décision. 

3. Quels sont les droits nécessaires pour mettre à disposition Internet Services ?

   Si vous ne parvenez pas à créer une ressource et à l'ajouter à un groupe de ressources, vous êtes probablement confronté à un problème d'accès. Vous devez avoir au moins le rôle Afficheur pour le groupe de ressources et au moins le rôle Editeur pour le service du compte. Vous pouvez contacter l'administrateur du compte pour vérifier l'accès qui vous est affecté. Pour plus d'informations, voir [Gestion de l'accès aux ressources](/docs/iam?topic=iam-iammanidaccser).
   
 
