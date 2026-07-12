# Deploying World Intelligence OS

This folder is ready to deploy as-is. Two files:

- `index.html` — the whole app
- `api/ask.js` — a serverless function that keeps your Claude API key private and powers the "Ask AI" features

## Fastest path: Vercel (free tier, ~5 minutes)

1. Go to https://vercel.com and sign up / log in (GitHub login is easiest).
2. Click **Add New → Project**.
3. Either:
   - **Push this folder to a GitHub repo** and import it in Vercel, or
   - Use the Vercel CLI: install with `npm i -g vercel`, then from inside this folder run `vercel` and follow the prompts.
4. Before your first deploy finishes, go to **Project → Settings → Environment Variables** and add:
   - Key: `ANTHROPIC_API_KEY`
   - Value: your key from https://console.anthropic.com/settings/keys
5. Deploy. Vercel gives you a live URL immediately (e.g. `your-project.vercel.app`).
6. To use your own domain: **Project → Settings → Domains → Add**, then point your domain's DNS at Vercel per the instructions shown there.

No build step is needed — Vercel serves `index.html` as a static file and auto-detects `api/ask.js` as a serverless function.

## Alternative: Netlify

Same idea, slightly different serverless syntax:
1. Drag this folder into https://app.netlify.com/drop for the static part (instant, no AI assistant yet).
2. To add the AI proxy, move `api/ask.js` into `netlify/functions/ask.js` and change its export to `exports.handler = async (event) => {...}` (Netlify's function signature differs slightly from Vercel's — ask me if you want this rewritten for Netlify specifically).
3. Set `ANTHROPIC_API_KEY` under **Site settings → Environment variables**.

## Alternative: Cloudflare Pages

Also works well and is generous on the free tier; Cloudflare Pages Functions use a similar but distinct signature (`onRequestPost`). Ask if you want the `api/ask.js` rewritten for that runtime.

## If you skip the proxy entirely

You can deploy just `index.html` on any static host (GitHub Pages, S3, plain Nginx, etc.) with zero setup. Everything works — crypto, forex, earthquakes, country data, news — **except** the "Ask AI" boxes, which will show "Could not reach the AI assistant" since there's no key behind `/api/ask`. That's a fine place to start if you want something live today and can wire up the AI part later.

## What does NOT need a key

These all call free public APIs directly from the browser and need no server at all:
- CoinGecko (crypto prices)
- Frankfurter.app (forex rates)
- USGS (earthquakes)
- REST Countries (country facts)
- GDELT (news headlines)

They're all subject to their own rate limits, so if you get heavy traffic later, that's the first thing to watch.
