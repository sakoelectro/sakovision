# Lecteur M3U — Version Serveur (PHP + SQLite)

## Contenu
- `index.html` : Frontend (lecteur + login).
- `channels.json` : Playlist intégrée (générée depuis votre M3U).
- `api/` : API PHP (auth JWT-like par token, mots de passe hashés, rôles, expiration).
- `data/` : Dossier pour la base SQLite (`app.db`) (créée automatiquement à la première requête).

## Déploiement
1. **Hébergeur/Serveur** : Apache + PHP ≥ 8.0 avec SQLite activé.
2. **Upload** : Déposez tout le dossier `m3u_web_secure` à la racine de votre hébergement.
3. **Réécriture d'URL** : Assurez-vous que `AllowOverride All` est actif. Le fichier `api/.htaccess` route `/api/*` vers `api/index.php`.
4. **Accès** : Ouvrez `index.html` dans le navigateur (ex : `https://votre-domaine/index.html`).

## Comptes initiaux
- Admin : **admin** / **admin123** (créé automatiquement, expiration +365 jours).

## API (résumé)
- `POST /api/login` → { username, password } → { token, user }
- `POST /api/logout` (Bearer token)
- `GET /api/me` (Bearer token)
- `GET /api/users` (admin)
- `POST /api/users` (admin) → ajouter
- `PUT /api/users/{id}` (admin) → modifier
- `DELETE /api/users/{id}` (admin) → supprimer

## Mise à jour de la playlist
Remplacez `channels.json` par une version régénérée (ou demandez-moi d'intégrer un nouveau `.m3u`).

## Remarques
- Certains flux peuvent ne pas jouer en raison de **CORS** ou de restrictions d'origine par les hébergeurs. Les flux `.m3u8` sont pris en charge via **Hls.js**.
- Pour HTTPS obligatoire / tokens persistants, envisagez une **expiration plus courte** et l'activation du **HTTPS** sur votre domaine.
