# Présentation Coder avec l'IA

## Contexte

Cette présentation a été donnée pour la première fois à la factory Tech de Digital 113 le 17/10/2025.

## Le support

Le support de la présentation est à retrouver ici : https://docs.google.com/presentation/d/1fC02bUsKOIoJnm9Wnc3p6vN61zQkAXlghy3I5JHV0sY/edit?usp=sharing

## Les prompts

### 1 - la vérification de données

#### Le but

Demander à l'IA de générer un code de vérification de données utile pour certains process d'entreprises.

#### Le prompt prépartif

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


#### Le prompt

Rédige un prompt concis (15 lignes maximum) décrivant la tâche suivante :

- Créer deux scripts qui filtrent des adresses e-mail valides selon la RFC 5322.  
- Un script **JavaScript (Node.js)** qui lit un fichier CSV d’entrée et génère un fichier de sortie avec le même contenu + une colonne `valid` (true/false), enregistré avec le suffixe `_checked`.  
- Un script **Excel VBA** qui lit les adresses dans la **colonne A**, ignore la première ligne d’en-tête, et écrit le résultat (`True`/`False`) dans la **colonne B** du même fichier.  
- Les deux doivent utiliser une **RegEx robuste et commentée**, proche de la RFC 5322, et expliquer brièvement ses segments clés.  
- Mentionner les règles de validation (pas de `..`, pas de point initial/final, domaine correct, TLD ≥ 2, punycode autorisé).  
- Inclure quelques exemples valides/invalides, les limites (pas de vérif DNS/MX, pas d’Unicode local-part), et des pistes d’amélioration (normalisation punycode, test DNS).  

Le résultat attendu est un prompt compact, en Markdown facile à copier coller.

### ? - Créer un workflow n8n

#### Le but

Lui demander de générer le blueprint en JSON d'un workflow.

Exemple : workflow “Vérification de mot de passe secret”

Illustrer les concepts fondamentaux de n8n :

* **Saisie utilisateur** via un formulaire,
* **Comparaison de valeurs**,
* **Branchement conditionnel (IF)**,
* **Réponse HTML dynamique**,
* **Gestion d’erreur HTTP**.

Ce workflow montre comment n8n peut servir de passerelle logique entre une entrée utilisateur et une réponse web formatée.

**Déroulement général**

1. **Un utilisateur remplit un formulaire web** en entrant un mot de passe.
2. **n8n compare** la valeur saisie à un mot de passe de référence stocké localement.
3. Si la valeur correspond :
   → une page HTML de succès est renvoyée.
4. Sinon :
   → une erreur HTTP 401 est générée, avec un message explicite.


#### Le prompt

Crée le blueprint en json d'un **workflow n8n (v1.114+)** composé de 5 nœuds :

1. **Form node** en POST recevant un champ `password`.
2. **Set** contenant une variable `expectedPassword` = `"OpenSesame42"`.
3. **IF** comparant `{{$json["body"]["password"]}}` (depuis le webhook) avec `{{$json["expectedPassword"]}}` (du Set).
4. **Form Ending** sur la branche *true* :
   * Code 200
   * Type `text/html`
   * Corps : “✅ Accès autorisé ! Bienvenue dans la zone secrète.”
5. **Error** sur la branche *false* :
   * Code 401
   * Type `text/html`
   * Corps : “❌ Accès refusé. Mot de passe incorrect.”

Inclure les connexions entre nœuds, les expressions correctes, des commentaires d'expliction et un nom clair pour chaque nœud.
Résultat attendu : un JSON n8n complet prêt à importer.


### ? - Analyser du code

#### Le but

#### Le prompt


### ? - Créer une petite application web

#### Le but

#### Le prompt
