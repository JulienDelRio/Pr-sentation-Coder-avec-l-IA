Crée une **application web de messagerie interne** simple mais complète, exécutable facilement (`docker compose up` ou `npm run dev`).
Utilise **Node.js + Express + SQLite + Prisma + JWT** pour le backend, et un **frontend léger (React ou Vanilla JS)**.

**Fonctionnalités principales :**

1. **Cycle utilisateur**

   * Sign up, login, logout.
   * Deux rôles : `user` (par défaut) et `admin`.
   * Création automatique d’un **compte admin** via variables d’environnement (`ADMIN_EMAIL`, `ADMIN_PASSWORD`, `ADMIN_NAME`, `JWT_SECRET`, `DATABASE_URL`).
   * Auth sécurisée par **JWT** (en cookie httpOnly).
   * **Expiration du JWT** + **refresh token automatique**.
   * **Réinitialisation de mot de passe** via email ou **token généré par l’admin**.

2. **Gestion utilisateur**

   * Page de **profil** (nom complet, avatar, bio courte).
   * Possibilité de **modifier son profil** (nom, mot de passe, avatar).
   * **Hashage fort des mots de passe** (bcrypt ou argon2).
   * **Historique d’activité** visible uniquement par les admins.
   * **Admins** peuvent : supprimer un utilisateur, changer son rôle, réinitialiser un mot de passe.

3. **Messagerie (auth requise)**

   * Lire la **liste des messages** (avec pagination ou lazy loading).
   * Écrire un message.
   * **Éditer son message** dans un délai de 2 minutes.
   * Supprimer **ses propres messages** (avec **confirmation visuelle**).
   * Affichage style “messagerie instantanée” :

     * messages de l’utilisateur courant à droite,
     * messages des autres à gauche.
   * Chaque message affiche :

     * le **nom de l’expéditeur**,
     * l’**horodatage** (“il y a 3 min” ou format lisible).
   * **Notification visuelle** (badge ou surbrillance) à la réception de nouveaux messages.
   * **Scroll automatique** vers le dernier message après envoi ou réception.

4. **Admin / Modération**

   * Supprimer un utilisateur.
   * Changer les droits (user ↔ admin).
   * Supprimer **n’importe quel message**.
   * Consulter l’**historique d’activité** (journal minimal).
   * Journalise automatiquement : création/suppression de message, changements de rôle, connexions.

5. **Technique / DevOps**

   * Variables d’environnement documentées dans `.env.example`.
   * **Migration automatique** via `Prisma migrate`.
   * **Script de seed initial** :

     * création de l’admin,
     * ajout d’un **message de bienvenue** signé par l’admin.
   * Endpoints REST documentés (mini OpenAPI/Swagger).
   * Endpoint `/health` pour monitoring.
   * Logs structurés avec Winston ou Pino.
   * Code clair, commenté et prêt à tester (tests unitaires basiques).

6. **Exécution**

   * Tout doit fonctionner via :

     ```bash
     docker compose up
     ```

     (avec Dockerfile, docker-compose.yml, seed et migrations automatiques).
   * Alternative :

     ```bash
     npm install && npm run dev
     ```

7. **Livrables**

   * Code source complet.
   * README détaillant :

     * variables d’environnement,
     * installation,
     * commandes de migration/seed,
     * comptes de test (admin / user),
     * structure des endpoints.
