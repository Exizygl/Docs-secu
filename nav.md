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

