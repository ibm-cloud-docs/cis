---
copyright:
  years: 2018
lastupdated: "2018-03-06"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Jeu de règle WAF par défaut

| Règle | Action |
|----------|---------------|
|Nombre de botnets|demande d'authentification
|Botnet CtrlFunc|demande d'authentification
|Faille LFI générique au niveau des chemins les plus courants dans ARGS|blocage
|Règle générique d'inclusion de fichiers locaux (LFI) avec améliorations|simulation
|Faille LFI générique au niveau des chemins les plus courants dans l'URI|blocage
|Faille LFI générique au niveau des chemins les plus courants dans l'URI sans post-traitement|blocage
|Faille RCE générique au niveau des commandes les plus courantes|blocage
|Faille RCE générique au niveau des commandes shell|blocage
|Faille RCE générique au niveau des commandes réseau les plus courantes|simulation
|Empêcher les failles RCE au niveau de la famille de commandes nc|blocage
|Rechercher les failles SQLi|blocage
|Bloquer la fonction de chaîne SQLi à l'aide de techniques d'évasion|blocage
|Bloquer la concaténation de chaîne SQLi à l'aide de techniques d'évasion|blocage
|Bloquer la recherche de mise en veille SQLi|blocage
|Bloquer la recherche de mise en veille SQLi (attente)|blocage
|Tentative SQLi (Conditional) |blocage
|Tentative SQLi (Where)|blocage
|Tentative SQLi (IS NULL)|blocage
|Tentative SQLi (Equation) [ ]|blocage
|Tentative SQLi (Math Comparison) []|blocage
|Tentative SQLi (Math Comparison) Beta []|simulation
|Tentative SQLi (End comparison) PATH []|blocage
|Tentative SQLi (End comparison) URI []|blocage
|Tentative SQLi (End comparison) ARGS []|blocage
|Tentative SQLi (Sub query Evasion) []|blocage
|Tentative SQLi (Wildcard Evasion) []|blocage
|Tentative SQLi (Early Func) []|blocage
|Tentative SQLi (Embedded Func) []|simulation
|Tentative SQLi (MultiLevel Func) []|blocage
|Tentative SQLi (Union Vector) []|simulation
|Recherche SQLi|blocage
|Interdire les commentaires SQLi |blocage
|Interdire les chaînes se terminant par des commentaires SQLi |simulation
|Tentative SQLi (Wildcard Escape)|blocage
|Bloquer les en-têtes X-Forwarded-Host non valides |demande d'authentification
|Bloquer les requêtes des systèmes de contrôle de version|blocage
|Bloquer le bot de commentaire du signal Wow!|blocage
|CVE-2014-6271 - ShellShock|blocage
|CVE-2014-6271 - ShellShock|blocage
|Inondation DDoS classique|demande d'authentification
|Analyse XSS classique|demande d'authentification
|Analyse XSS à l'aide du mot clé alert|demande d'authentification
|Analyse XSS à l'aide de balises script|blocage
|Analyse XSS à l'aide d'événements javascript|blocage
|Analyse XSS à l'aide d'événements javascript (Strict)|demande d'authentification
|Analyse XSS à l'aide de l'URI javascript|demande d'authentification
|Faille XSS masquée dans les URI de données en base64 |demande d'authentification
|Détection XSS atob() à l'aide de techniques d'évasion|blocage
|Détection XSS eval() à l'aide de techniques d'évasion|blocage
|Détection XSS lenient eval() à l'aide de techniques d'évasion|simulation
|Bloquer le moteur d'exploration semalt|blocage
|Annuler les bots DDoS espacés|blocage
|Arrêter les en-têtes de cookie NULL|blocage
|Interdire les balises de code PHP dans les en-têtes|blocage
|Bloquer les agents utilisateur Mozilla mal formatés|blocage
|Analyse XSS générique|demande d'authentification
|Tentative XSS SVG|demande d'authentification
|Empêcher IIS DoS - CVE-2015-1635 []|blocage
|Empêcher les faux googlebots d'explorer vos pages|blocage
|Empêcher les faux bingbots d'explorer vos pages|blocage
|Empêcher les faux BaiduBots d'explorer vos pages|blocage
|Empêcher les faux yandexbot d'explorer vos pages|blocage
|Bloquer les faux agents d'utilisateur baidu utilisés dans les attaques DoS|blocage
|Bloquer toutes tentatives visant à obtenir des informations sur le serveur d'origine|blocage
|Empêcher l'accès aux extensions susceptibles d'être utilisées par les éditeurs de texte pendant l'enregistrement/la sauvegarde|blocage
|Bloquer les tentatives d'accès à la page de statut apache/statut serveur|simulation
|Annuler les analyses du scanner Acunetix|demande d'authentification
|Annuler les analyses Java du scanner Acunetix|demande d'authentification
|Injection SQL Joomla CVE-2015-7857 |blocage
|Se connecter lorsque deux en-têtes sont envoyés avec une requête|simulation
|Détecter les faux IE6 [Type B]|demande d'authentification
|Détecter les faux IE6 [Type C]|demande d'authentification
|Bloquer les agents utilisateur Google Chrome usurpés/corrompus|blocage
|Bloquer les tentatives d'injection sur l'en-tête d'alias nginx|demande d'authentification
|Bloquer les attaques par force brute connues|demande d'authentification
|Bloquer les tentatives d'exploitation d'Imgmagik CVE-2016-3714 |blocage
|Bloquer les tentatives d'exploitation de GraphicsMagick CVE-2016-5118 |blocage
|PHPMailer RCE - CVE-2016-10033 Type A|blocage
|PHPMailer RCE - CVE-2016-10033 Type B|blocage
|Bloquer les tentatives d'exploitation CVE-2017-5638 (Content-Type)|blocage
|Empêcher les tentatives IIS RCE CVE-2017-7269 |blocage
|Tentative d'inclusion SSI dans Struts/OGNL (CVE-2017-9791 etc.)|blocage
|Bloquer les tentatives d'injection SQL 'drop table ...' []|simulation
|Bloquer les requêtes HTTP avec un agent utilisateur correspondant aux 26 lettres de l'alphabet uniquement|blocage
|Suppression des requêtes avec l'en-tête X-Requested-With et l'ID APK de l'attaque Endurance|simulation
|Suppression des requêtes correspondantes CVE-2017-9805|blocage
|Analyser les commentaires SQLi|simulation
|Tentative SQLi []|simulation
|Tentative SQLi []|blocage
|Commentaires SQLi interparamètres []|simulation
|Analyse XSS à l'aide d'événements javascript|simulation
|Protection RFI exécutable|simulation
|Protection RFI redirigée|simulation
|SQLi pour UNION SELECT ALL NULL|simulation
|CVE-2017-7525 - Struts / Jackson RCE|blocage
|Mauvais AU :: Tentative par force brute|demande d'authentification
|Faux AU :: Utilisé dans les attaques par force brute Wordpress|demande d'authentification
|Faux AU :: Utilisé dans les attaques par force brute Wordpress|demande d'authentification
|Faux AU :: Utilisé dans les attaques par force brute Wordpress|demande d'authentification
|Faux AU :: Utilisé dans les attaques par force brute Wordpress|demande d'authentification
|Faux AU :: Utilisé dans les attaques par force brute Wordpress|demande d'authentification
|Faux AU :: Utilisé dans les attaques par force brute Wordpress|demande d'authentification
|Blocage de la vulnérabilité mfunc WordPress|blocage
|Blocage du favicon CDorked.A|blocage
|Règle visant à atténuer Atlassian Confluence Security Advisory 2015-01-21|demande d'authentification
|Exploiter SQLi DB 28129 Practico CMS|blocage
|WebHive LOIC|demande d'authentification
|Script d'attaque UITSEC|blocage
|CVE-2013-2251 - Apache Struts RCE|simulation
|Supprimer les requêtes essayant d'exploiter CloudBees Jenkins RCE (CVE-2017-1000353)|simulation
|Atténuation pour Apache Tomcat CVE-2016-6816|blocage
|Bloquer les larges requêtes vers xmlrpc.php pour Drupal CMS|blocage
|Bloquer les requêtes avec des arguments étranges de type tableau|blocage
|Bloquer Rosetta Flash|demande d'authentification
|Bloquer Rosetta Flash|demande d'authentification
|Exploitation Joomla JCE|blocage
|Suppression de la tentative RCE agent utilisateur/X-Forwarded-For sur Joomla. CVE-2015-8562|blocage
|Bloquer l'enregistrement utilisateur non autorisé dans Joomla CVE-2016-8870|blocage
|Bloquer l'enregistrement utilisateur non autorisé dans Joomla CVE-2016-8869|blocage
|Bloquer l'élévation de privilèges sur groupe CVE-2016-9838|blocage
|Bloquer SQLi com_fields SQLI dans Joomla|blocage
|Bloquer SQLi com_fields SQLI dans Joomla|blocage
|Bloque l'exploitation Magento intitulée SUPEE-5344|blocage
|Interdire l'accès aux fichiers d'installation Magento APPSEC-1421|blocage
|Interdire RCE via l'API Magento APPSEC-1420 (Type A)|blocage
|Interdire RCE via l'API Magento APPSEC-1420 (Type B)|blocage
|Exploitation d'exécution de code à distance Apache/PHP 5.x|demande d'authentification
|Interdire les URI php:// pour éviter les attaques RCE et LFI|blocage
|Interdire le brouillage PHP pour éviter les attaques RCE|blocage
|Requête Plone interdite|blocage
|Vulnérabilité WHMCS 5.2.7|blocage
|Vulnérabilité WHMCS 5.2.8|blocage
|Vulnérabilité WHMCS 5.2.10|blocage
|Blocage WordPress Pingback|demande d'authentification
|Désactiver WAF pour wp-admin|activation
|Désactiver WAF pour WordPress post.php|activation
|Exploitation de l'injection SQL en aveugle DB 28485|blocage
|Protection Wordpress Jetpack|blocage
|Interdire à timthumb d'extraire des fichiers php|blocage
|Bloquer les scripts dynamiques dans les répertoires cache|blocage
|Interdire à timthumb d'extraire des sources externes|simulation
|Yoast WordPress - SQLi en aveugle|blocage
|Bloquer les noms d'hôte anormalement longs dans les rétroliens|blocage
|Bloquer les commentaires anormalement longs|blocage
|Bloquer l'attaque XSS TwentyFifteen DOM|blocage
|Empêcher l'injection SQL CVE-2015-2213 dans le système de commentaires|blocage
|Corriger une faille RCE dans EWWW Image Optimizer pour WordPress|blocage
|Désactiver WAF pour les requêtes de sauvegarde VaultPress vérifiées|activation
|Empêcher une faille RCE Mailport via téléchargement de fichier|blocage
|Empêcher une faille RCE via téléchargement dans Revolution Slider|blocage
|Empêcher l'exécution des fichiers qui se trouvent dans les programmes de décompression de mise à jour|blocage
|Empêcher une faille RCE via téléchargement dans Gravity Forms|blocage
|Empêcher l'exploitation de l'API wp-json Type A|blocage
|Empêcher l'exploitation de l'API wp-json Type B|blocage
|Empêcher l'exploitation de l'API wp-json Type C|simulation
|Protection contre les attaques LFI wp-config.php|blocage
|Supprimer le code XML dans la zone post meta|blocage
|CVE-2018-6389 : suppression des requêtes qui tentent des attaques par amplification Dos sur le script JS|simulation
