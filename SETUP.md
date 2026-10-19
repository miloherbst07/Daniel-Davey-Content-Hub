# VERUS Content Hub: setup

About 15 minutes, all free. Until step 2 is done the site runs in **demo mode** (saves only in your own browser), so you can try everything first.

## 1. Create the Firebase project
1. Go to https://console.firebase.google.com and click **Create a project** (e.g. `verus-content-hub`). Analytics isn't needed.
2. Stay on the free **Spark** plan. Images are compressed and stored inside the database, so you don't need Firebase Storage or a paid plan.

## 2. Connect the site
1. In the project overview, click the **web icon `</>`** to add a web app. Any nickname. Skip Firebase Hosting.
2. Copy the `firebaseConfig` values it shows into **`firebase-config.js`**, replacing `null`:
   ```js
   window.FIREBASE_CONFIG = { apiKey: "...", authDomain: "...", projectId: "...", storageBucket: "...", messagingSenderId: "...", appId: "..." };
   ```
   These values aren't secret. Security comes from the rules in step 4.

## 3. Turn on sign-in
1. **Build → Authentication → Get started.**
2. Under **Sign-in method**, enable **Google** (and **Email/Password** if Daniel would rather use a password).
3. **Settings → Authorised domains → Add domain:** `miloherbst07.github.io`
4. For email/password users: **Users → Add user** with Daniel's email and a password.

## 4. Create the database and lock it to you two
1. **Build → Firestore Database → Create database.** Pick a European location (e.g. `eur3`) and start in **production mode**.
2. Open the **Rules** tab, paste the contents of **`firestore.rules`**, replace Daniel's placeholder email with his real one (lowercase), and click **Publish**.
   Anyone not on that list can't read or write anything.

## 5. Publish on GitHub Pages
1. Create a new repository, e.g. `verus-content-hub` (it can be private on paid GitHub plans; public is fine because the data lives in Firebase, not the repo).
2. Upload **all** the files, keeping the `icons` folder.
3. **Settings → Pages → Build and deployment:** Source = *Deploy from a branch*, Branch = `main` / root. Save.
4. After a minute it's live at `https://miloherbst07.github.io/verus-content-hub/`.

## 6. First sign-in
- The first time you sign in, the hub sets itself up with the three funnels, their content types, the 45 starter ideas, starter plan notes, the housekeeping checklist and all 118 videos from `library-seed.json` (with thumbnails and links). Leave the page open for a minute while the videos load. Edit or delete any of it.
- Go to **Settings → Team** and make sure each name has the exact email that person signs in with. That's how reflections and comments get labelled Milo or Daniel.

## 7. Put it on your phones
- **iPhone:** open the site in Safari → Share → **Add to Home Screen**.
- **Android:** Chrome menu → **Install app**.

## Good to know
- **Free limits:** Firestore's free tier (1 GB stored, 50k reads/day) is far more than two people need. Each image is shrunk to under ~850 KB, with a small thumbnail for lists.
- **Offline:** changes made offline sync when you're back online.
- **Backups:** Settings → Backup & export gives CSVs and a full JSON backup. Worth doing monthly.
- **Updating the site:** replace `index.html` in the repo. Your data isn't affected.
- **Demo data:** anything you add in demo mode stays in that browser and doesn't move to Firebase.
