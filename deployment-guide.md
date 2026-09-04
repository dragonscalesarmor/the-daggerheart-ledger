# Deploying the Daggerheart Ledger

This guide walks through putting the Ledger online for good: a free shared database (Firebase), and free hosting with a permanent link (GitHub Pages). No credit card, no server, no ongoing cost at this scale.

Total time: about 15–20 minutes, once.

---

## Part 1 — Create the Firebase project

1. Go to **console.firebase.google.com** and sign in with any Google account.
2. Click **Add project** (or **Create a project**).
3. Give it a name — e.g. `daggerheart-ledger`. Click **Continue**.
4. You'll be asked about Google Analytics. **Turn it off** — it's not needed here, and skipping it makes setup one step shorter.
5. Click **Create project**, wait for it to finish, then **Continue**.

You now have a free Firebase project.

---

## Part 2 — Turn on Firestore (the database)

1. In the left sidebar, click **Databases & Storage**, then choose **Firestore** from the "NoSQL" section of the menu that appears. (Not "Realtime Database" — that's a different, older Firebase product.)
2. Click **Create database**.
3. It'll ask to start in **Production mode** or **Test mode** — pick either one, it won't matter, because Part 3 replaces the rules anyway.
4. Choose a location. Pick one physically close to most of your players (e.g. an `eur3` / Europe option if your group is mostly in Europe). **This can't be changed later**, but for a small shared app the difference is milliseconds either way — don't overthink it.
5. Click **Enable**.

---

## Part 3 — Open up the security rules

By default, Firestore either blocks everything or only allows access for 30 days ("test mode"). Since this app has no login system — that's the whole point — it needs permanently open rules instead.

1. Still in **Firestore Database**, click the **Rules** tab at the top.
2. Delete everything in the box and paste this instead:

   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /{document=**} {
         allow read, write: if true;
       }
     }
   }
   ```

3. Click **Publish**.

**What this means, plainly:** anyone who has your app's link can read and write to this database. There's no login checking who's allowed in — same trade-off as everything else in this ledger (the DM/Player split, the join codes). It's built for a trusted group, not for the public internet at large. Don't put anything truly sensitive in it.

---

## Part 4 — Register a web app and get your config

This is the piece that connects your HTML file to your specific Firebase project.

1. Go back to the **Project Overview** page (the little house icon, top-left).
2. Under "Get started by adding Firebase to your app," click the **`</>`** (Web) icon.
3. Give it a nickname, e.g. `Ledger web`.
4. **Leave "Also set up Firebase Hosting" unchecked** — we're using GitHub Pages instead.
5. Click **Register app**.
6. You'll see a code block containing something like this:

   ```js
   const firebaseConfig = {
     apiKey: "AIzaSy...",
     authDomain: "daggerheart-ledger-xxxxx.firebaseapp.com",
     projectId: "daggerheart-ledger-xxxxx",
     storageBucket: "daggerheart-ledger-xxxxx.appspot.com",
     messagingSenderId: "123456789",
     appId: "1:123456789:web:abcdef123456",
   };
   ```

   **Copy that whole object.** You'll paste it into the app file next.

   This isn't a secret to protect — it's meant to be public. It ends up visible in your page's source the moment it's live anyway. The Firestore rules from Part 3 are what actually govern access, not this config.

7. Click **Continue to console**. You're done with Firebase for now.

---

## Part 5 — Paste your config into the app file

1. Open `index.html` (the app file) in any plain text editor.
2. Near the top, find this block:

   ```js
   const firebaseConfig = {
     apiKey: "PASTE_YOUR_API_KEY_HERE",
     authDomain: "PASTE_YOUR_PROJECT_ID.firebaseapp.com",
     projectId: "PASTE_YOUR_PROJECT_ID",
     storageBucket: "PASTE_YOUR_PROJECT_ID.appspot.com",
     messagingSenderId: "PASTE_YOUR_SENDER_ID",
     appId: "PASTE_YOUR_APP_ID",
   };
   ```

3. Delete it and paste in the real one you copied from Firebase in Part 4.
4. Save the file. Keep the filename exactly `index.html`.

That's the only edit this file ever needs from you.

---

## Part 6 — Put it on GitHub Pages

1. Go to **github.com** and log in.
2. Click the **+** in the top-right → **New repository**.
3. Name it something like `daggerheart-ledger`.
4. Set it to **Public** (required for free GitHub Pages hosting on a personal account).
5. Don't add a README or anything else — leave it empty. Click **Create repository**.
6. On the new repo's page, click **uploading an existing file** (or **Add file → Upload files**).
7. Drag in your edited `index.html`.
8. Scroll down, click **Commit changes**.
9. Go to the repo's **Settings** tab → **Pages** (left sidebar, under "Code and automation").
10. Under **Build and deployment → Source**, choose **Deploy from a branch**.
11. Under **Branch**, choose **main** and **/ (root)**, then **Save**.
12. Wait about a minute, then refresh the page. GitHub will show a green box with your live URL — something like:

    ```
    https://yourusername.github.io/daggerheart-ledger/
    ```

That's the link. Anyone can open it, anywhere, no account, no login.

---

## Part 7 — Test it

1. Open the URL from another device if you can (phone, different browser).
2. Pick a role, create a test character.
3. Open the same URL on a second device/browser and confirm the character shows up for the DM (or reappears if you re-enter the same account code as a Player).
4. If nothing shows up or you see an error banner: double-check Part 3 (rules) and Part 5 (config) — those two are where almost every setup issue comes from.

---

## Making changes later

Whenever you get an updated file (from me, or someone else editing it):

1. Go to your repo on GitHub, open `index.html`.
2. Click the pencil (✎) icon to edit.
3. Select all the existing content, delete it, paste in the new version.
4. Scroll down, click **Commit changes** directly to `main`.
5. Give it about a minute — GitHub Pages redeploys automatically. No separate "publish" step.

Nothing about Parts 1–4 (the Firebase project itself) needs to be touched again for ordinary app updates — only the file content changes.
