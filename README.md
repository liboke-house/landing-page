# Liboké House — Landing Page

Minimalist single-page site for **Liboké House** (Nairobi) — *"L'authenticité congolaise, réinventée."*
Delivery-only, pre-launch page: brand story, upcoming drop dates, and a WhatsApp waitlist. No backend — it's a static site.

## Structure

```
landing-page/
├── assets/
│   ├── logo.png     # brand logo (favicon + og:image fallback)
│   └── tote.jpg      # branded signature tote, used in the "Packaging" section
├── index.html         # the entire site (HTML + CSS + a few lines of JS)
├── vercel.json         # redirects + security headers
└── README.md
```

## Editing content

Everything lives in `index.html` — no build step, no dependencies.

- **Drop dates**: edit the three `.drop-card` blocks in the `#drops` section.
- **WhatsApp number/message**: the `wa.me` links in `#reserve` and the footer. Format is `https://wa.me/<countrycode+number, no plus or spaces>?text=<url-encoded message>`.
- **Social links**: Instagram and TikTok URLs appear in the hero and footer.
- **Colors/fonts**: CSS variables at the top of the `<style>` block (`--cream`, `--ink`, `--accent`).

## Deploying to Vercel

1. Push this repo to GitHub.
2. In Vercel, **Add New → Project** → import the repo. No framework/build settings needed (static site) — leave build command empty and output directory as `./`.
3. Deploy. Vercel will serve `index.html` at the root.

## Domains

**Primary: `libokehouse.com` (Namecheap)**
1. In the Vercel project → **Settings → Domains**, add `libokehouse.com` (and `www.libokehouse.com` if you want the www version too — set one as the redirect target for the other, Vercel does this for you).
2. Vercel will show you the DNS records to add. In Namecheap → Domain → **Advanced DNS**, add those records (typically an `A` record pointing at Vercel's IP, or a `CNAME` for the `www` subdomain — Vercel's UI gives you the exact values to paste).
3. Wait for DNS to propagate (usually minutes to a few hours), then Vercel auto-issues an SSL certificate.

**Secondary: `libokehouse.co.ke` → redirects to `.com` (hosted at HostAfrica)**
This domain is *not* pointed at Vercel — it stays on HostAfrica and simply forwards visitors to the main site. This is the simpler and more reliable setup since HostAfrica manages the `.co.ke` DNS.
1. Log into your HostAfrica client area / cPanel for `libokehouse.co.ke`.
2. Look for a **"Redirects"** or **"Domain Forwarding"** tool (in cPanel it's usually under *Domains → Redirects*).
3. Set up a redirect from `libokehouse.co.ke` (and `www.libokehouse.co.ke`) to `https://libokehouse.com/`, as a **301 (permanent)** redirect.
4. If HostAfrica only offers DNS-level forwarding rather than cPanel redirects, ask their support to set up a 301 redirect/URL forward to `https://libokehouse.com/` — this is a standard request.

> Alternative (more setup, skip unless you need it): you could instead add `libokehouse.co.ke` as a domain inside the *same* Vercel project and let `vercel.json`'s redirect rules handle the bounce to `.com`. That requires pointing the `.co.ke` DNS at Vercel instead of HostAfrica, which only makes sense if you want everything managed in one place.

## Notes

- `1002099015.jpg` (unbranded tote) and `1002099017.jpg` (leaf-bundle graphic, carries a pngtree watermark) were **not** used in the site — the watermarked one isn't cleared for commercial use. They're left in the repo root in case you want them for reference; feel free to delete.
- Security headers (`X-Frame-Options`, `X-Content-Type-Options`, etc.) are set in `vercel.json` and apply automatically once deployed.
