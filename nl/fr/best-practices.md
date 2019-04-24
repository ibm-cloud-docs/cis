---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Best practices, CIS setup

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}

# Meilleures pratiques pour la configuration CIS
{:#best-practices-for-cis-setup}

IBM CIS étant placé à l'extrémité du réseau, certaines mesures supplémentaires sont nécessaires pour veiller à l'intégration harmonieuse de vos services CIS. Vous trouverez ci-dessous les meilleures pratiques en matière d'intégration CIS avec vos serveurs d'origine. 

Vous pouvez réaliser ces opérations avant ou après avoir changé votre DNS et activé votre service proxy. En suivant ces recommandations, vous garantirez une intégration parfaite d'IBM CIS à vos serveurs d'origine. De plus, vous éviterez les problèmes liés à l'API ou au trafic HTTPS, et vous permettrez aux journaux de collecter les vraies adresses IP de vos clients et non les adresses IP CIS de protection.

Voici les mesures supplémentaires :

 * Meilleure pratique 1 : Restaurer les adresses IP d'origine de vos clients
 * Meilleure pratique 2 : Incorporer les adresses IP CIS
 * Meilleure pratique 3 : Vérifier que les paramètres de sécurité n'interfèrent pas avec le trafic API
 * Meilleure pratique 4 : Configurer vos paramètres de sécurité de la façon la plus rigoureuse possible
 
## Meilleure pratique 1 : Savoir restaurer les adresses IP d'origine de vos clients
{:#best-practice-know-how-to-restore-origininating-ip}

En qualité de proxy inverse, nous fournissons l'adresse IP d'origine dans les en-têtes suivants :

  * `CF-Connecting-IP`
  * `X-Forwarded-For`
  * `True-Client-IP` (facultatif)

Vous pouvez restaurer les adresses IP utilisateur à l'aide de plusieurs outils, pour des infrastructures telles que Apache, Windows IIS et NGINX.

## Meilleure pratique 2 : Incorporer les adresses IP CIS pour une intégration en douceur
{:#best-practice-incorporate-cis-ip-addresses}

La procédure est la suivante :

  * Supprimez toutes les limites d'adresses IP CIS.
  * Configurez vos listes de contrôle d'accès (ACL) de manière à n'autoriser que les adresses IP provenant de CIS ou d'autres tiers de confiance.

Pour obtenir la liste à jour des plages d'adresses IP valides pour IBM CIS, [cliquez ici](/docs/infrastructure/cis?topic=cis-ibm-cloud-cis-whitelisted-ip-addresses).

## Meilleure pratique 3 : Vérifier que les paramètres de sécurité n'interfèrent pas avec le trafic API
{:#best-practice-review-security-settings-interference}

En règle générale, IBM CIS accélère le trafic API en supprimant la surcharge de connexion. Toutefois, la configuration de la sécurité par défaut peut interférer avec de nombreux appels API. C'est pourquoi, nous vous conseillons d'effectuer quelques actions supplémentaires afin d'empêcher toute interférence avec le trafic API lorsque la mise en proxy est activée.

 * Désactivez les fonctionnalités de sécurité de façon sélective, en utilisant les paramètres **Règles de page**.
   * Créez une règle de page avec le masque d'URL de votre API, par exemple `api.example.com`
   * Ajoutez les comportements de règles suivants :
     * Définissez **Niveau de sécurité** sur **Essentiellement désactivé**
     * Définissez **TLS** sur **Désactivé**
     * Définissez **Contrôle d'intégrité navigateur** sur **Désactivé**
   * Sélectionnez **Provisionner 1 ressource**

 * Vous pouvez également désactiver totalement l'option **Pare-feu d'application Web** sur la page de sécurité.

| *A quoi sert le contrôle d'intégrité du navigateur ?* | 
|------------------------------------------------|
| *Le contrôle d'intégrité du navigateur recherche les en-têtes HTTP les plus fréquemment utilisés par les spammeurs. Il leur refuse alors tout accès à votre page. Il bloque également les visiteurs qui ne possèdent pas d'agent utilisateur ou qui ajoutent un agent utilisateur qui n'est pas standard (cette tactique est généralement utilisée par les bots, les moteurs d'exploration ou les API malveillantes).* |

## Meilleure pratique 4 : Configurer vos paramètres de sécurité de la façon la plus rigoureuse possible
{:#best-practice-configure-stict-security-settings}

CIS propose des options de chiffrement de votre trafic. En notre qualité de proxy inverse, nous fermons les connexions TLS au niveau de nos centres de données et nous ouvrons une nouvelle connexion TLS vers vos serveurs d'origine. Lors de la fermeture de CIS, vous pouvez télécharger un certificat personnalisé depuis votre compte, utiliser un certificat générique mis à votre disposition par CIS, ou les deux.

### Télécharger un certificat personnalisé
{:#strict-upload-custom-cert}
 
Vous avez la possibilité de télécharger vos clés publique et privée lorsque vous créez un domaine d'entreprise. Si vous téléchargez votre propre certificat, vous êtes immédiatement assuré de sa compatibilité avec le trafic chiffré et vous gardez le contrôle sur votre certificat, par exemple, un certificat à confirmation étendue (EV). Rappelez-vous que vous êtes responsable de la gestion de votre certificat si vous devez télécharger un certificat personnalisé. Par exemple, IBM CIS ne contrôlera pas la date d'expiration de vos certificats. 
 
### Ou utiliser un certificat fourni par CIS
{:#strict-utilize-cert-cis-provisioned}
 
IBM CIS s'est associé à un grand nombre d'autorités de certification (CA) pour fournir des certificats génériques à vos clients, par défaut. Une vérification manuelle peut être requise pour configurer ces certificats, et votre équipe de support peut vous aider à réaliser ces étapes supplémentaires.
 
### Modifier votre paramètre TLS en **Signé CA de bout en bout**
{:#strict-change-tls-setting}
 
La plupart de nos clients d'entreprise utilisent le paramètre de sécurité signé par une CA de bout en bout. Le paramètre **Signé CA de bout en bout** nécessite qu'un certificat signé par une autorité de certification valide soit installé sur votre serveur Web. La date d'expiration ne doit pas être dépassée, et le certificat doit posséder un *nom d'hôte* ou un *autre nom de sujet* correspondant.

