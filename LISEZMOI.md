# EPR - Caisse commune (Firebase + PWA)

## Contenu
- `index.html` : l'application (formulaire, espace garant, gestion du groupe, connexion)
- `manifest.webmanifest`, `sw.js`, `icons/` : installation sur téléphone (PWA)
- `firestore.rules` : règles de sécurité de la base

## 1. Firebase (gratuit)
1. https://console.firebase.google.com > **Ajouter un projet** (nom : epr-caisse).
2. **Authentication** > Méthode de connexion : activer **E-mail/Mot de passe** et **Google**.
3. **Firestore Database** > Créer une base (mode production).
4. Onglet **Règles** de Firestore : coller le contenu de `firestore.rules` > Publier.
5. **Paramètres du projet** > Vos applications > icône web `</>` : copiez le bloc `firebaseConfig`.
6. Dans `index.html`, remplacez la ligne `const firebaseConfig = {...}` par le vôtre.

## 2. Premier administrateur
1. Connectez-vous une fois à l'application (cela crée votre compte).
2. Console Firebase > Authentication > Utilisateurs : copiez votre **UID**.
3. Firestore > Démarrer une collection `admins` > ID du document = votre UID (un champ quelconque, ex. `role: "admin"`).
4. Répétez pour chaque administrateur. Rechargez l'application : l'onglet « Gestion du groupe » apparaît.

## 3. GitHub + déploiement
1. Créez un dépôt GitHub, puis ouvrez-le dans **Codespaces** (bouton Code > Codespaces).
2. Déposez ces fichiers à la racine du dépôt (glisser-déposer dans l'explorateur).
3. Commit et push (onglet Contrôle de code source).
4. https://vercel.com ou https://netlify.com > importer le dépôt (aucun réglage, site statique).
5. Firebase > Authentication > Paramètres > **Domaines autorisés** : ajoutez votre domaine Vercel/Netlify (sinon la connexion Google échoue).

À chaque modification : commit + push, le site se met à jour tout seul. Les données Firebase ne sont pas touchées.

## 4. Installer l'application
Ouvrir le site sur le téléphone > menu du navigateur > « Ajouter à l'écran d'accueil ».

## Logo
Remplacez `icons/icon-192.png` et `icons/icon-512.png` par le logo EPR (mêmes noms, mêmes tailles).

## Limites actuelles
- Pas de notification email/SMS au garant : il voit la demande dans l'onglet « À signer ». Les notifications demandent des Cloud Functions (formule Blaze de Firebase) : à ajouter dans une étape suivante.
- Les signatures sont des images stockées avec la demande : c'est un accord interne au groupe, pas une signature électronique à valeur légale.
