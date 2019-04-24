---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Caching, IBM Cloud Internet Services, Web Application Firewall

subcollection: cis

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"} 

# A propos d'IBM Cloud Internet Services (CIS)
{:#about-ibm-cloud-internet-services-cis}

IBM Cloud Internet Services (CIS), alimenté par Cloudflare, fournit un service Internet rapide, performant, fiable et sécurisé aux clients qui gèrent leur entreprise à l'aide d'IBM Cloud.   

IBM CIS vous garantit une prise en main rapide du produit grâce aux réglages par défaut, que vous pouvez personnaliser comme bon vous semble via l'interface de programmation (API) ou l'interface utilisateur (UI). Les paramètres les plus fréquemment modifiés sont les suivants :

 * **Paramètres du DNS** : vous pouvez soit utiliser IBM CIS pour héberger votre DNS, soit créer des enregistrements CNAME.
 * **Paramètres de chiffrement (TLS)** : la valeur par défaut est le mode `flexible`, qui permet de chiffrer la connexion entre votre hôte et le serveur d'équilibrage des charges IBM CIS, sans chiffrer la communication entre le serveur d'équilibrage des charges IBM CIS et le serveur d'origine.

## Pare-feu d'application Web (WAF)
{:#about-waf}

IBM CIS fournit une fonctionnalité de pare-feu d'application Web qui recherche les activités suspectes. Le pare-feu filtre automatiquement le trafic non autorisé — sur la base de règles prédéfinies — en vue d'examiner les demandes Web GET et POST. Vous pouvez utiliser plusieurs jeux de règles pour déterminer le trafic à bloquer, vérifier ou transmettre. Notre application WAF peut bloquer les spams de commentaires, les attaques de type Cross-Site Scripting (XSS) et les injections SQL.

Vous pouvez activer ou désactiver le pare-feu à votre gré. Toutefois, nous vous conseillons de le laisser activé.

## Protection contre les attaques DDoS
{:#ddos-protection}

IBM CIS fournit une protection contre les attaques DDoS afin de protéger votre site Web contre les hackers, quelle que soit la taille ou la durée de l'attaque.

## Equilibrage de charge
{:#about-load-balancing}

La fonctionnalité d'équilibrage de charge d'IBM CIS s'exécute au niveau du DNS faisant autorité. Elle propose des contrôles de santé avancés qui permettent de surveiller la santé des origines, et ajuste dynamiquement les réponses du DNS. En outre, vous pouvez configurer des règles de géolocalisation pour l'agent de localisation globale (GLB).

### Contrôles de santé
{:#about-health-checks}

Les contrôles de santé d'équilibrage de charge sont réalisés sur des adresses URL spécifiques via des demandes HTTP ou HTTPS régulières, et sont configurés avec des intervalles, délais d'attente et codes d'état personnalisables. Lorsqu'un serveur d'origine est signalé comme étant malsain, les visiteurs sont acheminés à l'écart des menaces, à l'aide de nos routes de reprise en ligne rapide.
 
### Règles de géolocalisation et agent de localisation globale (GLB)
{geo-policies-and-glb}

Les règles de géolocalisation vous permettent de contrôler les serveurs d'origine vers lesquels est acheminé un client donné, en fonction de l'emplacement géographique de ce client. Par exemple, vous pouvez configurer vos règles de géolocalisation de sorte que les visiteurs basés en Europe soient acheminés vers l'origine européenne la plus proche de votre site Web ou application, les visiteurs basés aux Etats-Unis vers une origine nord-américaine, et ainsi de suite.

## Mise en cache
{:#about-caching}

La mise en cache consiste à stocker le contenu statique de vos pages Web le plus près possible des visiteurs de votre site, afin d'améliorer sensiblement les performances du site Web. Notre environnement de diffusion mondialement distribué permet aux propriétaires de contenu Web de fournir une expérience unique au niveau mondial.  
 
## Chiffrement TLS
{:#encryption-with-tls}

Le protocole TLS permet de chiffrer les communications entrantes et sortantes de votre site Web. Un délai de 24 heures peut s'écouler entre le moment où votre site est actif et celui où les nouveaux certificats sont émis.

Pour plus d'informations sur le protocole TLS, voir la rubrique [FAQ](/docs/infrastructure/cis?topic=cis-faq).
