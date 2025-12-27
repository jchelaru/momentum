# Deploy to GitHub Pages

This guide will help you deploy your Momentum habit tracker to GitHub Pages.

## Prerequisites

- A GitHub account
- Your project pushed to a GitHub repository
- Supabase credentials set up

## Step 1: Push Your Code to GitHub

If you haven't already, create a repository and push your code:

```bash
# Initialize git (if not already done)
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit"

# Add your GitHub repository as remote
# Replace 'yourusername' and 'momentum' with your actual values
git remote add origin https://github.com/yourusername/momentum.git

# Push to main branch
git branch -M main
git push -u origin main
```

## Step 2: Configure Repository Name in Vite Config

**Important**: If your repository name is NOT `momentum`, you need to update the base path:

1. Open `vite.config.js`
2. Find the line: `base: process.env.GITHUB_PAGES === 'true' ? '/momentum/' : '/',`
3. Replace `/momentum/` with `/[your-repo-name]/`

For example, if your repo is `my-habit-tracker`:
```javascript
base: process.env.GITHUB_PAGES === 'true' ? '/my-habit-tracker/' : '/',
```

**If deploying to a custom domain (yourusername.github.io):**
- Change the base to `'/'` (root path)

## Step 3: Add Supabase Secrets to GitHub

1. Go to your GitHub repository
2. Click **Settings** → **Secrets and variables** → **Actions**
3. Click **New repository secret**
4. Add these two secrets:

   **Secret 1:**
   - Name: `VITE_SUPABASE_URL`
   - Value: Your Supabase project URL (from your `.env` file)

   **Secret 2:**
   - Name: `VITE_SUPABASE_ANON_KEY`
   - Value: Your Supabase anon key (from your `.env` file)

## Step 4: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** → **Pages** (left sidebar)
3. Under **Source**, select:
   - **Source**: `GitHub Actions`
4. Click **Save**

## Step 5: Trigger Deployment

The deployment will automatically trigger when you:
- Push to the `main` branch, OR
- Manually trigger it from the **Actions** tab

To manually trigger:
1. Go to **Actions** tab in your repository
2. Select **Deploy to GitHub Pages** workflow
3. Click **Run workflow** → **Run workflow**

## Step 6: Access Your Deployed App

After deployment completes (usually 1-2 minutes):

1. Go to **Settings** → **Pages**
2. Your site URL will be shown (e.g., `https://yourusername.github.io/momentum/`)
3. Click the link to view your deployed app!

## Troubleshooting

### Build Fails - Missing Environment Variables
- Make sure you added `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` as GitHub Secrets
- Check the Actions tab for detailed error messages

### 404 Errors / Blank Page
- Verify the `base` path in `vite.config.js` matches your repository name
- Check browser console for errors
- Ensure the build completed successfully in Actions

### Routes Not Working
- GitHub Pages serves static files, so client-side routing needs special handling
- The app should work, but direct URL access to routes might need a `404.html` redirect
- Consider using HashRouter instead of BrowserRouter for GitHub Pages (see below)

### Authentication Issues
- Verify Supabase URL and keys are correct in GitHub Secrets
- Check Supabase dashboard to ensure your project is active
- Review browser console for specific error messages

## Optional: Use HashRouter for Better GitHub Pages Support

If you experience routing issues, you can switch to HashRouter:

1. Open `src/App.jsx`
2. Change:
   ```javascript
   import { BrowserRouter, ... } from 'react-router-dom'
   ```
   to:
   ```javascript
   import { HashRouter, ... } from 'react-router-dom'
   ```
3. Replace `<BrowserRouter>` with `<HashRouter>`

This will use hash-based routing (`#/route`) which works better with static hosting.

## Custom Domain Setup

To use a custom domain:

1. In GitHub Pages settings, add your custom domain
2. Update DNS records as instructed by GitHub
3. Update `vite.config.js` base to `'/'` (root path)
4. Rebuild and redeploy

## Updating Your Deployment

Every time you push to `main`, the site will automatically rebuild and deploy. Just:

```bash
git add .
git commit -m "Your changes"
git push
```

The GitHub Action will handle the rest!

## Local Testing Before Deploy

To test the GitHub Pages build locally:

```bash
npm run build:gh-pages
npm run preview
```

This builds with the GitHub Pages base path so you can verify everything works.

