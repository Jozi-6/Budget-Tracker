# GitHub Pages Deployment Instructions

## Overview
This application uses Firebase for backend services. The Firebase configuration is stored in `config.js`, which is excluded from version control for security. To deploy to GitHub Pages, we use GitHub Actions to dynamically generate the `config.js` file from repository secrets during deployment.

## Step 1: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** > **Pages**
3. Under **Build and deployment**, select **GitHub Actions** as the source
4. Click **Save**

## Step 2: Add Firebase Configuration as Repository Secrets

1. Go to your repository on GitHub
2. Click **Settings** > **Secrets and variables** > **Actions**
3. Click **New repository secret**
4. Add the following secrets (get these from your Firebase Console):

### Required Secrets

| Secret Name | Description | Example |
|------------|-------------|---------|
| `FIREBASE_API_KEY` | Your Firebase API key | `AIzaSyAk3D8yH7WiSlTHo6UrZEckL5aT7IUqUFQ` |
| `FIREBASE_AUTH_DOMAIN` | Your Firebase Auth domain | `budget-tracker-7d6a3.firebaseapp.com` |
| `FIREBASE_PROJECT_ID` | Your Firebase project ID | `budget-tracker-7d6a3` |
| `FIREBASE_STORAGE_BUCKET` | Your Firebase storage bucket | `budget-tracker-7d6a3.firebasestorage.app` |
| `FIREBASE_MESSAGING_SENDER_ID` | Your Firebase messaging sender ID | `158701995803` |
| `FIREBASE_APP_ID` | Your Firebase app ID | `1:158701995803:web:578dfb93e5a5608ce175be` |
| `FIREBASE_MEASUREMENT_ID` | Your Firebase measurement ID (optional) | `G-5Y7CZ81MSM` |

### How to Get Your Firebase Configuration

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Select your project
3. Click the gear icon (⚙️) > **Project settings**
4. Scroll down to **Your apps** > **Web app**
5. Copy the configuration values

## Step 3: Enable Anonymous Authentication in Firebase

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Select your project
3. Click **Authentication** in the left sidebar
4. Click **Get Started**
5. Enable **Anonymous** sign-in provider
6. Click **Save**

## Step 4: Push Your Changes

Push the following files to your repository:
- `.github/workflows/deploy.yml` - GitHub Actions workflow
- Updated `index.html` - Improved error handling
- `config.example.js` - Template for local development

```bash
git add .
git commit -m "Add GitHub Pages deployment with Firebase config"
git push origin main
```

## Step 5: Verify Deployment

1. Go to your repository on GitHub
2. Click the **Actions** tab
3. You should see the "Deploy to GitHub Pages" workflow running
4. Wait for the workflow to complete (green checkmark)
5. Click the workflow run to see the deployment details
6. Visit your GitHub Pages URL to verify the app is working

## Local Development

For local development, create a `config.js` file in the project root:

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID",
    measurementId: "YOUR_MEASUREMENT_ID"
};
```

**Important:** The `config.js` file is in `.gitignore` and will not be committed to the repository.

## Troubleshooting

### App shows "Firebase configuration not found" in production
- Verify all secrets are added to GitHub Repository Settings
- Check the Actions workflow logs for any errors
- Ensure the workflow is using the correct secret names

### App works locally but not on GitHub Pages
- Make sure you pushed the `.github/workflows/deploy.yml` file
- Verify GitHub Pages is enabled and set to use GitHub Actions
- Check that all required secrets are configured

### Firebase authentication errors
- Verify Anonymous Authentication is enabled in Firebase Console
- Check that Firestore security rules allow authenticated users
