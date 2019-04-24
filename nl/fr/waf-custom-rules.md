---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-14"

keywords: WAF Custom Rules, Custom WAF Rules

subcollection: cis

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:DomainName: data-hd-keyref="DomainName"}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:generic: data-hd-programlang="generic"}


# Règles WAF personnalisées 
{:#waf-custom-rules}

Accédez aux règles WAF personnalisées via **Sécurité > Pare-feu d'applications Web > Règles personnalisées**. Les règles WAF sont disponibles sur les forfaits Enterprise et sont créées en fonction des exigences spécifiques d'un client donné et/ou des masque de trafic de son site Web. Cela signifie que vous pouvez nous demander de bloquer pratiquement toute combinaison de caractéristiques d'une demande.  

Les règles WAF personnalisées s’adressent aux situations dans lesquelles IBM WAF n’a pas encore de règle en place et où l'auteur de l'attaque utilise un masque spécifique ou un agent utilisateur spécifiquement conçu pour la structure de votre site Web. Dans ces situations, vous pouvez créer une règle personnalisée pour votre propriété Web. 

## Demande d'une règle personnalisée 
{:#request-a-custom-rule}

Pour demander une règle, envoyez un e-mail à l'adresse wafsup@us.ibm.com avec les exigences de la règle ou les masque de trafic.  

Fournissez autant d'informations que possible, y compris : 
* Des journaux d'accès présentant un échantillon d'environ 100 requêtes présumées malveillantes.
* Un exemple de demande POST incluant les données POST (si les demandes ont un corps POST) pour déterminer si la demande contient tout ce que nous pouvons bloquer ou déclencher. 
* Si vous souhaitez que les demandes soient totalement bloquées ou contestées en cas de faux positifs potentiels. 
* Les domaines spécifiques auxquels vous souhaitez appliquer ces règles. 
* Si vous souhaitez que les règles soient activées ou désactivées par défaut.

Une fois vos règles WAF personnalisées créées, vous devez activer toutes les règles personnalisées pour qu'elles prennent effet. {:note}
