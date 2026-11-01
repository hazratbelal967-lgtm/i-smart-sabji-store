# FreshMart — Vegetable Shop Management Website

A mobile-friendly vegetable catalogue and shopkeeper inventory dashboard.

## Features
- Public customer catalogue with live stock and per-kg prices
- Search and category filter
- 500 g / 750 g / custom weight price calculator
- Shopkeeper email/password login
- Separate delivery batches with arrival date and estimated shelf life
- Low-freshness warning based on the estimated date
- Reduce stock after a sale
- Mark a batch spoiled so it disappears from the public catalogue
- Firebase Firestore shared database

## Project files
- `index.html` — website structure
- `style.css` — responsive design
- `app.js` — app logic and Firebase connection
- `firebase-config.js` — Firebase web app settings
- `firestore.rules` — database access rules

## 1. Create Firebase project
1. Open https://console.firebase.google.com/
2. Create a project, for example `freshmart-shop`.
3. In Project settings > General > Your apps, add a Web app.
4. Copy the web configuration into `firebase-config.js`.
5. In Build > Authentication > Sign-in method, enable **Email/Password**.
6. In Authentication > Users, add the shopkeeper's email and a strong password.
7. In Build > Firestore Database, create a database.

## 2. Set the shopkeeper as the only editor
1. In Firebase Authentication > Users, copy the shopkeeper user's **UID**.
2. Open `firestore.rules`.
3. Replace `PASTE_OWNER_UID_HERE` with that exact UID.
4. Publish these rules in Firestore > Rules.

Important: the public website can read the stock. Only the matching signed-in UID can create, update or delete stock. Do not use test-mode rules in production.

## 3. Run locally
Because the app uses JavaScript modules, open it through a local web server rather than double-clicking `index.html`.
- VS Code: install the Live Server extension, right-click `index.html`, choose **Open with Live Server**.
- Or use Python from this folder: `python -m http.server 8000`, then visit `http://localhost:8000`.

## 4. Publish on GitHub Pages
1. Create a GitHub repository, e.g. `freshmart-vegetable-store`.
2. Upload all six project files to the repository root.
3. Open repository Settings > Pages.
4. Under Build and deployment, select **Deploy from a branch**.
5. Select `main` and `/ (root)`, then Save.
6. Wait for the Pages deployment. Your website URL will look like `https://YOUR-USERNAME.github.io/freshmart-vegetable-store/`.

## How stock works
Every delivery creates a separate batch. Example: 10 kg tomatoes received on Nov 1 and another 15 kg received on Nov 3 are stored separately. The customer catalogue combines active batches by vegetable name and shows the latest batch's listed price.

Shelf-life days are only an estimate. Storage conditions vary, so the shopkeeper must physically inspect vegetables and mark spoiled batches manually. An estimated date is not a food-safety guarantee.

## Important production notes
- This starter project stores quantity and price in Firestore, but does not yet include online payments, customer orders, delivery scheduling, or sales invoices.
- The Firebase web config is intended to be public; security comes from Authentication and Firestore Rules. Never upload a Firebase service-account key or private credentials.
- For a real shop, add a custom domain, privacy notice, backups, and test the security rules before relying on the app.
