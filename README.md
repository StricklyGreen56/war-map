# Season 1 War Map · Server #267

Interactive Palmon Survival Season 1 conquest map. Anyone with the link can view it. Leads who know the passcode can add plans and change tile owners, and everyone sees changes live.

Live site (after setup): https://stricklygreen56.github.io/war-map/

## How it works

- **GitHub Pages** hosts the page (`index.html`, `config.js`, `map-capture.jpg`).
- **Firebase Firestore** stores plans (`pins`), owner changes (`owners`), the change log (`log`), approved editors (`editors`) and pending edit requests (`requests`).
- **Accounts:** anyone can view without signing in. To edit, a person signs in with Google or email, taps **Request edit access**, and an admin approves them on the map. `firestore.rules` only accepts edits from approved editors and admins.
- **Admins** are listed in the `admins` collection, which can only be changed in the Firebase console.

## Setup

GitHub Pages and the Firebase project are already set up. To switch on accounts:

### 1. Turn on Google and email sign-in

1. Firebase console → **Security** → **Authentication** → **Sign-in method** tab.
2. **Add new provider** → **Google** → turn it on, pick your email as the support email → **Save**.
3. **Add new provider** → **Email/Password** → turn on the first switch only → **Save**.
4. (Optional) Turn **Anonymous** off. It isn't used anymore.

### 2. Publish the new rules

Firestore → **Rules** tab → replace everything with the contents of `firestore.rules` → **Publish**.

### 3. Make yourself the admin

1. Open the map, tap **Sign in**, and sign in with Google (or create an email account).
2. The Account card shows **Your user ID**. Copy it.
3. Firestore → **Data** → **Start collection** → Collection ID `admins` → Next.
4. Document ID: paste your user ID. Add a field `name` (string) with your name → **Save**.
5. Reload the map. You'll see **Edit requests** and **Editors** cards.

To add another admin, repeat step 3 with their user ID.

### 4. Clean up the old passcode (optional)

Firestore → Data → delete the `admin` collection and the `editors` documents created by the passcode version.

## Everyday use

- **Viewing:** share the link in Discord. No account is needed.
- **Getting edit access:** sign in → **Request edit access**. An admin taps **Approve** under Edit requests.
- **Removing someone:** under Editors, tap **Remove**. They can still view.
- **Undoing a mistake:** the change log shows who changed what and when. Use **Back to video** on a tile to undo an owner change, or ✕ to remove a plan.
- **Resetting all owner changes:** in Firestore, delete the `owners` collection.
