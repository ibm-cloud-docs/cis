---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: CIDR blocks, Whitelist Block Challenge, IBM Cloud Internet Services, security features

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Comment IBM Cloud Internet Services (CIS) sécurise-t-il vos activités ?
{:#how-cis-keeps-your-work-secure}

IBM CIS est un service Cloud distribué dans le monde entier qui bloque les menaces et limite les bots et autres moteurs d'exploration malveillants, susceptibles de gaspiller votre bande passante et vos ressources serveur. IBM CIS fonctionne en tant que proxy inverse HTTP(S) global et en tant que prestataire de services DNS gérés. Votre trafic Web est acheminé sur notre réseau global intelligent afin d'optimiser à la fois vos performances et votre sécurité.

![security-graphic.png](images/security-graphic.png)

Voici un bref aperçu des fonctionnalités :

## Caractéristiques de sécurité
{:#cis-security-features}

 * [Enregistrements DNS](/docs/infrastructure/cis?topic=cis-dns-concepts#proxying-dns-records) proxy ou [GLB](/docs/infrastructure/cis?topic=cis-global-load-balancer-glb-concepts) pour utiliser les fonctionnalités de sécurité. Cela permet au trafic de circuler sur nos serveurs et les données peuvent être surveillées.
### Pare-feu d'application Web (WAF)
{:#cis-web-application-firewall}

 * WAF est mis en oeuvre à travers deux jeux de règles : [OWASP](/docs/infrastructure/cis?topic=cis-owasp-rule-set-for-waf) et [CIS](/docs/infrastructure/cis?topic=cis-waf-settings#cis-rule-set-for-waf). 
### Atténuation des attaques DDoS illimitées
{:#cis-unlimited-ddos-mitigation}

 * L'atténuation des attaques DDoS est généralement un service coûteux dont le coût peut augmenter en cas d'attaque. Nous incluons une limitation illimitée des attaques DDoS avec CIS, sans frais supplémentaires. 

## Normes et plateforme de sécurité
{:#security-standards-and-platform}

 * TLS (SHA2 et SHA1)
 * IPv6
 * HTTP/2 et SPDY

## DNS
{:#cis-dns}

 * Réseau anycast global
 * DNSSEC

## Attaques réseau et mesures d'atténuation
{:#network-attacks-and-mitigation}

En règle générale, les attaques peuvent être classées en deux catégories

| Attaques de la couche 3 ou 4 | Attaques de la couche 7 |
|------------------------------|-----------------|
|Ces attaques consistent à saturer le trafic au niveau de la couche 3 du modèle OSI (couche réseau), telles que les inondations ICMP, ou au niveau de la couche 4 (couche transport), telles que les inondations SYN TCP ou les inondations SYN par réflexion |Ces attaques envoient des demandes malveillantes au niveau de la couche 7 du modèle OSI (couche application), telles que des inondations GET.  |
| Ces attaques sont bloquées automatiquement au niveau de notre serveur de périphérie | Nous traitons ces attaques à l'aide du “Mode défense”, du pare-feu d'application Web (WAF) et des paramètres de niveau de sécurité |

## Pare-feu IP
{:#cis-ip-firewall}

IBM Cloud Internet Services propose plusieurs outils de contrôle de votre trafic afin de protéger vos domaines, URL et répertoires contre les volumes de trafic, certains groupes de demandeurs et certaines adresses IP de demandeurs. Cette section détaille les outils disponibles. 

### Règles IP
{:#cis-ip-rules}

Les règles IP vous permettent de contrôler l'accès à des adresses IP spécifiques, des plages IP, des pays spécifiques, des ASN spécifiques et certains blocs CIDR. Les actions disponibles sur les demandes entrantes sont : 
  * Liste blanche 
  * Blocage  
  * Demande d'authentification (Captcha) 
  * Demande d'authentification JavaScript (demande d'authentification IUAM)

Par exemple, si vous remarquez qu'une adresse IP particulière provoque des demandes malveillantes, vous pouvez bloquer cet utilisateur par adresse IP. 

### Règles de blocage des agents utilisateurs 
{:#user-agent-blocking-rules}

Les règles de blocage de l'agent utilisateur vous permettent d'agir sur n'importe quelle chaîne de l'agent utilisateur que vous sélectionnez. Cette fonctionnalité fonctionne comme le verrouillage de domaine, comme décrit précédemment, à l'exception que le bloc examine la chaîne entrante de l'agent utilisateur plutôt que l'adresse IP. Vous pouvez choisir comment traiter une demande de correspondance avec la même liste d'actions que celle que vous avez établie dans les règles IP (Blocage, Demande d'authentification et Demande d'authentification JS). Notez que le blocage d'agent utilisateur s'applique à l’ensemble de votre zone. Vous ne pouvez pas spécifier les sous-domaines de la même manière que vous pouvez verrouiller le domaine. 

Cet outil permet de bloquer toute chaîne d'agent utilisateur que vous jugez suspecte.  

### Verrouillage de domaine
{:#cis-domain-lockdown}

Le verrouillage de domaine vous permet de mettre en liste blanche des adresses IP et des plages d'adresses IP spécifiques de sorte que toutes les autres adresses IP soient sur liste noire. Le verrouillage de domaine prend en charge : 

  * Sous-domaines spécifiques. Par exemple, vous pouvez autoriser l'accès IP `1.2.3.4` au domaine `foo.example.com` et autoriser l'accès IP `5.6.7.8` au domaine `bar.example.com`, sans autoriser nécessairement l'inverse.
  * URL spécifiques. Par exemple, vous pouvez autoriser l'accès IP `1.2.3.4` au répertoire `example.com/foo/*` et autoriser l'accès IP `5.6.7.8` au répertoire `example.com/bar/*`, sans autoriser nécessairement l'inverse. Cette fonctionnalité est utile lorsque vos règles d'accès nécessitent une plus grande granularité, car, avec les règles IP, vous pouvez appliquer le blocage à tous les sous-domaines du domaine actuel ou à tous les domaines de votre compte et vous ne pouvez pas spécifier d'URI. 

### Réussite à la demande d'authentification
{:#cis-challenge-passage}

Situé dans les paramètres de sécurité **Avancés**, ce paramètre vous permet de contrôler la durée pendant laquelle un visiteur ayant réussi une demande d'authentification ou une demande d'authentification JavaScript aura accès à votre site avant de devoir à nouveau s'authentifier. Ce mécanisme est basé sur l'IP du visiteur et ne s'applique donc pas aux demandes d'authentification présentées par les règles WAF, car elles sont basées sur une action que l'utilisateur effectue sur votre site. 

### Contrôle d'intégrité navigateur 
{:#cis-browser-integrity-check}

Ce paramètre est situé dans les paramètres de sécurité **Avancés**. Le contrôle d'intégrité du navigateur recherche les en-têtes HTTP les plus fréquemment utilisés par les spammeurs. Il leur refuse alors tout accès à votre page. Il bloque et conteste également les visiteurs qui ne possèdent pas d'agent utilisateur ou qui ajoutent un agent utilisateur qui n'est pas standard (cette tactique est généralement utilisée par les bots, les moteurs d'exploration ou les API malveillantes). 
