# VidGrab marketing site

Static landing + legal/support pages for VidGrab.

## Stack

- Plain HTML5 + Tailwind CDN + Inter (Google Fonts)
- Vanilla JS for tiny interactions (FAQ accordion, smooth scroll, scroll-reveal)
- Zero build step. Deploy as-is.

## Pages

| Path | Purpose |
|---|---|
| `/` (index.html) | Marketing landing - hero, features, pricing, FAQ, CTA |
| `/privacy.html` | Privacy policy - required for Chrome Web Store |
| `/terms.html` | Terms of service |
| `/refund.html` | 30-day money-back policy (referenced from paywall) |
| `/support.html` | FAQ + email contact |
| `/sitemap.xml` | SEO |
| `/robots.txt` | SEO |
| `/assets/og-image.png` | 1200×630 social preview (regenerable from `og-image.svg`) |

## Deploy in 30 seconds - pick one

### Option A - Netlify Drop (NO account needed for instant URL)

1. Go to https://app.netlify.com/drop
2. Drag the entire `website/` folder onto the drop zone
3. Get an instant URL like `https://random-name.netlify.app`
4. Optionally claim it by signing up (keeps the URL, lets you connect a custom domain)

**Best when**: you want it live in 30 seconds with zero commitment.

### Option B - Vercel CLI (recommended)

```bash
cd website
npx vercel --yes
```

Prompts on first run only:
- Sign in (opens browser)
- Link to project (accept defaults)

Subsequent deploys: `npx vercel --prod` (instant).

**Best when**: you want a long-term home with great DX, automatic HTTPS, custom domains, and analytics.

### Option C - Cloudflare Pages

1. Go to https://dash.cloudflare.com → Pages → Create a project
2. Upload assets → drag the `website/` folder
3. Get a `*.pages.dev` URL

**Best when**: you also use Cloudflare for DNS or CDN.

### Option D - GitHub Pages

1. Push the `website/` folder to a GitHub repo (or a `gh-pages` branch of an existing repo)
2. Settings → Pages → Source: Deploy from branch → `main` (or `gh-pages`) → folder `/website`
3. Wait 1-2 minutes → URL `https://<user>.github.io/<repo>/`

**Best when**: you already use GitHub and want zero new accounts.

---

## Custom domain (vidgrab.app)

After deploying:

### On Vercel
1. Project → Settings → Domains → Add `vidgrab.app`
2. Vercel shows the DNS records to add at your registrar
3. Add the records (typically: `A` record for apex, `CNAME` for `www`)
4. Wait for propagation (5 min - 24 h)
5. Vercel auto-issues an SSL certificate

### On Netlify
1. Site → Domain management → Add custom domain → `vidgrab.app`
2. Netlify shows DNS records to add
3. Add at your registrar → wait → done

### On Cloudflare Pages
1. Already on Cloudflare? Just add the domain to the project - DNS auto-configured.
2. Otherwise transfer the domain to Cloudflare or add the recommended records.

### Buy the domain
If `vidgrab.app` isn't yours yet:
- **Cloudflare Registrar** (cheapest, no markup, ~$10/year for `.app`) - recommended
- **Namecheap** (~$15-20/year `.app`)
- **Google Domains / Squarespace** (~$15-20/year)

---

## Update the OG image

The 1200×630 PNG OG image was generated from `assets/og-image.svg`. To regenerate:

```bash
cd /tmp && npm install sharp
node -e "
require('sharp')('./website/assets/og-image.svg')
  .resize(1200, 630).png()
  .toFile('./website/assets/og-image.png');
"
```

Or replace `og-image.png` manually with a custom 1200×630 design.

---

## Pre-publish checklist

Before going live:

- [ ] Replace **all** occurrences of `https://vidgrab.app/` with your real domain (in HTML, sitemap.xml, robots.txt) - do a project-wide find/replace
- [ ] Replace `support@vidgrab.app` with your real support email if different
- [ ] Update placeholder testimonials in `index.html` once you have real customer quotes
- [ ] Once the Chrome Web Store extension is live, replace the `href="#"` on "Add to Chrome" buttons with the real Web Store URL (search "Add to Chrome" in `index.html`)
- [ ] Add a Google Search Console property + submit `sitemap.xml` for SEO indexing
- [ ] (Optional) Generate a Plausible/Fathom/Umami account for privacy-respecting analytics - embed the snippet in each `<head>`
