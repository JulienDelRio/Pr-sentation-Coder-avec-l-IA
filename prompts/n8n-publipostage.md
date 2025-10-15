Crée un **workflow n8n** (compatible v1.114 ou supérieure) qui lit un **fichier CSV uploadé par l’utilisateur** contenant les colonnes `nom` et `email`.
Le workflow doit :

1. Commencer par un **Form Trigger** permettant de téléverser le fichier.
2. Lire le contenu du CSV et convertir chaque ligne en objet JSON.
3. Pour chaque utilisateur, générer un **message personnalisé** du type :

   > Bonjour {{nom}}, bienvenue dans notre communauté !
4. Envoyer ce message par **email** (utilise le nœud “Email Send”).
5. En cas d’erreur d’envoi, consigner l’échec dans un nœud **IF + Log**.
6. Retourner à la fin un **résumé HTML** listant :

   * les emails envoyés avec succès,
   * les erreurs éventuelles.
7. Fournis le **schéma complet JSON du workflow n8n**, prêt à importer.
8. Indique ensuite la **structure attendue du CSV d’entrée** et un exemple de test.
