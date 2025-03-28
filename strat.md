# Sommaire

- Introduction
    - Contexte
    - Impact
    - Organisation du document
- Type d'attaque
- Philosophie de developement


- Base de donnée
    - Authentification
    - UUID
    - Encryptions
    - Les clés d’encryptage 
    - ORM
    - Site de sauvegarde
    - Copie de la base de données
    - Audit 
- Back
    - validation d'entrée
    - traitement des données et vérification des sorties
    - authentification
      
    - autorisation d'accés
    - Mot de passe
    - Menace
    - jwt
    - waf
   
- Front
    - TLS
    - SOP
    - Cors
    - CSP
    - défence XSS
    - referrer policy
    - web storage
    - cookie
    - XMLhttp et fetch
    - HTML annd JS


# Introduction 

 

## Contexte 

The goal of documentation is to present the security measure we will take to ensure the security of pire2pire.com. Today, the danger of cyber threats is omnipresent and must ensure that security measure to protect against those threats are taken at every step of the project, Strating with this document to the conception of the site and its functionality to the development and release. 

This document as for goal to be understandable for everyone from the debutant to the expert, that mean it will be present in a pedagogical way, we will focus on the different dangers, present and explain a potential solution to those danger. 

The pire2pire.com is a website is a e-learning website where people will be able to learn different course, there will be visitor, student, coach. 

## Impact 

A badly secure website can cause a lot of arms, here are a list of danger that may this includes: 

- Sensitive information being stolen: Malicious actors may obtain access to sensitive data like financial information, a corporation’s confidential information or an individual personal information, the danger is that the attacker may use those stolen data for identity theft, blackmail or fraud. 

- Damage to brand: a website can be disfigured, that mean that inappropriate content can be insert on it, political message can be insert, advertisement for products can be insert or just a warning that the website has been hacked, all of those will damage the trust of current and potential costumer. In case of actual suceful attack it is really advice to inform the costumer in the shortest delay so that the costumer can protect themselves and be more careful against potential identity theft or fraud 

- Criminal activity:  Gaining information costumer or taking control of the website can lead to a lot of criminal activity like spreading malware, posting illegal content, conducting phishing or use the platform to attack other system or person having an access with it. 

- Banning or suspension: Content that is insert on the website be suspicious content, either spam, malware or link to distrustful website. Those can be flag as dangerous or suspicious by search engine, those flag scan can lead the hacked website to be in turn flag as suspicious which will impact search engine result (up to removal of the website from result) and affect traffic to the website. 
In the worst-case scenario the host of the site may shit-down the website 

- Harm to the user experience: One of the side effects of being hack may be simply activity or code that slow the reaction speed to request which will ruin user experience, to add to that problem there is the possibility of spam and malware to also affect the user experience negatively, which  may lead to users leaving the website 

- Financial losses: Access to financial data may lead to financial loss especially if the hacker gains enough access to do transaction, the loss of costumer may also impact revenue, there is also the potential compensation to costumer and cost of dealing and repairing the security breach 

## Organization of the documentation 

 	This document will present the different type of danger that may happen during the lifetime of the site we will then present the different how those problem will be stop, then we will detail all the protection we will in each part of the documentation from the database to the front 

 
# RGPD
 Le Règlement Général sur la Protection des Données(RGPD) est une reglemenation de l'union européen que le site devra suivre et appliquer, il se concentre le traitement des données personnel est donne plus de controle au utilisateur.

 Nous devrons donc:

    - Consentement: demandé le conce,tement claire et explicite au utilsateur avant toutes collecte de donnée.

    -Droit: L'utilisateur a le droit d'accéder  au information récoltét, de les rectifier, le droit de portabilité,  le droit d'opposition du traitement des donnée ainsi que le droit à l'oubli

    - La responsabilité: on a l'obligation de protéger c'est donnée, ce dossier étant une explication de qu'elle messure on va mettre d'un point technique.

    - la notification : toutes violation  de donnée doit etre informer au authorité dans les prochaine 72h

En cas de non-conformité avec la Réglémenation, l'entreprise  peut  recevoir une amende entre 20 millions d'euros et 4% du chiffre d'affaire mondial 


# Type d'attaques rencontrer 

 

Ici nous allons présenter les différents types d’attaques que ce guide a pour but de prévenir : 

 

XSS : L’attaque Cross-Site Scripting consiste a injecté de code (Javascript ou HTML) dans une page web pour obtenir un comportement visé quand ce code sera exécuté, le but étant de récupérer des informations sur des utilisateur d’un site 

 

CSRF : L’attaque Cross-site Request Forgery consiste à tromper un utilisateur pour lui forcer à faire une action voulu sur un site donné depuis un site tier, par exemple envoyer une requête cachée à pire2pire.com en interagissant sur un site créer par l'hacker  

 

SSRF : L’attaque Serve-side Request forgery consiste à demander au serveur d’effectuer des requêtes vers une destination choisies par l’attaquant en profitant éventuellement des privilèges du serveur. 

 

SQLi : L’attaque SQL injection consiste à envoyer une requête pas prévu par les fonctions du site ou les droits d’utilisateur pour affecter la base de données, cela donne la possibilité à l’attaquant de faire ce qu’il veut. 

 

LFI/RFI : L’attaque Local/Remote File Inclusion consiste à trouver un moyen d’accédé à un fichier local ou distant sur le site normalement pas accessible pour une personne n’ayant pas les droits 

Ddos: l'attaque Ddos consiste a fiare un grand nombre de demande automatisé au serveur pour le surchargés et pertubé l'utilisation des autre utilisateur en ralentissant voir rendre incapable au serveur de répondre au demande.    

XXE : L’attaque XML External Entity  consiste à injecter du XML mal pour exécuter ce code et obtenir des accès normalement impossibles. 

 
# Philosophie de développement  

 

Pour protéger de c’est attaque certaines mesures vont être respecter à travers le développement de du projet. 

 

Unités distinctes : Chaque couche de l’application sera séparée (Front, back, base de données, API), cette séparation nous permettra de bien définir les interactions entre chacune d’entre elle, ces interactions étant bien définit nous allons pouvoir développer des mécanismes de défence et de vérification pour chacune d’entre elle 

 

Moindre privilège : Le moindre privilège consiste à donner le moins de possibilité d’action possible à chaque rôle des utilisateurs, les visiteurs du site ne doivent pas avoir accès à des fonctions dédiées aux étudiants, coachs ou administrateurs 

 

Réduction de la surface d’attaque : Plus nous ajoutons de composants au site et plus agrandissons l’exposition aux réseaux de notre site, plus il y a d’opportunité de se faire attaquer, nous n’allons pas rajouter des composants inutilise ou non-sécurisé ainsi que retirer ce qui sont seulement utiles au cours de la phase de développement quand nous passeront à la phase de déploiement. De même pour l’exposition réseau, plus on en a, plus il y a de vulnérabilité, nous devons limiter les accès réseau. 

 

 

Sécurisation des échanges de donnée : Tout échange de donnée doivent être sécurisé pour ne pas être intercepté pendant son transfert, nous allons utiles des protocoles comme le protocole Https pour la protection. 

  

Conformité du contenu : Nous allons assurer la conformité des données pour faire en sorte que le site apparaisse dans le navigateur des utilisateurs comme il a été conçu pour assurer l’expérience promise. 

 

Journalisation : La journalisation consiste à enregistrer les interactions sur chaque couche du site des journaux d’évènement pour garder une trace de tout ce qui s’y passe ainsi que quand ces évènements se sont passés, le but étant que en cas de de problème, attaque ou tentative d’attaque, on puisse retracer l’attaque pour corriger de potentielle faille ainsi qu'avoir une idée de l’ampleur des dégâts. 



# La Base de données. 

 

La base de données est au cœur de la sécurité du site, c’est l’endroit où toutes les informations importantes se trouve et les protections de la base de données sont extrêmement importante au cas où les protections des couches rencontrées avant on était contourné ou si l’attaquant arrive à attaquais directement la base de données 

 

## Authentification 

Utiliser un système d’authentification est important pour protéger une base de données, ce système permet de créer des rôles qui gèrent les droits sur la base de données, cela permet de gérer ceux qui peut être vu, écrit, supprimer ou être mis à jour  
 
Forcé une identification permet de bloquer les requêtes où la personne qui l’envoie n’a pas moyen d’accédée aux identifiants, une gestion des rôles est à faire, avec tout rôle inutile devant être supprimer, le principe du moindre privilège doit être utilisé, par exemple ne pas donner un droit d’écriture à sur des cours lorsque qu’il a était décider que le rôle étudiant n’a que le droit de lire c’est information. 

 
Les rôles demandant un identifiant et un mot de passe pour ce connecté, les bonnes pratiques d’utilisation de mot de passe doivent être appliqué de la complexité du mot de passe au hachage 

 

 

## UUID 

UUID est l'universel unique identifier, contrairement au UID qui utilise l’incrémentation pour se différencier, le UUID est utile pour éviter qu’un hacker puisse au hasard trouver un id lors de son Attaque. 

 

L’UUID fait 16 et se présente sous la forme de 32 de chiffres hexadécimaux, ce qui rend le nombre énorme avec un nombre de variance paressant presque infini 
	 

Si l'hackeur se retrouver en position ou il doit trouver un id pour son attaque que soit pour voler des données ou tenter une attaque LFI par l’URL, L’UUID permet de rendre cette tache presque impossible. 

 

## Encryptions 

L’encryptions est le fait de transformé les données pour qu’elle soit illisible a toute personnes qui arrive a volé les données 

Elle fonctionne avec une clé qui permet de décrypter les données quand les vérifications que la demande est légitime. 

Bien sûr cette clé demande alors de n’être pas facilement accessible, on utilise un système de gestion de clé pour qu’elle soit dans un endroit sécurisé 

 

 
## Les clés d’encryptage 

Dans un système de gestion de clé des bonnes pratiques pour l’accès doivent être utilisé, le moindre privilège, la clé doit être utilisé qu’un certain temps, le délai par défaut conseiller est 90 jours, nous allons donc utiliser ce délai pour pire2pire.com, au bout de ses 90 jours une rotation de la clé d’encryptage du site devrait être faites pour le déchiffrage des données et les encryptés de nouveau avec la nouvelle clé. 

Le cycle de vie d’une clé est : 

 

Génération : la clé est générée avec l’algorithme de chiffrement  

 

Distribution : la distribution la distribution de la clé se doit être fait de manière sécuriser via une connexion TLS 

 

Utiliser : elle est utilisée pour encrypter toutes les données précédemment décrypter par l’ancienne clé. 

 

Stockage : on le la stocke ensuite dans notre gestionnaire de clé 

 

Rotation : la clé étant à la fin de sa vie, la rotation commence, on déchiffre toutes les données pour la clé suivant 

 

Révocation : tous les droits d’utilisation de la clé sont révoqués et elle est donc inutilisable 

 

Destruction : La clé est officiellement détruite 

  

## ORM 

ORM L’Object-Relational Mapper fournit une couche orienté objet entre la base de données et le code, il permet de faire en sorte que l’on n'envoie pas la requête reçue directement dans la base de données. 
 

Il permet de configurer des points d’entrée vers la base de données, plutôt que d’envoyer directement une requête SQL.  On utilise les fonctionnalités de L’ORM pour la créer pour nous. 

 

Ainsi seulement des requêtes prédéterminées peuvent aller jusqu’à la base de données par les autres couches de l’application, empêchant ainsi des attaques SQLi. 

 

Le tout créer une couche protectrice autour de la base de données limitant les types d’accès à la base de données. 

 

## Site de sauvegarde 

Il faut avoir un site de sauvegarde sécurisé pour la base de données un site non-sécurisé peut se faire attaquer par une personne directement. 

 

L’attaquant aura alors accès à la base de données directement et seule les mesure d’authentification et d’encryptage peut protéger la base de données. 

 

 
## Copie de la base de données 

En cas de destruction du lieu physique de la base de données ou d’une attaque détruisant des données, des copies de la bade de donnée sont nécessaire. 

 

Les copies devront se trouver dans un lieu différent de la base de données principale. Pire2pire.com étant un site de e-learning la base de données et la mise fréquemment à jour de la base de données demande que celle-ci soit copié plusieurs fois par jour 

 

## Audit 

L’audit de la base de données est un journal de toutes les activités qui se passe sur la base de données. 

 

Il permet de se rendre compte de toutes les actions qui se passe dans la base, il garde toutes les actions qui se passe que c’est action soit réussite ou non ainsi que l’heure de c’est action. 

Seul permet de voir les tentatives qui se passe sur la base de données et surtout si c’est attaque ont réussi, que l’on puisse examiner l’ampleur des dégâts et ainsi pouvoir prévenir et au mieux y remédier. 



# Le Back

Le back-end d'un site web est l'endroit ou toutes les informations transit, du front qui est vu par tous les utilisateurs à la base de donnée qui a toutes les informations importantes que nous voulons protéger, cela veut dire que c'est l'endroit ou l'on va pouvoir faire le maximun de vérification.

## Vérification des entrées

Toutes demandes envoyer par un utilsateur doivent etre vérifier, par exemple dans la barre de recherche de pire2pire pour par exemple trouver une formation, on doit vérifier s'il y a pas de code Html,JS ou des requetes SQL dans la demande envoyé

Dans le cas de l'accée à une autre une page, on doit vérifier si l'utilisateur à le droit d'accés a cette page, avec l'authentification et les jetons JWT, le but étant d'éviter que une personne comme un visiteur ne puisse faire des dégàt sur le site en accédent à des endroit où il n'a pas le droit.

Si il n'a pas le droit et il arrive à trouver la page juste en cherchant le chemin, ceci est l'attaque LFI dont on avait parler plus, et la vérification des droit est le moyen de les bloquée.

On peut noté que cela inclut aussi le fait d'esseyer de trouvé des fichiers qui ne sont pas des pages qui doivent etre afficher mais juste des fichiers utiliser pour le bon déroulement de l'application, dans ce cas là nous allons bloquer tout character qui montre qu'on esseye de naviger l'arboresence de fichier.

La vérification se fait aussi par d'où viennent les requetes, pire2pire n'étant pas une API ouverte, les requette devront etre vérifier  d'ou elle vienne dans l'en-tetes HTTP et si elles viennent bien de pire2pire.com ou d'une autre source autorisé, par exemple les informations de transaction bancaire.

Les entrées sont aussi les entrée venant d'autre part que le front, que se soit la base de donnée, la récupération de la clé d'encryption ou encore une autre API.

Dans le cas de la base donnée c'est vérifier si les données reçu corespondent au format attendu de la requete envoyer avant.

Le but de toutes c'est vérification est d'avoir un nombre limité d'accée à l'api pour que l'on puisse surveiller et controler ce qui se passe.

## Traitement des données et sortie des donnée.

Toutes données qui passe dans l'API doivent etre traité après vérification pour leur sortie.

Dans le cas des requetes vers la base de donné, par exemple la création d'un nouveau compte, les données doivent etre vérifier, préparer et encrypter pour les préparer à les envoyer à la base de donnée, dans le cas de mot de mat il va falloir les haché en plus.

Ensuite tout est envoyer à l'ORM pour qu'il fasse lui meme la requete vers la base de donnée.

Le cas inverse se passe aussi pour se que l'on a recu de l'ORM.

on traite les données reçu, on les déchiffre et on les formate pour les rendre conforme au besoins pour le front, le but étant d'éviter le traitement de donné coté client.

## Mot de passe

Le mot de passe est une important pour authentification et la sécurité du site, car il étape important pour savoir le role de l'utilsateur et à qu'elle donnée il a le droit d'accées, il est donc primordiale de le protéger

### Menace

il y a plusieurs type de menace sur les mot de passes


Les attaques en ligne: le hackeur esseye de passer outre les défence du système pour avoir accès au identifiant.
Comme exemple de ce genre d'attaque on a:
- attaque par force brute: le hackeur esseye des des mot passe au hasard, potentiellement venant de dictionnaire de mot de passe avec des test automatisé

- attaque par protocole d'authentification : le hackeur intercepte des donnée d'identification par un transfert non sécuriser ou vole de token pour ce faire passer pour l'utilisateur

- le vol du moyen d’authentification: le mot de passe se fait volé, vol du mot de passe sur un bout de papier, hameconnage.

### sécurité du mot de passe

Dans le cas de pire2pire.com, les facteur d'authentification seront des facteur de connaissance.

Nous devons protéger le mot de passe de la meilleur façon, il ya plusieur mesure que l'on peut etre en place

- La complexiter du mot de passe: le mot de passe ne doit pas etre trop simple, il doit etre assez long et avoir des characters assez diversifié pour se protéger contre l'attaque de force brute, il est donc conseiller de mettre une taille minimun de 10 characters avec au moins une majuscule, une minuscule, un chiffre et un xgaracter spécial.

- le hachage: avant d'etre encrypté le mot de passe doit etre  maské avec en le hachant avec un algoryteme de hachage on y rajoute un sel pour assurer la sécuriter et protéger des attaques de rainbow table.


- Limitation du nombre de tentative: quand un nombre de 10 tentatives a était esseye, l'utilisateur sera bloqué pour une dizaine de minute avec comme seul recour le changement de mot de passe

- détection des motif simple(12345, date d'anniversaire,....)

note: on ne dira jamais lors d'un echec si l'email ou le mot de passe est faux

### le changement de mot de passe

Le changement de mot de passe est une étape nécéssaire de toute application pour éviter de perdre des utilsateur qui on perdu accé à leur compte 

le changement de mot de passe se fait en demandant l'email de l'utilisataire, on ne confirme pas si un compte correspond à l'email ou non pour éviter a un hackeur de pourvoir faire une liste de compte existant sur le site.

un token sera générer avec une durée de temps limité de temps de 15 minute, il sera envoyer dans un lien dans l'email de l'utilsateur.

l'utilisateur pourra cliqué sur le lien pour choisir un nouveau mot de passe

## Restriction des dernier mot de passe

on garde en mémoire le hache des 5 derniers mot de passe pour dire à l'utilisateur qu'ils ne sont pas réalisable, on fait cela en cas d'attaque pour éviter qu'un utilsateur réutilise en mode de passe qu'il a l'habitude qui peut etre compromie.


## Pour les roles plus important

Dans le cas des employers de pire2pire qui ont accées a des information importante, on précaunise une authenfication plus forte, avec un facteur de possesion, après l'entrée du mode de passe confirmé, un SMS qui envoie un code sera envoyé, l'employé devra entré ce code pour ce connecté 

une autre sécuriter que l'on peut mettre est une durée de vie pour un mot de passe, la personne devra changer sont mot de passe tous les mois.

## JWT

le JWT est un token générer lors de l'identification, il est envoyer coté de manière sécurisé pour l'identification, il est conserver de manière sécurisé du coté client  et il est envoyé à chaque foit qu'un appel à l'api est fait, il permet de prouvé que le client est bien lui meme et évoter des attaques CSRF.

On va mettre une durée d'expiration de 10h sur ce token, ce qu forcera les utilisateur à ce reconnecté le lendemain
af

## WAF

Le WAF est un web application firewall, il se situe entre le client et l'api protège l'api des attaques, il permet de protéger des attaques SQLi,  XXS et les attaque de type DDos et d'analysé les requette https

On peut le configurer pour qu'il laisse passer que les requete voulue et qu'il bloque les requete malveillante.




# Le Front

Le front est le coté client ce qui se passe sur la machine du client, le client peut donc avoir accée a toute information qui est envoyé,
Nous devons donc protégè toutes les info qui y arrice pour empécher qu'une autre perssone que le hacker puisse y avoir accés

## TLS

Le Transport Layer Security(TLS)  est un protocole de sécurité utilisé pour chiffrer les communications entre les applications sur Internet.

on l'utilisera avec le protocol https pour sécurissé le transfert des donné, le but étant d'empecher un potentiel hacker de capté les information, par les attack de Man-in-theMiddle

on utilisera la dernière version de TLS(1.3) pour la sécurité

On utilisera aussi les mesures de HSTS pour forcer tout accé en HTTPS et aucun en HTTP

On utilisera aussi les certificats TLS pour indiquer que le site est sur et il seront surveiller par le certificate transparacy, le but des certificats et de prouver que le site est reconnu comme sûr et ne pas avoir des problèmes avec les navigateurs et le ressancement.


## SOP

Le SOP(same-origin Policy) est une regle utilisé par défaut pour protéger où arrive les données.

Le but étant que tout transfaire vers un autre cite non autorisé ne sois pas possible et que les information sensible comme les cookie et les identifiant ne soit pas lisible par une autre origine. cette mesure peut protéger des attack XSS et CSRF.

## CORS

Le Cross-Origin Resource Sharing  on l'utilisera pour contourner le SOP quand on en aura besoin d'accedé à d'autre origin que la notre
comme par exemple pour des video youtube créer par pire2pire.com.

Le cors permet aussi d'utilisé les préflight, ou une vérification que la demande est conforme et autorisé est faite avant son execution 

## CSP

le CSP est une politique de sécurité que nous allons utilisé en complément de Cors pour controler l'activité venant d'autre origin, si Cors consiste a dire avec qui on peut communiqué, CSP est la pour dire avec qui ont ne peut pas communiqué.

Le but du CSP est de dire dans une entete ce que le navigateur doit laisser passer et bloqué comme resource venant d'une autre origine, le but étant d'empecher le site executer un script venant d'une source que l'on approuve pas, cela arrete les attaques XXS.

CSP peut aussi bloque les connexions vers d'autre domaine pas autoriser et donc éviter que l'utilsateur active une requete silencieuse à son insu.

CSP peut aussi empecher le clickjacking, le fait qu'un attaquant pllace un filtre invisible devant une page du site

La dernière fonctionnalité de CSP est qu'il peut gardr un journal des tentative de le contourner, ceux qui nous permet de voir les potentiel attack est comment les hackeur attaque le site.

Le CSP peut également bloqué les orgine d'execution du JS, en autorisant seulement dans un fichier dissocier on peut empécher des attaque XSS

Toutes c'est fonctionnalité seront utilsé pour le site pire2pire.com

## Referrer Policy

Le referrer policy est une politique de sécurité qui nous permet de controler l'URL qui passe dans l'entete qunad un utilisateur click sur un lien.

Cela nous permet de par exemple voirde quel page vient l'utilsateur, dans le cadre de pire2pire cela va etre utilisé comme mesure de protection, pire2pire étant une plate de forme de e-learning, il est possible que des lein frauduleux soit posté ou envoyé à quelqu'un pour éviter que toutes information qui se trouve dans l'URL soit envoyé on peut utilisé le Refferer policy pour indiqué quoi mettre dans l'entete HTTP envoyé, de l'URL entier à seulement le nom de domaine à rien.

Dans le cas de pire2pire on envera seulement le domaine vers d'autre origin.

## stockage de donnée coté client

il y a plusieurs moyen de stocké des donnée coté utilisateur

Le webstorage, l'indexdb et les cookies sont c'est différent moyen

Le webstorage est accesible au js et les données sont stocké en clair ce qui le rends suceptible au attaque XXS

L'indexdb stocke en clair directement les donnée de l'utilisateur, cet peut etre utilisé par des webwork ce qui le rends aussi succeptible au XXS attack.

Les cookies par contre ont des options de protection, on peut limité leur accés, les empeché d'etre transmit vers d'autre domaine et leur donnée une date d'expiration

Les cookie sont donc la solution que nous allons utilisé pour l'authentifictaion en gardant qui est la persone dedans ainsi que son JWT token, en utilisant tous les option de security et une date d'expiration.


## sécuriter des information envoyé depuis le client

L'utilisateur va envoyer des information a travers des formulaires, c'est informations devront etre vérifier pour vois si elles sont conforme à ce qu'on s'attend.

En plus de c'est vérification on doit vérifier que les donnée ne soit pas dangeureuse, des donnée envoyer peuvent avoir du code qui va s'exécuter, nous allons donc échapper les entré utilisateur pour éviter tout execution de code ainsi que ne pas utiliser de fonction qui va potentiellemen executé ce code comme eval. nous allons jamais inséré du contenu dans le DOM sans traitement et vérification avant.

L'envoie d'une requette peut etre une requete détourné par un site piégé envoyer a l'utilisateur pour éviter cela nous allos utiliser des token CRSF, le token sera normalement généré quand l'utilisateur arrive sur la page, il sera conservé dans la session et mit en valeur caché dans le formulaire, on pourra les comparer lors de l'envoi du formulaire pour voir si c'est vraiment une requete venant dans utilisateur utilsant la méthode normal ou une attque CSRF pour mannipulé les crédential de l'utilisateur.

## Appel au Api

Tou appel vers une api sera fait avect fetch XMLhttprequest étant plus sensible au attaque XSS.

Fetch a un meilleur support avec le CSP et le CORS, mais aaussi la possibilité d'intéragir avec les cookie de crédentiel

Nous utiliserons alors la méthode fetch pour le site

## Iframe

Dans le site, l'incrustation de vidéo youtube peut etre utilisé pour un autre support au étudiant.

Nous pouvons isoler c'est video youtube pour que le domaine youtube est zero accés à ce qui se passe, cela permetra d'empecher le 2eme domaine que l'on fait apparaitre sur la page de, soummetre des formulair, executer du code accéder au info protéger par le SOP, accéder au DOM.

Ainsi on peut utiliser les avantage de foncion d'autre site sans mettre en danger la sécurité de pire2pire.com

## Protection contre les injections de codes


### Strict mode

Toutes utilisation des Javascript sera fera avec l'activation du strict mode de JS, le strict force des meilleur pratique de codage, avec ce mode des simples erreur lors de l'excution du code bloqueront son avancement.

L'ajout de ce mode peut bloqué le code injecter lors  d'une XSS attack

### web worker 

On peut utiliser les web worker pour l'éxucution du code javascript dans un environnement séparee, sans qu'il ne puisse  affecter le DOM directement, cela nous permet de faire de l'execution de de code JS avec plus de sécuriter.

Nous devons quand meme faire des vérifications sur ce qui rentre dans le web worker dans le web worker, ainsi ce qui sort avant de l'utilisé pour dans le DOM.

Le CSP doit etre utilisé avec le web worker pour limiter les sources externes.

### Template string

Lorsque l'on recoit des informations on peut utilisé les fonction d'échappement des templates string  pour remplacé les characters qui indique des fonctionnalités de code, pour Le navigateur comprendra qu'il devra affiché les characters initial lors de l'affichage mais ils ne seront pas reconnu comme du code dans lors de l'execution. 


# Conclusion

Nous allons mettre en place toute c'est mesure dans le bute de respecté la réglementation, mais aussi éviter toutes forme de dégat sur à pire2pire et donnée la meilleur experience utilisateur à tous les personnes qui i vont inérargire avec le site, que se soit des visieut, des étudiant ou bien encore des employés de pire2pires.