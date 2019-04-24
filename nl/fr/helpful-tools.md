---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: Helpful tools, whois, IPv4

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Outils efficaces pour la gestion de votre déploiement CIS
{:#helpful-tools-for-managing-your-cis-deployment}

Certains outils d'administration système Unix à domaine public peuvent vous aider à gérer votre déploiement IBM CIS.

## Outils sysadmin
{:#cis-sysadmin-tools}

 * whois (outil d'identification de domaine)
 * dig (outil DNS)
 * curl (outil HTTP et HTTPS)
 * netcat (outil IP et port)
 * traceroute (outil réseau)

## Outils commerciaux destinés aux tests externes et à distance
{:#commercial-tools-for-external-and-remote-testing}

 * GTMetrix (http)
 * Test page Web (http)
 * WhatsMyDNS (outil DNS)
 * G Suite Toolbox (DNS et HTTP)

## Outils de recherche de journaux et d'historique
{:#tools-for-looking-at-logs-and-history}

 * Fichiers archives HTTP (fichiers HAR)


### Utilisation de `whois`
{:#using-whois}

`whois` est un outil de ligne de commande Unix que vous pouvez utiliser pour consulter les informations de registre concernant une adresse IP ou un nom de domaine spécifique, par exemple les serveurs de référence du domaine ou le propriétaire d'une adresse IP particulière.

Exemples :

`whois example.com`

`whois 8.8.8.8`

### Utilisation de `dig`
{:#using-dig}

`dig` est un outil de ligne de commande Unix destiné à effectuer des requêtes DNS et à vérifier les enregistrements DNS d'un domaine spécifique. Il est similaire à `nslookup`.

Le schéma de cette commande est : dig <recordtype. <domainname> <options>

**Exemples :**

`dig example.com`

`dig my.example.com`

`dig example.com +trace`

`dig NS example.com`

`dig example.com @ns.example.com`

### Utilisation de `cURL`
{:#using-curl}

`cURL` est un outil de ligne de commande Unix qui vous permet de transmettre des données à l'aide de la syntaxe URL. Il est couramment utilisé pour effectuer des requêtes HTTP ou pour comparer les réponses des serveurs.

Le schéma de cette commande est : `curl -option1 -option2 http://example.com/url`

**Exemples :**

`curl -svo /dev/null http://www.example.com`

`curl -svo /dev/null -A “USER_AGENT_STRING” http://www.example.com`

`curl -svo /dev/null -H “host: www.example.com” http://ORIGIN_IP`

`curl -svo /dev/null -H https://www.example.com --resolve www.example.com:443:ORIGIN_IP`

### Utilisation de `mtr` et `traceroute`
{:#using-mtr-and-traceroute}

MTR et `traceroute` sont des outils de ligne de commande Unix qui vous permettent de mesurer les performances ou la latence le long d'un chemin réseau spécifique vers un hôte ou un serveur de destination spécifique.

**Exemples :**

`mtr -rwc 20 example.com -T -4`
`mtr -rwc 20 8.8.8.8 -T -6`

`traceroute example.com -T -4`

`traceroute 8.8.8.8 -T -6`

| Option | Définition |
|---------|-----------|
| -c | Définit le nombre de pings envoyés |
| -T | Force le routage TCP (normalement ICMP) |
| -4 | Force l'utilisation d'IPv4 |
| -6 | Force l'utilisation d'IPv6 |

### Génération d'un fichier HAR
{:#generating-a-har-file}

Un fichier HAR est un enregistrement des requêtes HTTP provenant d'un navigateur Web. Les navigateurs tels que Chrome possèdent une section Outils pour les développeurs susceptible de vous aider à générer un fichier HAR.
