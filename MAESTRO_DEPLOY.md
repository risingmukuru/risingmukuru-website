# Maestro's Deployment Guide
## Rising Mukuru Website — GitHub + Cloudflare Pages + Netlify CMS Auth

---

## Overview

```
Beth edits → Decap CMS → commits to GitHub → Cloudflare deploys → live site updates
You push code → GitHub → Cloudflare deploys → live site updates
```

Everything is free except the domain (~$15/year). No servers to manage.

---

## Phase 1 — Create Organization Accounts

Create fresh accounts using the Rising Mukuru email (`hello@risingmukuru.org` once set up, or a temp Gmail to start):

### 1a. GitHub
1. Go to `https://github.com/join`
2. Create account: `risingmukuru` (username)
3. Create a **new repository**: `risingmukuru-website`
   - Make it **Public** (required for free Cloudflare Pages)
   - Don't add any files yet

### 1b. Netlify (CMS Auth only — not for hosting)
1. Go to `https://app.netlify.com` → sign up with the GitHub account above
2. No need to deploy anything here — Netlify is only used for the OAuth "Login with GitHub" button in the CMS

### 1c. Cloudflare
1. Go to `https://dash.cloudflare.com` → create account
2. Add your domain (you bought it — transfer nameservers to Cloudflare for free DNS + Pages hosting)

---

## Phase 2 — Push the Site to GitHub

On your machine, open Terminal (or use GitHub Desktop if you prefer a GUI):

```bash
# Navigate to the project folder
cd "/path/to/Rising Mukuru Main Files for claude"

# Initialize git
git init
git add .
git commit -m "Initial Rising Mukuru website"

# Connect to GitHub repo
git remote add origin https://github.com/risingmukuru/risingmukuru-website.git
git branch -M main
git push -u origin main
```

---

## Phase 3 — Connect Cloudflare Pages

1. In Cloudflare Dashboard → **Pages** → **Create a project**
2. Click **Connect to Git** → select **GitHub** → authorize
3. Select the `risingmukuru/risingmukuru-website` repo
4. Build settings:
   - **Framework preset:** None
   - **Build command:** *(leave blank)*
   - **Build output directory:** `/` (root)
5. Click **Save and Deploy**

Cloudflare will deploy the site and give you a URL like `risingmukuru-website.pages.dev`. Test it — the full site should be live.

---

## Phase 4 — Connect Your Domain

1. In Cloudflare Dashboard → Pages → your project → **Custom domains**
2. Add `risingmukuru.org` and `www.risingmukuru.org`
3. Cloudflare will automatically set the DNS records (it controls your nameservers)
4. Done — usually live within minutes

---

## Phase 5 — Set Up Netlify CMS Auth

This is what lets Beth click "Login with GitHub" on the `/admin` page:

1. In **Netlify** → Sites → **Add new site** → **Deploy manually** → drag any empty folder
2. Go to **Site settings** → **Access control** → **OAuth**
3. Click **Install provider** → **GitHub**
4. You'll need to create a GitHub OAuth App:
   - Go to GitHub → Settings → Developer settings → OAuth Apps → New OAuth App
   - **Application name:** Rising Mukuru CMS
   - **Homepage URL:** `https://risingmukuru.org`
   - **Authorization callback URL:** `https://api.netlify.com/auth/done`
   - Copy the **Client ID** and generate a **Client Secret**
5. Back in Netlify → paste Client ID and Client Secret → Save
6. Note your Netlify site URL (e.g. `calm-thunder-abc123.netlify.app`)

The `admin/config.yml` is already configured with `base_url: https://api.netlify.com` — this matches the setup above.

---

## Phase 6 — Test the CMS

1. Go to `https://risingmukuru.org/admin`
2. Click **Login with GitHub**
3. Authorize the app
4. You should land on the Decap CMS dashboard
5. Make a small edit (e.g. change a stat number) and click **Publish**
6. Check GitHub — you should see a new commit appear automatically
7. Cloudflare should redeploy within 30–60 seconds
8. Refresh the live site — the change should be visible

If the CMS login button doesn't appear or redirects to an error, double-check the OAuth callback URL in the GitHub OAuth App settings.

---

## Phase 7 — Set Up Formspree (Volunteer Forms)

1. Go to `https://formspree.io` → create account with org email
2. Create a new form → copy the endpoint URL (e.g. `https://formspree.io/f/xyzabc123`)
3. Go to `/admin` → Volunteer Page → Volunteer Settings
4. Paste the URL into the **Formspree Endpoint** field → Publish
5. The volunteer forms will now email submissions to the org email

Free tier: 50 submissions/month. Upgrade if needed.

---

## Phase 8 — Set Up Zenlipa (Donations)

1. Beth creates a Zenlipa merchant account at `https://zenlipa.com`
2. She gets a payment link URL (looks like `https://zenlipa.com/pay/risingmukuru`)
3. Go to `/admin` → Donate Page → Donation Settings
4. Paste the URL into **Zenlipa Base URL** → Publish
5. Test with a small amount to confirm it works

---

## Phase 9 — Set Up Brevo Newsletter

1. Go to `https://brevo.com` → create account
2. Create a subscription form
3. Embed the form HTML into the footer area of `index.html` (a small code snippet)
4. Push the updated `index.html` to GitHub → Cloudflare auto-deploys

Free tier: 300 emails/day, unlimited contacts. Perfect for Rising Mukuru's scale.

---

## Ongoing: How to Push Code Updates

Whenever you make improvements to the site:

```bash
cd "/path/to/Rising Mukuru Main Files for claude"
git add .
git commit -m "describe what you changed"
git push
```

Cloudflare detects the push and redeploys automatically. Usually live within 60 seconds.

---

## Folder Structure Reference

```
risingmukuru-website/
├── index.html              ← Homepage
├── donate.html             ← Donate page
├── volunteer.html          ← Volunteer page
├── assets/
│   └── images/             ← All community photos
├── admin/
│   ├── index.html          ← Decap CMS entry point
│   └── config.yml          ← CMS field configuration (edit here to add/remove fields)
└── content/
    ├── data/               ← JSON files Beth edits via the CMS
    │   ├── contact.json
    │   ├── hero.json
    │   ├── stats.json
    │   ├── about.json
    │   ├── cta.json
    │   ├── donate.json
    │   └── volunteer.json
    ├── programs/           ← One markdown file per program
    └── stories/            ← One markdown file per community story
```

---

## Costs Summary

| Service | Cost |
|---|---|
| GitHub | Free |
| Cloudflare Pages | Free |
| Netlify (auth only) | Free |
| Decap CMS | Free |
| Formspree (50 submissions/month) | Free |
| Brevo (300 emails/day) | Free |
| Domain (risingmukuru.org) | ~$15/year |
| Zenlipa | Transaction fees only |
| Cloudflare Email Routing | Free with domain |

**Total: ~$15/year for the domain.**

---

## Emergency: Reverting a Bad Edit by Beth

If Beth publishes something that breaks the site:

1. Go to `https://github.com/risingmukuru/risingmukuru-website`
2. Click on the affected file (e.g. `content/data/contact.json`)
3. Click **History** → find the last good commit
4. Click the commit → **Browse files** → open the old version
5. Copy the content → go back to the current file → click Edit → paste → commit

Or in Terminal:
```bash
git log --oneline content/data/contact.json
git checkout <commit-hash> -- content/data/contact.json
git commit -m "Revert contact.json to previous version"
git push
```

---

*Built by Maestro Productions for The Rising Mukuru.*
*Questions: paimaxxproductions@gmail.com*
