# obfy.xyz — Setup Guide

## Repo Structure

```
obfy/
├── index.html          ← landing page (obfy.xyz)
├── toddler.html        ← toddler mode (obfy.xyz/toddler)
└── .github/
    └── workflows/
        └── deploy.yml  ← auto-deploy on push to main
```

---

## Step 1 — Create GitHub Repo

```bash
cd obfy
git init
git add .
git commit -m "initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/obfy.git
git push -u origin main
```

---

## Step 2 — Enable GitHub Pages

1. Go to your repo on GitHub
2. **Settings → Pages**
3. Under **Source**, select **GitHub Actions**
4. Push anything to `main` — the workflow auto-deploys
5. GitHub gives you a URL like `https://yourusername.github.io/obfy`

---

## Step 3 — Add Custom Domain in GitHub

1. **Settings → Pages → Custom domain**
2. Type: `obfy.xyz`
3. Click Save — GitHub creates a `CNAME` file automatically
4. Check **Enforce HTTPS** once DNS propagates

---

## Step 4 — Point obfy.xyz DNS at GitHub Pages

Log into wherever obfy.xyz is registered (Namecheap, Cloudflare, etc.) and add these records:

### If using Cloudflare DNS (recommended):

| Type | Name | Content | Proxy |
|------|------|---------|-------|
| A | @ | 185.199.108.153 | ❌ DNS only |
| A | @ | 185.199.109.153 | ❌ DNS only |
| A | @ | 185.199.110.153 | ❌ DNS only |
| A | @ | 185.199.111.153 | ❌ DNS only |
| CNAME | www | YOUR_USERNAME.github.io | ❌ DNS only |

> ⚠️ **Important:** Set Cloudflare proxy to **DNS only** (grey cloud, not orange).
> GitHub Pages handles HTTPS itself — Cloudflare proxying breaks it.

### If using Namecheap or another registrar:

Add the same 4 A records above pointing to GitHub's IPs.

---

## Step 5 — Transfer Domain to Cloudflare (Optional but recommended)

Since you use Cloudflare for everything else:

1. Go to **Cloudflare → Add a site → obfy.xyz**
2. Choose the free plan
3. Cloudflare scans existing DNS records
4. Update nameservers at your registrar to Cloudflare's
5. Once active, add the A records from Step 4 with proxy **off**

---

## Deploying Updates

Just push to `main` — GitHub Actions handles the rest:

```bash
git add .
git commit -m "update"
git push
```

Live in ~30 seconds.

---

## Adding New Pages

Drop any `.html` file in the root and it's live at `obfy.xyz/filename`:

```
obfy/
├── index.html       → obfy.xyz
├── toddler.html     → obfy.xyz/toddler
├── nextidea.html    → obfy.xyz/nextidea   ← just add files
```

No build step, no config, no framework needed.
