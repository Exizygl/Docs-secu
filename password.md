# Etape
- Enregistrement
- Phase d’identification
- Authentification
- Accès aux ressources

# Menace

- Attaquant en ligne(bloqué après plusieur tentative)
- Attaquant hors ligne, accésempreintes de mots de passe ou une clé publique(hachage et des protocoles d’authentification sécurisés.)

## type d'attaque
- Attaques par force brute
- Attaques sur le protocole d’authentification par homme du milieu, attaque par rejeu,
- Vol du moyen d'authentification( vol de carte à puce,, ou l’ingénierie sociale)

## attaques sur les facteurs de connaissance

- Attaque par recherche exhaustive(tentative random ou mode passe commun)
- Attaque par dictionnaire( test d'une librairie de mot de passe/variation inclu)
- Attaque par tables pré-calculées (Rainbow tables, L'attaquant utilise des empreintes cryptographiques pré-calculées de mots de passe pour accélérer la recherche et comparer ces empreintes avec celles volées afin de trouver le mot de passe.)
- Attaque par ingénierie sociale (l’hameçonnage ou l'usurpation d'identité.)

- defence
    - Recherche exhaustive(Limite temporelle entre chaque essai et fonctions de hachage itératives)
    - Recherche par dictionnaire(Mots de passe robustes et aléatoires, coffre-fort de mots de passe)
    - Tables pré-calculées (Rainbow tables, Utilisation de sel aléatoire long lors du hachage des mots de passe)
    - Hameçonnage / Ingénierie sociale (Authentification multifacteur (MFA))

## Menaces et attaques sur les facteurs de possession
- Vol
- perte
- duplication
- falsification
- compromission de l'équipement

## Menaces et attaques sur les facteurs inhérents (biométrie)
- Leurrer le mécanisme biométrique

# limitation des mot de passes
- Mémorisation des mots de passe
    - mots de passe simples et facilement mémorisable
    - meme mote de passe réuse

- Mots de passe robustes
    - longs et complexes, intégrant des majuscules, minuscules, chiffres et caractères spéciaux.
    - peuvent etre compliqué a mémo.

- Gestion des mots de passe
    - Coffre-fort de mots de passe
    - reutilisation de mot de passe

- Vulnérabilités liées à la gestion des mots de passe
    - la réutilsation peut etre dangereux en cas de fuite de donnée.

- recommentdation
    - coffre ou multi facteur identification

# L'authentification multifacteur (AMF)
- Facteur de connaissance
- Facteur de possession 
- Facteur inhérent 
- multifacteur =/= double facteur

# Authentification forte vs. Authentification multifacteur
- Authentification multifacteur (AMF)
    - plusieur type de facteur
- Autentification forte
    - mot de passe compliqué
    - Puce
    - doit résister au attack
    - OTP

# Choix
    - Analyse de Risque
    - Pas de faux sentiments de sécurité
    - exp user à prendre en compte(pas trop compliquer pour éviter qu'il note le mot de passe)
    - prendre en compte la gestion de multifacteur
    - contexte, en cas d'urgence un PIN est préféravle
    - outil externe d'authentification augmente la surface d'attaque.

# Cycle de vie
- création et renew
    - création des facteur d'authentification dans un environement simple
    - élement aléatoire de haute qualité, conforme au norme en vigueur
    - facteur d'authen envoir par canl sécu
    - process de renewal
    
- utilisation
    - Éviter la réutilisation de mots de passe faibles.
    - Mettre en place des mécanismes de verrouillage après plusieurs tentatives échouées.
    - Surveiller les tentatives d'accès inhabituelles ou suspectes
    
- révocation facteur
    - révoc quand plus utilisé
    - gestion éfficace de la révocation

# Facteur d'utilisation
- SMS
    - envoie de code peut etre intercepté
    - ne pas envoyer les facteur d'authentification par SMS

- conserver l'historique d'identification

- limitation tentavive sur une periode

- canal sécurisé d'envoie
    - TLS ou IPsec

- limiter la durée de vie d'une session

- protection des donnée identification stockée
    - hash

- information de L'echec d'authentification
    - zero info sur l'ehec au user

- sensibilisation des users

- révocation
    - mise en place d'un processus de révoc
    - moyen au user de demandé d'etre revoc
    - délai de révocation rapide en fonction du risque

# facteur de connaissance

- Politique de sécurité des mots de passe
    - Catégorie de mots de passe (mémorisés ou non)
    - Longueur des mots de passe
    - Règles de complexité (types de caractères autorisés)
    - Délai d'expiration des mots de passe
    - Limitation des essais d'authentification
    - Méthodes de conservation des mots de passe
    - Méthode de recouvrement d'accès en cas de perte ou vol
    - Coffre-fort de mots de passe

- Longueur des mot de passes
    - longueur minimal impossé
    - laisser la possibilité de mot de passe long

- Règle de conplexité 