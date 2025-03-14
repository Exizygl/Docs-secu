# Menaces et types d'attaques

## Danger
- ressource compromise :
    - disfiguration(changrement contenu)
    - potentiel watering hole(ex: malware for everyone)
- vol de données
- Ddos
- attack vers l'hébergueur(attaque par rebond)

## Type d'attaques

- XSS (cross-site scripting): envoie de script malveillant a travel URL,un formulaire envoyé 
    - refléchie : dans url(lien par email)
    - stockée : envoyé dans la base de donée (éxécuté quand call later)
    - DOM : modifié dom en modifiant l'URL

- CSRF (Cross-Site Request Forgery): envoie d'une requete malveillant d'une origine vers une autre origine.


# Bonne pratique

- unité distinctes
    - intéraction bien définie
    - chaque interaction = mech de défence
    - L'architecture et l'hébergement doivent tous les deux être safe.

- moindre privilège
    - role bien définie avec le minimun de droit possible pour l'utilsation de chaque role

- Réduction de la surface d'attaque
    - Ne pas rajouter des composants inutiles ou suceptible d'avoir des failles(module et biblio)
    - minimiser l'exposition au réseau(base de donnée, restraindre port ouvert, https, protection partie administrative, pas exposer fichier sensible, firewall,etc)

- sécu échange donnée

- Conformité du contenu

- Faire des Audit, des vérif de sécurité
    - Audit automatisé(analyse code, dépendance)
    - Audit manuel (config serveur, politique de sécu)
    - strat Audi(quoi, quand)
    - test intrusion( simulation d'attaque par whit-hat hackers)

- Journalisation
    - garder une trace des actions et modif sur le site/serveur
    - pour pouvoir retracer les incidents


# TLS(Transport Layer Security)

- HTTPS
    - Plus sur car utilise le protocole TLS
    - évite attack Man in the middle
    - la norme, évite alerte par nav
    - utilisé TLS 1.2 ou 1.3

- HSTS
    - force accés en HTTPS
    - config en en-tete HTTP avec Strict-Transport-Security

- CT(certificate Transparacy)
    - Protocal pour surveiller les certif SSL/TLS émis
    - permet de check les illégitime
    - a surveiller

# Mécanismes de Sécu web

## SOP(Same-origin policy)

- objectif
  - éviter les attaques
  - Pas de restriction pour la meme origin, restriction pour d'autre origin

- Origin
    - Définit par le protocole, la destination et le port
    - protocole (https), domaine(www.toya.com), port(:80) par défaut 80 ou 443(https)

- Cas particulier
    - iframe (pas de commu entre les 2 origines)
    - XMLHttp request et fetch bloqué sans CORS
    - Web Storage et IndexedDB sont de la same origin
    - cookie ont la meme origin(port pas compris)

- contourner
    - CORS
    - Cross-document messaging / Web Messaging

- pas affecté
    - js
    - css
    - Fichier multimédia

## CORS

- Cors
    - requête Cross-origin(demande envoyé avec en-tete Origin)
    - réponse serveur (envoie origin accepté Access-Control-Allow-Origin: https://www.exemple.com ou *)
    - verif nav(if yes YYYEEEAAAHHH, if no the no)

- security
    - faire un preflight
    - controler l'en tete origin coté serveur pour éviter les attck
    - séparer web service sur d'autre domaine
    - éviter des biblio qui font des appel CORS
    - crossorigin="anonymous" pour protéger les authentifiant

## CSP (Content Security Policy)

- CSP
    - Permet de définir qu'elle resource sont autorisé

- méthode
    - En tete HTTP
    ```
    Content-Security-Policy: default-src 'self'; script-src 'self' https://trusted.cdn.com; report-uri /csp-violation-report-endpoint/

    ```
    - balise Méta
    ```
    <meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self';">

    ```
- plugin dans diff framework

- Directive
    - **script-src, style-src, img-src, media-src, object-src, font-src** : Spécifient les origines autorisées pour les JavaScript, CSS, images, médias (audio/vidéo), objets embarqués (comme PDF) et fontes.
    - **child-src, frame-ancestors** : Définissent les origines autorisées pour les travailleurs (workers) et les frames (iframe).
    - **form-action, connect-src** : Spécifient les origines vers lesquelles les formulaires peuvent être envoyés ou vers lesquelles des connexions asynchrones (XHR, Fetch, WebSockets, EventSource) peuvent être initiées.
    - **default-src** : Spécifie la source par défaut pour toutes les ressources en l'absence de directives spécifiques.
    - **Autres directives globales** : Telles que `upgrade-insecure-requests` (pour forcer les ressources en HTTP à être chargées en HTTPS), `block-all-mixed-content` (pour bloquer le contenu mixte en HTTPS), ou `sandbox` (pour appliquer des restrictions de fonctionnalités du navigateur).


    - Les directives CSP acceptent des valeurs sous forme de liste de sources de contenu, qui peuvent être :
        - **Origines** : URL complète (par exemple, `https://domaine.fr`), ou partie d’une origine avec des caractères génériques (par exemple, `*://*.domaine.fr:*`).
        - **Mots-clés** :
        - **'none'** : Désactive la prise en charge du type de ressource.
        - **'self'** : Autorise la ressource provenant de la même origine que la page actuelle.
        - **'unsafe-inline'** : Permet l'exécution de code inline (JavaScript ou CSS intégré dans la page HTML).
        - **'unsafe-eval'** : Permet l’utilisation de fonctions d’évaluation de code JavaScript (comme `eval()`).
        - **Empreintes ou nonce** : Autorise un script ou un style inline spécifique grâce à une empreinte ou un nonce sécurisé.
        - **strict-dynamic** : Permet la propagation de l'autorisation pour les ressources chargées dynamiquement (niveau CSP 3).

- Par défaut CSP bloque plusieurs vuln XSS et encourage les bonne pratiques 

- Protection contre le clickjacking
    - empéché l'iframemisation du site par un autre si pas dans la liste des origin added.
    - X-Frame-Option pour certein nav

- Rapport de violation
    - envoie rapport a un URL
    - option Report-only pour pas bloqué
    - risque fuite info sur les vunérabilité
    - risque sur la confidentialité
    - augmentation de la surface d'attaque
    - en congig pour etre safe

- Maitrise rapport silencieux
    -control des orgin pour ping



# XSS et bonne pratique

- Pas de méthode exécutent du code HTML ou JS seulement du texte
- dissocier les donnée(HTML, CSS, JS séparer)
- donner encoder (ex JSON)
- échapement du contenu
- vérif conformiter donnér
- JSPN.parse() not Eval
- API DOM sécuriser(textContent)


# Referrer policy
- l'envoie de donner vers une nouvelle page pour dire d'ou le user vient dans l'entete referer-policy
    - option pour limiter les info d'envoie(ex: https to http, diff origin)
    - posibilité de congig pour chaque link

# Web Storage, indexedb et cookies

- Webstorage(local strorage et session storage)
    - toutes meme origin can see them
    - persistence donnée sensible
    - à use pour pref only and no risky data.
    - analyse de risque avant use
    - préviligier cookies sécurisé et identififiant coté serveur de session temp.

- indexedb
    - Clé/objet
    - SOP(pas de restriction)
    - can be use in a web worker
    - vulnérable au XSS
    - pas restriction dans SOP
    - use for non-critiq(ise en chache state)
    - analyse risque avant

- cookies
    - pas stocké donnée sensible
    - cloisonner les sessios en utilisant des noms de domaine distincts
    - define path pour limiter le path cookie.
    - utilisé secure pour l'envoie.
    - limiter envoie cross-site
    - valider et controle les cookies coté serveur
    - condidèrer les cookies comme volatile

# XMLHttp et fetch

 - requet XHR
    - Eviter injection XSS via innerHTML, formater avec Json ou XML

- API
    - verififier sécurité de la pméthodes http

- get
    - risque
        - données en clair dans l'url
        - réponse peut etre en cache.
        - peut etre intercepter
    - use
        - données publique (barre de recherche)
        - pas de change server side.

- post
    - better
        - no info in URL
        - less chance of a interception
        - avoid cache

- Put
    - even better
        - Preflight CORS by default
        - less chance of CSRF

- bien config CORS

- CSRF token
