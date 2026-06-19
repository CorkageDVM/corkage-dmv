# Deploying Corkage DMV to Cloudflare Pages

The whole site is static (`index.html` + a few support files), so it deploys to
Cloudflare Pages with no build step. Two ways to do it — start with Option A.

## Option A — Direct upload (fastest, live in ~5 min, no GitHub needed)

1. Log in at https://dash.cloudflare.com → **Workers & Pages** → **Create** → **Pages** → **Upload assets**.
2. Name the project (e.g. `corkage-dmv`).
3. Drag this entire folder's contents (`index.html`, `_headers`, `robots.txt`) into the upload box.
4. Click **Deploy**. You'll get a free URL like `corkage-dmv.pages.dev`.
5. To publish changes later, open the project → **Create new deployment** → upload the updated files again.

## Option B — Git-backed (best once you're editing often / adding pages)

1. Put this folder in a GitHub repo (free). Tell me and I'll initialize git and the first commit.
2. In Cloudflare: **Create** → **Pages** → **Connect to Git** → pick the repo.
3. Build settings: **Framework preset = None**, **Build command = (blank)**, **Output directory = /**.
4. Every push to the main branch auto-deploys. No manual uploads.

## Pointing your domain (moving off WordPress)

The exact steps depend on where the domain is registered and whether you want
to move DNS to Cloudflare. General flow:

1. In the Pages project → **Custom domains** → **Set up a domain** → enter your domain.
2. If the domain's DNS is already on Cloudflare, it adds the record automatically.
3. If DNS is elsewhere, Cloudflare gives you a CNAME (or asks you to move nameservers).
   For a full move off WordPress, transferring nameservers to Cloudflare is cleanest.
4. **Don't cancel WordPress hosting until the new site resolves on the live domain** —
   verify `https://yourdomain.com` shows this directory first.

## Notes / dependencies in the current site

- Google Fonts loaded from CDN — works as-is on Pages.
- The "Suggest a Restaurant" form posts to Formspree (`formspree.io/f/xzdqqqbb`) —
  works on static hosting, no server needed.
- No database, no build, no server-side code.
