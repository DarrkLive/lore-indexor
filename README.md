# Lore Indexor 📚

Lore Indexor is a lightweight web application designed to load, display, and manage master lore tracking files directly through the Google Drive API.

The project features a fully responsive mobile layout with `100dvh` support, mobile browser cache recovery (`pageshow`), touch-sensitive sidebar swipe gestures, and zero-exposure security architecture.

---

## 🏗 Project Architecture

- **`index.html`**: Main user interface, app logic, touch swipe handlers, and Google Drive API integration.
- **`.github/workflows/deploy.yml`**: GitHub Actions CI/CD pipeline that injects secrets, generates a temporary `config.js`, and deploys the build to GitHub Pages.
- **`.gitignore`**: Excludes local `config.js` files to prevent credentials from being tracked or pushed to Git.
- **`config.js`** *(Dynamically Generated)*: Holds `CLIENT_ID` and `DRIVE_FILE_ID` runtime variables during local development or production builds.

---

## 📱 Mobile & Touch Features

- **Swipe Gestures:** 
  - Swipe **left** across the sidebar to collapse it.
  - Swipe **right** from the far left edge of the screen to open the sidebar.
- **State Persistence:** Automatically re-initializes view states and layout bounds when restored from mobile browser backgrounding (`bfcache`).

---

## 🔒 Security & Repository Secrets Setup

Sensitive credentials must be added to your repository before deployment:

1. Go to **Settings** > **Secrets and variables** > **Actions**.
2. Click **New repository secret** to add:
   - `CLIENT_ID`: Your Google Cloud OAuth 2.0 Client ID.
   - `DRIVE_FILE_ID`: The target Google Drive file ID for your lore file.

---

## 🌐 Google Cloud Console Authorized URLs

To prevent `Error 400: origin_mismatch` during Google Sign-In, ensure your domains are added to your Google Cloud Console:

1. Open the [Google Cloud Console Credentials Page](https://console.cloud.google.com/apis/credentials).
2. Click on your **OAuth 2.0 Client ID** to edit settings.
3. Under **Authorized JavaScript origins**, add your root domains:

| Environment | Authorized JavaScript Origin URI |
| :--- | :--- |
| **Production (GitHub Pages)** | `https://DarrkLive.github.io` |
| **Local Development** | `http://localhost:8000` |
| **Local IP Alternative** | `http://127.0.0.1:8000` |

> **Note:** Do not include subpaths (e.g., `/lore-indexor/`). Save and allow up to 2 minutes for changes to update.

---

## 🚀 Automated Deployment Pipeline

Every push to the `main` branch automatically triggers `.github/workflows/deploy.yml`. 

The deployment pipeline uses GitHub Action dependencies:
- `actions/checkout@v4`
- `actions/configure-pages@v4`
- `actions/upload-pages-artifact@v3`
- `actions/deploy-pages@v4`

---

## 💻 Local Development Setup

To test changes locally on your machine before pushing to GitHub:

1. Create a `config.js` file in the root folder:
   ```javascript
   const CONFIG = {
     CLIENT_ID: 'YOUR_LOCAL_CLIENT_ID',
     DRIVE_FILE_ID: 'YOUR_LOCAL_FILE_ID'
   };

   ```

  2. Start a local HTTP web server:

python3 -m http.server 8000

3. Navigate to http://127.0.0.1:8000 or http://localhost:8000 in your web browser.
