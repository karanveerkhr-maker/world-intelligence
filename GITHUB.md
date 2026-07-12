# Getting this live on GitHub

The repo is already initialized and committed in this folder (`git log` shows one commit). You just need to create the GitHub repo and push.

## Step 1 — Create the repo on GitHub

1. Go to https://github.com/new
2. Name it (e.g. `world-intelligence-os`)
3. Leave it **empty** — don't check "Add a README" (we already have files)
4. Click **Create repository**

## Step 2 — Push this folder

GitHub will show you a remote URL like `https://github.com/<your-username>/world-intelligence-os.git`.
From inside this folder, run:

```
git remote add origin https://github.com/<your-username>/world-intelligence-os.git
git push -u origin main
```

You'll be prompted for GitHub credentials — GitHub no longer accepts your account password here, so use a **Personal Access Token** instead: https://github.com/settings/tokens → "Generate new token (classic)" → check the `repo` scope → use that token as your password when prompted.

## Step 3 — Turn on GitHub Pages

1. In your new repo, go to **Settings → Pages**
2. Under "Build and deployment", set **Source** to `Deploy from a branch`
3. Branch: `main`, folder: `/ (root)` → **Save**
4. GitHub gives you a live URL within a minute or two, typically:
   `https://<your-username>.github.io/world-intelligence-os/`

That's it — the dashboard, globe, live crypto/forex/quakes/news/economy data all work immediately at that URL.

## About the AI Assistant on GitHub Pages

GitHub Pages only serves static files, so `api/ask.js` won't run there — the "Ask AI" boxes will show "Could not reach the AI assistant." Two ways to fix that without leaving GitHub:

**Option A — Vercel connected to this same GitHub repo (recommended, still free)**
1. Go to https://vercel.com → **Add New → Project** → **Import Git Repository** → pick this repo.
2. In the import screen (or after, under Settings → Environment Variables), add `ANTHROPIC_API_KEY` with a key from https://console.anthropic.com/settings/keys
3. Deploy. Vercel builds from the *same* GitHub repo, so every future `git push` auto-deploys to both GitHub Pages (static) and Vercel (full app) at once, if you keep both connected.
4. Use the Vercel URL as your "real" site (AI works); GitHub Pages URL still works as a lighter mirror without AI.

**Option B — GitHub Actions + a different backend**
More involved — a GitHub Action can't run a persistent serverless function itself, so you'd still need somewhere like Vercel, Cloudflare Workers, or Railway to host `api/ask.js`. Ask if you want this path instead.

## Keeping it updated

Any time you want to change something: edit `index.html` locally, then:
```
git add -A
git commit -m "describe what changed"
git push
```
GitHub Pages (and Vercel, if connected) will redeploy automatically.
