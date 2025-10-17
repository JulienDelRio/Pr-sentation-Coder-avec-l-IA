OBJECTIF
Tu crées un mini-site statique qui reproduit ma présentation Google Slides avec Reveal.js.

SOURCE
- URL du deck : https://docs.google.com/presentation/d/1fC02bUsKOIoJnm9Wnc3p6vN61zQkAXlghy3I5JHV0sY/edit?slide=id.p#slide=id.p
- Important : si tu ne peux pas accéder au contenu, ne devine RIEN. Génére la structure complète des slides avec des TODO clairement marqués à remplir manuellement.

CONTRAINTES GÉNÉRALES
- Code clair, modulaire, prêt à déployer sur GitHub Pages/Netlify.
- Pas de backend. 100% statique.
- Accessibilité : contrastes suffisants, navigation clavier, tailles lisibles.
- Licence MIT. README complet.
- Langue de l’UI et des contenus : français.

STACK
- Reveal.js (CDN ou npm), plugins officiels : Markdown, Notes, Search, Zoom, Highlight.
- Vite pour le dev/build.
- Typo sans-serif (Inter ou système).
- Thème sombre custom léger (overrides CSS).

ARBORESCENCE ATTENDUE
/reveal-deck/
  index.html
  slides.md                # contenu Reveal en Markdown
  /assets/                 # (placeholders si aucune image fournie)
    favicon.ico
    logo.png
  /styles/
    theme.css              # overrides (couleurs, tailles, spacing)
  /scripts/
    export-pdf.mjs         # script d’export PDF (Chrome headless)
  package.json
  vite.config.ts
  README.md
  .gitignore
  LICENSE

FONCTIONNALITÉS REVEAL À ACTIVER
- hash: true
- transition: 'slide'
- slideNumber: 'c/t'
- pdfSeparateFragments: true
- plugins: [Markdown, Notes, Search, Zoom, Highlight]

CONTENU & STRUCTURE DES SLIDES
- Crée 24 slides (si l’accès au deck est impossible, crée 24 sections vides cohérentes : titre, programme, chapitres, limites, Q/A, merci).
- Utilise `---` pour changer de slide, `<!-- .element: class="fragment" -->` pour révélation progressive.
- Ajoute dans `slides.md` un squelette prêt à remplir :
  - Slide 1 : Titre « Coder avec l’IA : de l’assistant au co-pilote »
  - Slide 2 : « Qui suis-je ? » (bullets placeholders)
  - Slides chapitres (programme, niveaux/typologies d’IA pour le code, démos, limites, questions, etc.)
  - Sur chaque slide, si le contenu n’est pas disponible : `<!-- TODO: coller contenu depuis Google Slides -->`
- Ajoute un exemple de fragments sur 1 slide (3 bullets).

INDEX.HTML (EXIGENCES)
- Charger Reveal + plugins.
- Charger `slides.md` (plugin Markdown).
- Config Reveal.initialize conforme aux fonctionnalités listées.
- Lier `styles/theme.css`.

THEME.CSS (EXIGENCES)
- Palette sombre (fond #111–#151), texte principal #EEE, liens accentués.
- Titres plus grands, interlignage confortable.
- Style impression : conserver fonds en mode print-pdf.

SCRIPTS NPM
- "dev": vite
- "build": vite build
- "preview": vite preview
- "export:pdf": "node scripts/export-pdf.mjs"
- "lint": "echo \"(optionnel)\""

EXPORT PDF (export-pdf.mjs)
- Utilise Chrome/Chromium headless pour ouvrir `index.html?print-pdf` et générer `deck.pdf`.
- Documentation dans README sur l’option alternative : impression via navigateur.

CI/CD (OPTIONNEL)
- Fournis un workflow GitHub Actions minimal pour GitHub Pages : build + deploy (branche `gh-pages`).

README.md (CONTENU MINIMUM)
- Objectif du projet, stack, prérequis.
- Démarrage : `npm i`, `npm run dev`.
- Build/preview.
- Export PDF (deux méthodes).
- Déploiement (Pages/Netlify).
- Comment éditer `slides.md` (fragments, code highlight).
- Accessibilité & bonnes pratiques.

CRITÈRES D’ACCEPTATION
- Le site démarre avec `npm run dev`, navigable au clavier, numérotation des slides, fragments fonctionnels.
- `slides.md` contient 24 slides (ou un nombre identique à la source si tu as pu parser).
- `?print-pdf` fonctionne et `npm run export:pdf` produit un PDF lisible.
- Thème sombre lisible + overrides CSS appliqués.
- README explicite et suffisant pour un contributeur tiers.

PLAN D’ACTION (CE QUE TU FAIS MAINTENANT)
1) Initialise le projet Vite + structure de dossiers.
2) Ajoute Reveal.js + plugins (import/cdn), crée `index.html` minimal.
3) Crée `slides.md` avec structure des 24 slides + TODO si contenu non accessible.
4) Écris `styles/theme.css` (sombre + responsive + print).
5) Implémente `export-pdf.mjs`.
6) Rédige `README.md` complet + LICENSE MIT.
7) Ajoute scripts npm.
8) Lance `npm run dev` et vérifie manuellement le rendu local (décris ce que tu as vérifié).
9) Fournis en sortie : l’arborescence finale, un court changelog des étapes, et les commandes pour builder/déployer.

CONTRAINTE IMPORTANTE
- N’invente pas de contenu. Si tu n’as pas pu charger le deck, laisse des placeholders clairs. Fournis un guide rapide dans le README pour copier/coller le contenu depuis Google Slides vers `slides.md`.

PRODUIT ATTENDU
- Un projet complet prêt à cloner et lancer.
- Un message final avec : 
  - l’arborescence,
  - les fichiers clés (extraits), 
  - et les commandes d’usage.
