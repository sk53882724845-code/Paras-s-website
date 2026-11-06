# Paras's Website — GitHub Pages + Firebase

This project uses GitHub Pages for the public website and Firebase for secure owner login, video storage, and video details.

## Files
- `index.html` — website
- `firestore.rules` — public video listing; only the owner can add/edit/delete records
- `storage.rules` — public video playback; only the owner can upload files

## 1. Create Firebase project
1. Open https://console.firebase.google.com/ and create a project.
2. Add a Web App in Project settings and copy its Firebase config.
3. In Authentication > Sign-in method, enable **Email/Password**.
4. In Authentication > Users, add the owner's email and a strong password. Do not create a public sign-up page.
5. In Firestore Database, create a database.
6. In Storage, get started and create the default bucket.

## 2. Add Firebase config
Open `index.html` and replace the placeholder values in `firebaseConfig` with your Web App config:
- `apiKey`
- `authDomain`
- `projectId`
- `storageBucket`
- `appId`

Firebase web config is designed to be included in a website. The actual access control is enforced by Firebase Security Rules, not by hiding this config.

## 3. Set owner UID in both rules files
In Firebase Authentication > Users, open the owner's account and copy its **UID**.
Replace `PASTE_OWNER_AUTH_UID` in both `firestore.rules` and `storage.rules` with that exact UID.
Publish each rules file in the matching Firebase console section:
- Firestore Database > Rules
- Storage > Rules

Do not leave the placeholder UID in the published rules.

## 4. Publish on GitHub Pages
1. Create a GitHub repository named `paras-website` (or use an existing repository).
2. Upload `index.html` to the repository root. Keep the two rules files for reference; Firebase rules are published in Firebase Console.
3. In GitHub: Settings > Pages > Deploy from a branch > `main` > `/(root)` > Save.
4. Wait for GitHub Pages to publish, then open the provided Pages URL.

## How it works
- Everyone can watch published videos.
- Only the Firebase owner account can sign in.
- Only that owner's UID can upload video files and create video records.
- Title, description, and video file are required.
- Uploads are limited to 500 MB per video in this starter version.

## Important
GitHub Pages is static hosting; it cannot securely process uploads by itself. Firebase provides the backend. Never put a service-account key or admin secret in `index.html`.
