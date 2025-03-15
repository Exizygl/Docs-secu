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