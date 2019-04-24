---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Bypass, header responses, brute-force login attempts

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Limitation de débit
{:#cis-rate-limiting}

La limitation de débit (forfait Enterprise uniquement) protège contre les attaques par déni de service, les tentatives d'intrusions illicites et tout autre type de comportement abusif visant la couche application. 

Sélectionnez le type de règle de limitation de débit, soit la **règle personnalisée**, soit la **protection de connexion**

## Création d'une règle de limitation de débit personnalisée 
{:#create-a-custom-rate-limiting-rule}

Entrez un nom de règle qui vous permet de mémoriser l'action de la règle. Il s'agit d'une zone facultative.

Les **critères de correspondance de trafic** utilisent l'opération AND. Entrez une URL pour laquelle vous limitez le débit, puis lorsque les demandes issues de la **même adresse IP dépassent** le nombre spécifié de **demandes par seconde**, la règle spécifiée est déclenchée. 

L'option **Critères avancés** vous permet de spécifier les méthodes HTTP, les réponses d'en-tête et les codes de réponse d'origine pour limiter davantage les critères de correspondance.  

Sélectionnez une valeur dans la liste déroulante **Méthode** (ANY est la valeur par défaut).   

Mettez à jour l'**en-tête de réponse HTTP**. Vous pouvez également **ajouter un en-tête de réponse** pour inclure les en-têtes renvoyés par votre serveur Web d'origine.  

Si plusieurs en-têtes se trouvent sous l'**en-tête de réponse HTTP**, la logique booléenne _AND_ s'applique. Pour exclure la correspondance d'un en-tête, utilisez l'option _N'est pas égal à_. En outre, chaque en-tête doit être une correspondance exacte. Cependant, la sensibilité à la casse ne s'applique pas. {:note}

Sous le **code de réponse d'origine**, tapez la valeur numérique valide de chaque code de réponse HTTP à rechercher. Pour inclure deux codes de réponse ou plus, séparez chaque valeur par une virgule. Par exemple, vous pouvez entrer `401, 403` si vous souhaitez uniquement que ces deux codes d'erreur soient comptabilisés.  

### Configuration de la réponse 
{:#rate-limiting-configure-response}

Sélectionnez l'une des actions répertoriées et spécifiez le délai d'expiration. Dans ce cas, le délai d'expiration fait référence à la période d'interdiction pendant laquelle l'action a lieu. Un délai de 60 secondes signifie que l'action est appliquée pendant 60 secondes. 

|Action| Description|
|------|------------|
|Blocage | Emet une erreur 429 lorsque le seuil est dépassé|
|Demande d'authentification | L'utilisateur doit transmettre une demande d'authentification Google reCaptcha avant de continuer. En cas de succès, nous acceptons la demande. Faute de quoi, la demande est bloquée. | 	
|Demande d'authentification JS |	 L'utilisateur doit transmettre une demande d'authentification Javascript avant de continuer. En cas de succès, nous acceptons la demande. Faute de quoi, la demande est bloquée. |Simulation| Vous pouvez utiliser cette option pour tester votre règle avant d'appliquer l'une des autres options de votre environnement de production.

**Réponse avancée**

Spécifiez le type de réponse lorsque le seuil d'une règle est dépassé.  

### Contournement
{:#rate-limiting-bypass}

Le contournement vous permet de créer l'équivalent d'une liste blanche ou d'une exception pour un ensemble d'URL. Aucune action ne se déclenche pour ces URL, même si la règle de limitation de débit concorde. 

## Protection de la connexion
{:#rate-limiting-protect-login}

La protection de la connexion crée une règle standard qui protège les pages de connexion contre les attaques par intrusion illicite. Les clients tentant de se connecter plus de 5 fois en 5 minutes sont bloqués pendant 15 minutes.  

Entrez un nom pour la règle et l'URL de connexion. 
