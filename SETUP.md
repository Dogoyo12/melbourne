# Melbourne '26: getting it on your phones

About 15 minutes, one time only. No coding needed.

## 1. Create the shared database (Firebase, free)
1. Go to https://console.firebase.google.com and sign in with any Google account.
2. **Create a project.** Name it something like `melbourne-trip`. You can turn Google Analytics off.
3. In the left menu, go to **Build → Firestore Database → Create database**. Pick location **australia-southeast1 (Sydney)** and start in **production mode**.
4. Open the **Rules** tab, replace everything with the rules below, and click **Publish**:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /trips/{tripId}/plan/{itemId} {
      allow read, write: if request.time < timestamp.date(2027, 3, 1);
    }
  }
}
```
(This lets the app read and write your trip until March 2027, then locks it. It covers the plan, notes, edits and the Bug Petting Championship scores, which are all stored in the same place.)

5. Click the gear icon, then **Project settings**. Under **Your apps**, click the **</>** (Web) icon. Give it a nickname and click **Register app**. You don't need Firebase Hosting.
6. You'll see a `firebaseConfig = { apiKey: ..., ... }` block. Copy those values into **firebase-config.js**, replacing the `PASTE...` placeholders. You can also send the block to Claude and it will do this for you.

## 2. Put it online (GitHub Pages, free)
1. Sign in at https://github.com (or create a free account).
2. Click **+ → New repository**. Name it, for example, `melbourne`, set it to **Public**, and click **Create repository**.
3. Click **uploading an existing file** and drag in **everything in this folder**: `index.html`, `firebase-config.js`, `sw.js`, `manifest.webmanifest`, `bg.jpg` and the `icons` folder. Then click **Commit changes**.
4. Go to **Settings → Pages**. Under "Branch", choose **main** and **/(root)**, then click **Save**.
5. After about a minute, your app is live at `https://YOUR-USERNAME.github.io/melbourne/`.

## 3. Install on both iPhones
1. Open the link in **Safari** (it has to be Safari).
2. Tap **Share**, then **Add to Home Screen**, then **Add**.
3. Open it from the home screen. It runs full screen with no browser bars. Enter your name on first launch. It needs to start with **Fred** or **Ash** so bug pets count for the right person.

The dot at the top right shows **Synced** when both phones are connected. If you're offline, changes save on your phone and sync automatically when you're back online.

**Heads-up:** a public repo means anyone with the link can see the files, including the photos and the letter. The link isn't listed anywhere, so only share it with Ash.
