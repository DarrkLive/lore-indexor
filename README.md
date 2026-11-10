Here is the updated, comprehensive **README** for your repository, reflecting the new v4.9 architecture where credentials are safely isolated in `config.js` for secure GitHub publishing and seamless mobile testing.

---

# LORE INDEXOR — Master Archive & Editor (v4.9)

## Mobile Testing & Deployment README

Welcome to **Lore Indexor**! This tool is designed as a fast, private, cloud-synced lore management system optimized for both desktop and mobile devices via Google Drive integration.

---

## 🚀 Key Features Built-In

1. **Persistent Cloud Sync (`localStorage`):**
* Authenticates securely with Google Drive and caches your session token locally. Once logged in, refreshes or revisits are **promptless and automatic**.


2. **Secure Config Architecture (`config.js`):**
* Credentials (Client ID and Drive ID) are cleanly separated into a local `config.js` file, keeping your repository safe and clean when hosted publicly on GitHub.


3. **Auto-Hiding Sidebar:**
* Automatically collapses once your master file is successfully fetched, maximizing your mobile reading and editing real estate.


4. **Peta & Standard Tag Management:**
* **Peta Tags** sit at the top of entry cards (`+ Peta` button), while **Standard Tags** sit below titles (`+ Tag` button). Both feature smart in-app dropdown suggestions populated from your archive.


5. **Editor-Only Tag Controls:**
* Tag addition and deletion (`×`) buttons only appear when you are actively in **Editor View**.


6. **Dynamic Category Auto-Coloring:**
* Writing any custom category in brackets (e.g., `[FACTIONS]: ...`) instantly assigns a unique theme color.



---

## 📂 Repository File Structure

When setting up your GitHub repository, your project structure should look like this:

```text
/lore-indexor
├── index.html       # The main application frontend & logic
└── config.js        # Your private configuration (keep local/gitignored)

```

### `config.js` Template

Create this file locally in your project folder (do not push it to public GitHub repositories):

```javascript
const CONFIG = {
  CLIENT_ID: 'YOUR_GOOGLE_CLIENT_ID',
  DRIVE_FILE_ID: 'YOUR_GOOGLE_DRIVE_FILE_ID'
};

```
