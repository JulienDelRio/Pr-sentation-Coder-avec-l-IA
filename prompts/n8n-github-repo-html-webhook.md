Crée un **workflow n8n (v1.114+)** nommé **“GitHub Repo Info with webhook”**.

Le workflow doit :
- Démarrer par un noeud **Incoming Webhook** qui présente une page HTML avec un formulaire acceptant deux paramètres : `owner` et `repo` obligatoires
- Qaudn le formulaire est saisit il renvoie vers l'url du webhook wait suivant
- Appeler l’API publique de GitHub : `https://api.github.com/repos/{owner}/{repo}`.
- Si le dépôt est introuvable ou privé → **erreur 404** (“Dépôt introuvable ou privé”).
- Sinon, récupérer aussi les **langages** via `/languages`.
- Construire une **page HTML** affichant : nom du dépôt, description, visibilité, licence, stars, forks, watchers, taille, date de mise à jour et liste des langages.
- Ajouter des badges visuels (★, forks, issues, etc.).
- Retourner la page HTML via **Response to webhook**.
- Si une étape échoue → message d’erreur clair en HTML.
- Code clair et commenté dans le nœud Code.

Le résultat doit être un **workflow JSON complet**, prêt à importer dans n8n.
