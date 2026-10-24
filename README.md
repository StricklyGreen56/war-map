# Season 1 War Map · Server #267

Interactive Palmon Survival Season 1 conquest map. Anyone with the link can view it. Leads who know the passcode can add plans and change tile owners, and everyone sees changes live.

Live site (after setup): https://stricklygreen56.github.io/war-map/

## How it works

- **GitHub Pages** hosts the page (`index.html`, `config.js`, `map-capture.jpg`).
- **Firebase Firestore** stores plans (`pins`), owner changes (`owners`) and the change log (`log`).
- **Editing** uses a passcode stored in Firestore at `admin/secret`. The site can never read it. When a lead enters it, Firebase checks it, and `firestore.rules` only accepts edits from people who entered the current passcode.

## One-time setup

### 1. Turn on GitHub Pages

1. Open the repo on GitHub → **Settings** → **Pages**.
2. Under **Build and deployment**, set Source to **Deploy from a branch**, Branch to **main**, folder **/ (root)**, then **Save**.
3. After a minute the site is live at the link above.

### 2. Create the Firebase project

1. Go to https://console.firebase.google.com and sign in with a Google account.
2. Click **Create a project** (or **Add project**), name it `war-map`, and turn Google Analytics **off**. Click **Create project**.

### 3. Create the database

1. In the left menu: **Build** → **Firestore Database** → **Create database**.
2. Pick a location near you (for example `nam5 (United States)`), then choose **Start in production mode** → **Create**.
3. Open the **Rules** tab, delete everything there, paste the full contents of `firestore.rules` from this repo, and click **Publish**.

### 4. Set the passcode

1. In Firestore, open the **Data** tab → **Start collection**.
2. Collection ID: `admin` → **Next**.
3. Document ID: `secret`. Add one field: name `key`, type **string**, value = your passcode. Click **Save**.

### 5. Turn on sign-in for leads

1. Left menu: **Build** → **Authentication** → **Get started**.
2. **Sign-in method** tab → **Anonymous** → turn it on → **Save**.
3. **Settings** tab → **Authorized domains** → **Add domain** → `stricklygreen56.github.io` → **Add**.

### 6. Connect the site

1. Click the gear icon → **Project settings** → **General** → scroll to **Your apps** → click the web icon (`</>`).
2. Nickname `war-map`, leave Firebase Hosting **unchecked**, click **Register app**.
3. Copy the `firebaseConfig = { ... }` block it shows. Either send it to Claude, or paste the values into `config.js` on GitHub (open the file → pencil icon → edit → **Commit changes**).

These config values are meant to be public. The passcode is what protects editing.

## Everyday use

- **Viewing:** share the link in Discord. No account is needed.
- **Editing:** tap **Edit**, enter your name and the passcode. Each device remembers it until you tap **Stop editing on this device**.
- **Changing the passcode:** in Firestore, open `admin` → `secret` and change `key`. Everyone is locked out of editing until they enter the new passcode.
- **Undoing a mistake:** the change log on the page shows who changed what and when. Use **Back to video** on a tile to undo an owner change, or ✕ to remove a plan.
- **Resetting all owner changes:** in Firestore, delete the `owners` collection.
