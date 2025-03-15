# keyword too look for
- XXE injection
- SSRF(Server-side Request forgery)
- SQLi
- LFI/RFI
- XXE

# SSRF
- cause
    - mauvaise gestion des URL
    - importation d'image depuis URL
    - webhooks
    - callback URL
    - communication service interne

- protection
    - si whitelist
        - vérification des entrées
            - vérification des adresses IP avec biblio fiable
            - vérification des noms de domaine sans effectuer de résolution DNS externe.
            - Regex
        - Securité réseau
            - pare-feu
            - segmentation du réseau
    
    - si pas de whitelist
        - liste de blocage : Interdire les IP privées et internes.
        - Accepter uniquement HTTP/HTTPS.
        - tokens d’authentification : Le service externe doit générer un token que l’application devra inclure dans la requête pour prouver sa légitimité.

# SQLi

- SQLi se produit lorsque des entrées non sécurisées sont concaténées dans des requêtes SQL dynamiques

- eviter
    - requete avec concaténation de chaines
    - empecher insertion malveillantes

- protéger
    - requêtes préparées
        - Séparer SQL et donné envoyer
        - Parameterized Queries
    - procédures stockées sécurisées 
    - valeur prédéfie si posible
    - éciter échapement(marche pas toujours)
    - least privilège
    - creation de vue SQL

# LFI/RFI
- LFI
    - inclure un ficher local dans une requete en manipulant l'entrée utilisateur
    - protection
        - verification des données utilisateurs
        - liste blanche des fichiers accessibles
- RFI
    - inclure un fichier venant d'un autre serveur dans l'url pour l executer en chargant la page
    - protection
        - verifire l'url avant execution(adresse IP)
        - allow_url_include = off en php same for allow_url_fopen
        - whiteliste???
