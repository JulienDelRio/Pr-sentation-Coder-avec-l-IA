On va créer ensemble une **application web de messagerie interne** simple mais complète, exécutable facilement via :

```bash
docker compose up
# ou
npm run dev
```

---

### 🧱 **Stack technique**

* **Backend** : Node.js + Express + SQLite + Prisma + JWT
* **Frontend** : React (ou Vanilla JS, au choix)
* **Sécurité / Auth** : Cookies httpOnly, bcrypt (ou argon2)
* **Logs / Docs / Tests** : Pino, Swagger, Jest (ou équivalent)
* **Infra** : Dockerfile + docker-compose + migrations auto
* **Objectif** : code clair, commenté, modulaire, et facile à exécuter.

---

## 🚀 Étapes de réalisation

### 0️⃣ Préparation

* Définir la stack, le style d’authentification, la stratégie de pagination et de notification (polling ou SSE).
* Créer un fichier `ARCHITECTURE.md` décrivant les flux (auth, messages), schémas DB, rôles, et contraintes.

---

### 1️⃣ Structure du projet

* Initialiser le dépôt Git et NPM.
* Créer la structure :

  ```
  /backend (src, prisma, tests)
  /frontend (src)
  /infra (Dockerfile(s), docker-compose.yml)
  ```
* Ajouter ESLint, Prettier, scripts `npm run dev`, `npm run build`.
* Objectif : `npm run dev` lance un serveur “Hello World”.

---

### 2️⃣ Backend minimal (Express + Prisma + SQLite)

* Installer : `express`, `cors`, `cookie-parser`, `pino`, `zod`, `prisma`.
* Initialiser Prisma (`npx prisma init`) et définir `provider = sqlite`.
* Créer endpoint `/health` qui renvoie `{ status: "ok" }`.

---

### 3️⃣ Modèle de données Prisma (v1)

* Tables :

  * `User`: id, name, email, passwordHash, role (`user`/`admin`), bio, avatar.
  * `Message`: id, text, authorId, createdAt, updatedAt.
  * `ActivityLog`: id, type, userId, createdAt, meta JSON.
  * `RefreshToken`: id, userId, token, expiresAt.
* Commandes :

  ```bash
  npx prisma migrate dev -n init
  npx prisma studio
  ```

---

### 4️⃣ Variables d’environnement + Seed initial

* `.env.example` doit contenir :

  ```
  DATABASE_URL="file:./dev.db"
  JWT_SECRET="changeme"
  ADMIN_EMAIL="admin@example.com"
  ADMIN_PASSWORD="password123"
  ADMIN_NAME="Super Admin"
  FRONTEND_URL="http://localhost:5173"
  PORT=3000
  ```
* Script `prisma/seed.ts` : crée l’admin + un message de bienvenue.
* Commande : `npm run prisma:seed`

---

### 5️⃣ Authentification JWT + Refresh Token

* Endpoints :

  * `POST /auth/signup`
  * `POST /auth/login`
  * `POST /auth/logout`
  * `POST /auth/refresh`
  * `GET /auth/me`
* Tokens :

  * `accessToken` court (15 min)
  * `refreshToken` long (7–30 j)
* Utiliser cookies `httpOnly`, `SameSite=Lax`, `Secure` en prod.
* Middleware : `requireAuth`, `requireAdmin`.

---

### 6️⃣ Réinitialisation du mot de passe

* Deux modes :

  1. Par email : `/auth/request-reset` → lien ou token.
  2. Par admin : `/admin/reset-password/:id`.
* Validation via Zod, tokens temporaires JWT.

---

### 7️⃣ Gestion utilisateur + Profil

* Endpoints :

  * `GET /me/profile`
  * `PUT /me/profile`
  * `GET /admin/users`
  * `PATCH /admin/users/:id` (changer rôle)
  * `DELETE /admin/users/:id`
* L’admin peut : supprimer un utilisateur, changer un rôle, réinitialiser un mot de passe.
* Ajout de `ActivityLog` automatique sur les actions clés.

---

### 8️⃣ Messagerie (auth requise)

* Endpoints :

  * `GET /messages?cursor=...` (pagination ou lazy load)
  * `POST /messages`
  * `PATCH /messages/:id` (si auteur & < 2 min)
  * `DELETE /messages/:id` (ou admin)
* Format message :

  * Nom de l’expéditeur
  * Horodatage (ex. “il y a 3 min”)
* Journaliser création/suppression de messages.

---

### 9️⃣ Notifications + “Instantané”

* Deux options :

  * **Polling** toutes les 3–5 s.
  * **Server-Sent Events (SSE)** sur `/events/messages`.
* Frontend :

  * Badge visuel à la réception d’un nouveau message.
  * Scroll automatique vers le bas après envoi ou réception.

---

### 🔟 Frontend – Auth & Routing

* Stack : React + Vite.
* Pages :

  * Login / Signup
  * Inbox (chat)
  * Profil
  * Admin Dashboard
* State global (user + token), garde de route selon rôle.
* `fetch(..., { credentials: 'include' })` pour cookies JWT.

---

### 11️⃣ Frontend – UI Messagerie & Admin

* Chat :

  * Messages courants à droite, autres à gauche.
  * Édition possible pendant 2 minutes.
  * Suppression avec **confirmation visuelle**.
  * Pagination/lazy loading au scroll.
* Admin :

  * Liste utilisateurs
  * Changement de rôle
  * Suppression utilisateur ou message
  * Consultation du journal d’activité

---

### 12️⃣ Observabilité & Documentation API

* Ajouter :

  * Logs structurés (`pino` ou `winston`)
  * Endpoint `/health` enrichi (uptime, DB status)
  * Mini Swagger (`swagger-ui-express`)
* Convention d’erreur : `{ error, code, message }`
* Page `/docs` (protégée ou non indexée).

---

### 13️⃣ Tests & Sécurité

* Tests unitaires sur :

  * Auth (hash/verify, refresh)
  * Messagerie (édition ≤ 2 min)
  * Rôles et permissions
* Tests d’API (auth flow, CRUD message)
* Sécurité :

  * `helmet`, `cors` strict
  * validation Zod partout
  * cookies sécurisés
  * rate-limit sur login

---

### 14️⃣ Docker & Exécution finale

* **Dockerfiles** :

  * Backend (multi-stage)
  * Frontend (build + serveur statique)
* **docker-compose.yml** :

  * Services : backend, frontend, volume SQLite, healthchecks
  * Lancement auto des migrations et du seed
* Commandes :

  ```bash
  docker compose up --build
  ```

  ou

  ```bash
  npm install && npm run dev
  ```
* Tout doit fonctionner sans configuration manuelle.

---

## 🧾 Livrables attendus

* Code source complet.
* `README.md` détaillé :

  * Installation et lancement
  * Variables d’environnement
  * Commandes Prisma (`migrate`, `seed`)
  * Comptes de test (admin / user)
  * Liste des endpoints REST
  * Architecture globale
* `.env.example` complet.

---

## ✅ Critères de réussite

* `docker compose up` démarre toute l’application (backend, frontend, DB, migrations auto, seed admin).
* Auth JWT + refresh token fonctionnels.
* Réinitialisation de mot de passe (email et admin).
* Messagerie instantanée fluide avec notifications visuelles.
* Logs, Swagger, `/health` et tests disponibles.
* Rôles et journal d’activité opérationnels.
* Code clair, commenté, modulaire, et exécutable sans intervention manuelle.
