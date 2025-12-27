# Quick GitHub Pages Deployment

## 🚀 5-Minute Setup

### 1. Push to GitHub
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
git push -u origin main
```

### 2. Update Repository Name (if needed)
If your repo is NOT named `momentum`, edit `vite.config.js`:
- Change `/momentum/` to `/[your-repo-name]/` on line 9

### 3. Add GitHub Secrets
Go to: **Settings → Secrets and variables → Actions**

Add two secrets:
- `VITE_SUPABASE_URL` = Your Supabase URL
- `VITE_SUPABASE_ANON_KEY` = Your Supabase anon key

### 4. Enable GitHub Pages
Go to: **Settings → Pages**
- Source: **GitHub Actions**
- Click **Save**

### 5. Deploy!
- Push to `main` branch (auto-deploys), OR
- Go to **Actions** tab → **Run workflow**

### 6. Access Your Site
After ~2 minutes, find your URL at:
**Settings → Pages** → Your site is live at `https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/`

---

📖 **Full guide**: See `GITHUB_PAGES_DEPLOY.md`

