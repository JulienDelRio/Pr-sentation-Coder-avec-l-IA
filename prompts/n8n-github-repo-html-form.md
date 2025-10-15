Crée un **workflow n8n (v1.114+)** nommé **“GitHub Repo Info”**.

Le workflow doit :
- Démarrer par un noeud **Form** acceptant deux paramètres : `owner` et `repo` obligatoires
- Appeler l’API publique de GitHub : `https://api.github.com/repos/{owner}/{repo}`.
- Si le dépôt est introuvable ou privé → **erreur 404** (“Dépôt introuvable ou privé”).
- Sinon, récupérer aussi les **langages** via `/languages`.
- Construire une **page HTML** affichant : nom du dépôt, description, visibilité, licence, stars, forks, watchers, taille, date de mise à jour et liste des langages.
- Ajouter des badges visuels (★, forks, issues, etc.).
- Retourner la page HTML via **End Form**.
- Si une étape échoue → message d’erreur clair en HTML.
- Code clair et commenté dans le nœud Code.

Le résultat doit être un **workflow JSON complet**, prêt à importer dans n8n.
