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

Le Règlement Général sur la Protection des Données (RGPD) est une réglementation de l'Union européenne que le site devra suivre et appliquer. Il se concentre sur le traitement des données personnelles et donne plus de contrôle aux utilisateurs.

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
