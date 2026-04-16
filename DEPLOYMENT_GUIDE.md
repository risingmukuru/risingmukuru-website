# DEPLOYMENT GUIDE: GitHub → Cloudflare Pages

**Time Required:** 15-20 minutes  
**Cost:** FREE  
**Difficulty:** Easy (no coding required)

---

## STEP 1: CREATE GITHUB ACCOUNT (3 min)

1. Go to **github.com**
2. Click **Sign up**
3. Enter email, password, username
4. Verify email
5. ✅ Account created

---

## STEP 2: CREATE NEW REPOSITORY (2 min)

1. After login, click **+** (top right) → **New repository**
2. Repository name: `rising-mukuru-website`
3. Description: "The Rising Mukuru — Dynamic website for community NGO"
4. Visibility: **Public** (so Cloudflare can access)
5. Click **Create repository**
6. ✅ Repository created

---

## STEP 3: UPLOAD FILES TO GITHUB (5 min)

**Option A: Via GitHub Web Interface (Easiest)**

1. In your new repository, click **Add file** → **Upload files**
2. Drag & drop these 3 files:
   - `index.html`
   - `donate.html`
   - `volunteer.html`
3. Click **Commit changes**
4. ✅ Files uploaded

**Option B: Via Git Command Line (If you know Git)**

```bash
git clone https://github.com/YOUR_USERNAME/rising-mukuru-website.git
cd rising-mukuru-website
cp index.html donate.html volunteer.html .
git add .
git commit -m "Initial commit: Dynamic website with 5 features"
git push origin main
```

---

## STEP 4: CONNECT GITHUB TO CLOUDFLARE (5 min)

1. Go to **pages.cloudflare.com**
2. Click **Create a project**
3. Select **Connect to Git**
4. **Authorize Cloudflare** to access GitHub (click "Authorize Cloudflare")
5. **Select your GitHub account**
6. **Select repository:** `rising-mukuru-website`
7. Click **Begin setup**

---

## STEP 5: CONFIGURE BUILD SETTINGS (2 min)

**Build settings:**
- Build command: *(leave blank)*
- Build output directory: *(leave blank)*
- Root directory: `/` (default)

**Environment variables:** *(leave blank)*

Click **Save and Deploy**

---

## STEP 6: WAIT FOR DEPLOYMENT (2 min)

Cloudflare builds & deploys automatically. You'll see:
```
✅ Deployment successful
🌐 Your site is live at: risingmukuru.pages.dev
```

---

## STEP 7: TEST YOUR SITE (3 min)

**Test these URLs:**
- `https://risingmukuru.pages.dev/` — Homepage
- `https://risingmukuru.pages.dev/donate.html` — Donation page
- `https://risingmukuru.pages.dev/volunteer.html` — Volunteer page

**Verify these work:**
- ✅ Scroll animations
- ✅ Counter stats
- ✅ Carousel slides
- ✅ Calculator updates
- ✅ Donation buttons link to Zenlipa
- ✅ Forms work

---

## STEP 8: CUSTOM DOMAIN (Optional, 10 min)

**Already have a domain?** (e.g., risingmukuru.org)

1. In Cloudflare Pages, click **Custom domains**
2. Click **Set up a domain**
3. Enter your domain: `risingmukuru.org`
4. Follow DNS setup instructions
5. Wait 24 hours for DNS to propagate

---

## TROUBLESHOOTING

### Site shows blank page?
- Check GitHub repository is **Public**
- Verify files are in root directory (not in a folder)
- Wait 5 minutes for rebuild

### Donation button doesn't work?
- Make sure Zenlipa URLs are updated
- Test link directly in browser

### Forms don't submit?
- Google Forms URL must be correct
- Forms must be published/shareable

### Slow loading?
- Should be instant (static site)
- Try clearing browser cache (Ctrl+Shift+Delete)

---

## FUTURE UPDATES

**When you make changes:**

1. Edit files locally
2. Upload to GitHub (via web or `git push`)
3. Cloudflare automatically rebuilds & deploys
4. Site updates within 1-2 minutes

**No need to touch Cloudflare again — it watches GitHub automatically!**

---

## YOUR LIVE WEBSITE

**Before Setup:**
- http://localhost:5173 (only you can see)

**After Setup:**
- https://risingmukuru.pages.dev (world can see!)
- https://risingmukuru.org (if you connect a domain)

---

## QUICK REFERENCE

| Step | What | Time |
|------|------|------|
| 1 | Create GitHub account | 3 min |
| 2 | Create repository | 2 min |
| 3 | Upload files | 5 min |
| 4 | Connect to Cloudflare | 5 min |
| 5 | Configure & deploy | 2 min |
| 6 | Test site | 3 min |
| **TOTAL** | **Live website** | **20 min** |

---

## NEXT: FINALIZE YOUR SITE

Before deploying, make sure you've done:

- [ ] Updated Zenlipa URLs in donate.html
- [ ] Created Google Form & linked in volunteer.html
- [ ] Updated contact email & phone in all pages
- [ ] Added community photos (optional but recommended)
- [ ] Tested all links locally (http://localhost:5173)

---

## SUPPORT

**Cloudflare Help:**
- https://support.cloudflare.com/hc/en-us/categories/200322407-Cloudflare-Pages

**GitHub Help:**
- https://docs.github.com/en/get-started

**Questions?** You can always re-deploy by pushing updates to GitHub!

---

## 🎉 YOU'RE DONE!

Your Rising Mukuru website is now live on the internet.

Share it with:
- Beth & the Mukuru community
- Donors & partners
- International funding sources
- Anyone who can help

Let's rise together. 💚
