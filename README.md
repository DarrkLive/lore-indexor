# Lore Indexor 📚

Lore Indexor is a web application designed to load, display, and manage master lore tracking files directly through the Google Drive API.

The project utilizes a zero-exposure security architecture: sensitive API credentials (`CLIENT_ID` and `DRIVE_FILE_ID`) are stored in GitHub Repository Secrets and injected dynamically at build time via GitHub Actions, keeping the public repository fully secure.

---

## 🏗 Project Architecture

- **`index.html`**: Main user interface, app logic, and Google Drive API integration scripts.
- **`.github/workflows/deploy.yml`**: GitHub Actions CI/CD pipeline that injects secrets, generates a temporary `config.js`, and deploys the build to GitHub Pages.
- **`.gitignore`**: Excludes local `config.js` files to prevent credentials from being tracked or pushed to Git.
- **`config.js`** *(Dynamically Generated)*: Holds `CLIENT_ID` and `DRIVE_FILE_ID` runtime variables during local development or production CI/CD builds.

---

## 🔒 Security & Repository Secrets Setup

Sensitive credentials must be added to your repository before deployment:

1. Go to **Settings** > **Secrets and variables** > **Actions**.
2. Click **New repository secret** to add:
   - `CLIENT_ID`: Your Google Cloud OAuth 2.0 Client ID.
   - `DRIVE_FILE_ID`: The target Google Drive file ID for your lore file.

---

## 🌐 Google Cloud Console Authorized URLs

To prevent `Error 400: origin_mismatch` during Google Sign-In, both your local development server and live GitHub Pages domains must be added to your Google Cloud Console.

1. Open the [Google Cloud Console Credentials Page](https://console.cloud.google.com/apis/credentials).
2. Click on your **OAuth 2.0 Client ID** to edit settings.
3. Under **Authorized JavaScript origins**, click **Add URI** and add the following URLs:

| Environment | Authorized JavaScript Origin URI |
| :--- | :--- |
| **Production (GitHub Pages)** | `https://DarrkLive.github.io` |
| **Local Development** | `http://localhost:8000` |
| **Local IP Alternative** | `http://127.0.0.1:8000` |

> **Note:** Do not include subpaths or repository names (e.g., `/lore-indexor/`) in the Authorized JavaScript origins section—only enter the root protocol and domain name. Save and allow up to 2 minutes for origin changes to update.

---

## 🚀 Automated Deployment Pipeline

Every push to the `main` branch automatically triggers `.github/workflows/deploy.yml`. 

The deployment pipeline uses current GitHub Action dependencies:
- `actions/checkout@v4`
- `actions/configure-pages@v4`
- `actions/upload-pages-artifact@v3`
- `actions/deploy-pages@v4`

### Action Workflow Script (`.github/workflows/deploy.yml`)

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Generate config.js securely
        run: |
          echo "const CONFIG = {" > config.js
          echo "  CLIENT_ID: '${{ secrets.CLIENT_ID }}'," >> config.js
          echo "  DRIVE_FILE_ID: '${{ secrets.DRIVE_FILE_ID }}'" >> config.js
          echo "};" >> config.js

      - name: Setup Pages
        uses: actions/configure-pages@v4

      - name: Upload Artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'

      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```
To test changes locally on your machine before pushing to GitHub:

    Create a config.js file in the root folder:
    JavaScript

    const CONFIG = {
      CLIENT_ID: 'YOUR_LOCAL_CLIENT_ID',
      DRIVE_FILE_ID: 'YOUR_LOCAL_FILE_ID'
    };

    Start a local HTTP web server:
    Bash

    python3 -m http.server 8000

    Navigate to http://127.0.0.1:8000 or http://localhost:8000 in your web browser.

    .gitignore ensures your local config.js file is never uploaded to GitHub.
