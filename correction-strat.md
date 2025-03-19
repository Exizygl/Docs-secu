# Introduction

## Contexte

The goal of this documentation is to present the security measures we will take to ensure the security of pire2pire.com. Today, the dangers of cyber threats are omnipresent, and we must ensure that security measures are taken at every step of the project, starting with this document, through the conception of the site and its functionalities, to the development and release.

The goal of this document is to be understandable for everyone, from beginners to experts. This means it will be presented in a pedagogical way. We will focus on the different dangers, present and explain potential solutions to those dangers.

Pire2pire.com is an e-learning website where people will be able to learn different courses. There will be visitors, students, and coaches.

## Impact

A poorly secured website can cause a lot of harm. Here is a list of dangers that may include:

- **Sensitive information theft:** Malicious actors may gain access to sensitive data, such as financial information, a corporation’s confidential information, or an individual’s personal information. The danger is that the attacker may use this stolen data for identity theft, blackmail, or fraud.
  
- **Damage to brand:** A website can be defaced, which means inappropriate content can be inserted, political messages can be inserted, advertisements for products can be inserted, or a warning that the website has been hacked. All of these will damage the trust of current and potential customers. In case of a successful attack, it is strongly advised to inform the customer as quickly as possible so that customers can protect themselves and be more careful against potential identity theft or fraud.

- **Criminal activity:** Gaining customer information or taking control of the website can lead to criminal activities like spreading malware, posting illegal content, conducting phishing, or using the platform to attack other systems or people who have access to it.

- **Banning or suspension:** Content inserted on the website may be suspicious, either spam, malware, or links to distrustful websites. These can be flagged as dangerous or suspicious by search engines. These flags can lead the hacked website to be flagged as suspicious, which will impact search engine results (up to the removal of the website from results) and affect traffic to the website. In the worst-case scenario, the host of the site may shut down the website.

- **Harm to the user experience:** One of the side effects of being hacked may be activities or code that slow the response time to requests, which will ruin the user experience. Adding to that problem, there is the possibility of spam and malware also affecting the user experience negatively, which may lead users to leave the website.

- **Financial losses:** Access to financial data may result in financial loss, especially if the hacker gains enough access to perform transactions. The loss of customers may also impact revenue. There is also the potential for compensation to customers and the cost of dealing with and repairing the security breach.

## Organization of the documentation

This document will present the different types of dangers that may occur during the lifetime of the site. We will then explain how these problems will be stopped. Finally, we will detail all the protections in each section of the documentation, from the database to the front.

# RGPD

Le Règlement Général sur la Protection des Données (RGPD) est une réglementation de l'Union européenne que le site devra suivre et appliquer. Il se concentre sur le traitement des données personnelles, la collecte, le stockage, le partage et donne plus de contrôle aux utilisateurs.

Nous devrons donc :

- **Consentement** : Demander le consentement clair et explicite de l'utilisateur avant toute collecte de données.
- **Droits** : L'utilisateur a le droit d'accéder aux informations récoltées, de les rectifier, le droit à la portabilité, le droit d'opposition au traitement des données ainsi que le droit à l'oubli.
- **Responsabilité** : Nous avons l'obligation de protéger ces données, ce dossier étant une explication des mesures techniques que nous mettrons en place.
- **Notification** : Toute violation de données doit être signalée aux autorités dans les 72 heures suivant la détection.

En cas de non-conformité avec la réglementation, l'entreprise peut recevoir une amende allant jusqu'à **20 millions d'euros ou 4 % du chiffre d'affaires mondial**.

---

# Type d'attaques rencontrées

Ici, nous allons présenter les différents types d’attaques que ce guide a pour but de prévenir :

- **XSS** : L'attaque *Cross-Site Scripting* consiste à injecter du code (JavaScript ou HTML) dans une page web pour obtenir un comportement visé lorsque ce code sera exécuté. Le but est de récupérer des informations sur les utilisateurs d'un site.
- **CSRF** : L'attaque *Cross-Site Request Forgery* consiste à tromper un utilisateur pour le forcer à effectuer une action voulue sur un site donné depuis un site tiers. Par exemple, envoyer une requête cachée à `pire2pire.com` en interagissant sur un site créé par l'attaquant.
- **SSRF** : L'attaque *Server-Side Request Forgery* consiste à demander au serveur d'effectuer des requêtes vers une destination choisie par l'attaquant, en profitant éventuellement des privilèges du serveur.
- **SQLi** : L'attaque *SQL injection* consiste à envoyer une requête non prévue par les fonctions du site ou les droits d'utilisateur pour affecter la base de données. Cela donne la possibilité à l'attaquant de faire ce qu'il veut.
- **LFI/RFI** : L'attaque *Local/Remote File Inclusion* consiste à trouver un moyen d'accéder à un fichier local ou distant sur le site normalement pas accessible pour une personne n'ayant pas les droits.
- **DDoS** : L'attaque *Distributed Denial of Service* consiste à envoyer un grand nombre de demandes automatisées au serveur pour le surcharger et perturber l'utilisation des autres utilisateurs, en ralentissant voire en rendant le serveur incapable de répondre aux demandes.
- **XXE** : L'attaque *XML External Entity* consiste à injecter du XML malveillant pour exécuter ce code et obtenir des accès normalement impossibles.


# Pratique de développement  

Pour protéger de ces attaques, certaines mesures vont être respectées à travers le développement du projet.  

## Unités distinctes  
Chaque couche de l’application sera séparée (Front, Base de données, API). Cette séparation nous permettra de bien définir les interactions entre chacune d’entre elles. Ces interactions étant bien définies, nous allons pouvoir développer des mécanismes de défense et de vérification pour chacune d’entre elles.  

## Moindre privilège  
Le moindre privilège consiste à donner le moins de possibilités d’action possible à chaque rôle des utilisateurs. Les visiteurs du site ne doivent pas avoir accès à des fonctions dédiées aux étudiants, coachs ou administrateurs.  

## Réduction de la surface d’attaque  
Plus nous ajoutons de composants au site et plus nous agrandissons l’exposition aux réseaux de notre site. Plus il y a d’opportunités de se faire attaquer. Nous n’allons pas rajouter des composants inutilisés ou non sécurisés, ainsi que retirer ceux qui sont seulement utiles au cours de la phase de développement lorsque nous passerons à la phase de déploiement. De même pour l’exposition réseau : plus on en a, plus il y a de vulnérabilités. Nous devons limiter les accès réseau.  

## Sécurisation des échanges de données  
Tout échange de données doit être sécurisé pour ne pas être intercepté pendant son transfert. Nous allons utiliser des protocoles comme le protocole HTTPS pour la protection.  

## Conformité du contenu  
Nous allons assurer la conformité des données pour faire en sorte que le site apparaisse dans le navigateur des utilisateurs tel qu'il a été conçu, afin d'assurer l’expérience promise.  

## Journalisation  
La journalisation consiste à enregistrer les interactions sur chaque couche du site dans des journaux d’événements pour garder une trace de tout ce qui s’y passe ainsi que du moment où ces événements se sont produits. Le but étant que, en cas de problème, d'attaque ou de tentative d’attaque, on puisse retracer l’attaque pour corriger de potentielles failles ainsi qu'avoir une idée de l’ampleur des dégâts.  


# La Base de données  

La base de données est au cœur de la sécurité du site, c’est l’endroit où toutes les informations importantes se trouvent, et les protections de la base de données sont extrêmement importantes au cas où les protections des couches rencontrées avant ont été contournées ou si l’attaquant arrive à attaquer directement la base de données.  

## Authentification  

Utiliser un système d’authentification est important pour protéger une base de données. Ce système permet de créer des rôles qui gèrent les droits sur la base de données, cela permet de gérer ce qui peut être vu, écrit, supprimé ou mis à jour.  

Forcer une identification permet de bloquer les requêtes où la personne qui l’envoie n’a pas moyen d’accéder aux identifiants. Une gestion des rôles est à faire, avec tout rôle inutile devant être supprimé. Le principe du moindre privilège doit être utilisé, par exemple ne pas donner un droit d’écriture sur des cours lorsqu’il a été décidé que le rôle étudiant n’a que le droit de lire ces informations.  

Les rôles demandant un identifiant et un mot de passe pour se connecter, les bonnes pratiques d’utilisation de mot de passe doivent être appliquées, de la complexité du mot de passe au hachage.  

## UUID  

UUID est l’Universel Unique Identifier. Contrairement au UID qui utilise l’incrémentation pour se différencier, le UUID est utile pour éviter qu’un hacker puisse, au hasard, trouver un ID lors de son attaque.  

L’UUID se présente sous la forme de 36 chiffres hexadécimaux, ce qui rend le nombre énorme avec un nombre de variantes paraissant presque infini.  

Si l’attaquant se retrouve en position où il doit trouver un ID pour son attaque, que ce soit pour voler des données ou tenter une attaque LFI par l’URL, l’UUID permet de rendre cette tâche presque impossible.  

## Chiffrement 

Le chiffrement est le fait de transformer les données pour qu’elles soient illisibles à toute personne qui arrive à voler les données.  

Elle fonctionne avec une clé qui permet de décrypter les données quand les vérifications montrent que la demande est légitime.  

Bien sûr, cette clé demande alors de ne pas être facilement accessible. On utilise un système de gestion de clés pour qu’elle soit dans un endroit sécurisé.  

## Les clés de chiffrement

Dans un système de gestion de clés, des bonnes pratiques pour l’accès doivent être utilisées. Le moindre privilège, la clé doit être utilisée pendant un certain temps, un délai de 90 jours sera appliqué. Nous allons donc utiliser ce délai pour pire2pire.com. Au bout de ces 90 jours, une rotation de la clé de chiffrement du site devrait être faite pour le déchiffrage des données et les chiffrer de nouveau avec la nouvelle clé.  

### Le cycle de vie d’une clé :  

- **Génération** : la clé est générée avec l’algorithme de chiffrement.  
- **Distribution** : la distribution de la clé doit être faite de manière sécurisée via une connexion TLS.  
- **Utilisation** : elle est utilisée pour encrypter toutes les données précédemment décryptées par l’ancienne clé.  
- **Stockage** : on la stocke ensuite dans notre gestionnaire de clés.  
- **Rotation** : la clé étant à la fin de sa vie, la rotation commence, on déchiffre toutes les données pour la clé suivante.  
- **Révocation** : tous les droits d’utilisation de la clé sont révoqués et elle devient inutilisable.  
- **Destruction** : la clé est officiellement détruite.  

## ORM  

ORM (*Object-Relational Mapper*) fournit une couche orientée objet entre la base de données et le code. Il permet de faire en sorte que l’on n’envoie pas la requête reçue directement dans la base de données.  

Il permet de configurer des points d’entrée vers la base de données plutôt que d’envoyer directement une requête SQL. On utilise les fonctionnalités de l’ORM pour la créer pour nous.  

Ainsi, seules des requêtes prédéterminées peuvent aller jusqu’à la base de données par les autres couches de l’application, empêchant ainsi des attaques SQLi.  

Le tout crée une couche protectrice autour de la base de données, limitant les types d’accès à la base de données.  

## Site de sauvegarde  

Il faut avoir un site de sauvegarde sécurisé pour la base de données. Un site non sécurisé peut se faire attaquer par une personne directement.  

L’attaquant aura alors accès à la base de données directement et seules les mesures d’authentification et d’encryptage peuvent protéger la base de données.  

## Copie de la base de données  

En cas de destruction du lieu physique de la base de données ou d’une attaque détruisant des données, des copies de la base de données sont nécessaires.  

Les copies devront se trouver dans un lieu différent de la base de données principale. Pire2pire.com étant un site de e-learning, la base de données et la mise à jour fréquente de la base de données demandent que celle-ci soit copiée plusieurs fois par jour.  

## Audit  

L’audit de la base de données est un journal de toutes les activités qui se passent sur la base de données.  

Il permet de se rendre compte de toutes les actions qui se passent dans la base. Il garde toutes les actions qui se passent, que ces actions soient réussies ou non, ainsi que l’heure de ces actions.  

Cela permet de voir les tentatives qui se passent sur la base de données et surtout si ces attaques ont réussi, afin que l’on puisse examiner l’ampleur des dégâts et ainsi pouvoir prévenir et au mieux y remédier.  
