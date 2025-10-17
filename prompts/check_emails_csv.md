# Le prompt prépartif

Génère un **fichier CSV** nommé `emails_test.csv` contenant une seule colonne intitulée `email`.
Le fichier doit comporter **50 lignes** d’adresses e-mail simulées :

* **10 adresses valides** conformes à la **RFC 5322** (ex. `prenom.nom@example.com`)
* **40 adresses invalides**, présentant **des erreurs variées**, par exemple :

  * caractères interdits (`space@domain.com`, `john@@mail.com`)
  * absence d’arobase ou de domaine (`jane.mail.com`, `@example.com`)
  * points mal placés (`.john@domain.com`, `john..doe@domain.com`)
  * domaines incorrects (`user@localhost`, `user@domain.c`)
  * TLD inexistants (`user@domain.123`, `user@domain.xyzxyz`)
  * adresses incomplètes (`user@`, `user@domain.`)
  * espaces ou guillemets mal échappés (`"user name"@domain.com`)

Le résultat attendu doit être du **texte CSV brut**, sans ligne d’en-tête supplémentaire, prêt à être enregistré.
Assure-toi que les erreurs soient **diversifiées et réalistes**.


# Le prompt

- Créer deux scripts qui filtrent des adresses e-mail valides selon la RFC 5322.  
- Un script **JavaScript (Node.js)** qui lit un fichier CSV d’entrée et génère un fichier de sortie avec le même contenu + une colonne `valid` (true/false), enregistré avec le suffixe `_checked`.  
- Un script **Excel VBA** qui lit les adresses dans la **colonne A**, ignore la première ligne d’en-tête, et écrit le résultat (`True`/`False`) dans la **colonne B** du même fichier.  
- Les deux doivent utiliser une **RegEx robuste et commentée**, proche de la RFC 5322, et expliquer brièvement ses segments clés.  
- Mentionner les règles de validation (pas de `..`, pas de point initial/final, domaine correct, TLD ≥ 2, punycode autorisé).  
- Inclure quelques exemples valides/invalides, les limites (pas de vérif DNS/MX, pas d’Unicode local-part), et des pistes d’amélioration (normalisation punycode, test DNS).  

Le résultat attendu est un prompt compact, en Markdown facile à copier coller.
