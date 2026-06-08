# 235 Electric website (SoW draft)

Static site built from the layout and patterns in the [EASI reference site](../website/), with content from **Logo and website SoW for 235 Electric.pdf**.

**Live demo host:** `https://samplesite.joshuapastizzo.com` (subdomain on joshuapastizzo.com via local Caddy)

## Pages (SoW + landing)

| Page | File | SoW requirement |
|------|------|----------------|
| Home | `index.html` | Landing; summarizes value prop and links to SoW pages |
| About | `about/index.html` | Company building radioisotope generators for data centers, 1 to 100 kW |
| Customers | `customers/index.html` | Co-60 + TPV technology, product advantages, comparison, deployment, economics |
| Investors | `investors/index.html` | Brief intro + downloadable seed investor deck (PDF) |
| Contact | `contact/index.html` | Form → `tamas@235electric.com`, Wilmington address |

Pages live in folders (`/about`, `/customers`, …) so clean URLs work without `.html`. Use a local server (below). Opening `index.html` directly in the browser will not resolve `/about` paths.

## Hosting on `samplesite.joshuapastizzo.com` (Caddy)

1. **name.com:** A record host `samplesite` → your home public IP (no underscores in the hostname; required for HTTPS certs).
2. **Router:** Forward **80** and **443** to the PC running Caddy (same as your existing setup).
3. **Caddy:** Add the site block from `Caddyfile.example` (update the `root` path if needed). Use the `rewrite` + `file_server` pattern, not `try_files` on `/`, which can cause a blank page.
4. Reload Caddy. Links use root paths (`/about`, `/css/...`), which is correct for a subdomain.

Main site `joshuapastizzo.com` can stay on Vercel; only `samplesite.joshuapastizzo.com` points home.

## Assets

- **Logo:** `images/Logo.png` (navy `#05223d` + white)
- **Generator:** `images/RTG.png`, `images/RTG2.png`
- **Capsule:** `images/Cap1.png`, `images/Cap2.png`, `images/Cap3.png`
- **Investor deck:** `assets/235-electric-seed-investor-deck.pdf` (linked from Investors page)

## SoW items not in this repo
- **LinkedIn:** One-liner, cover image, and sample posts are separate from this site. Suggested tagline from SoW: *“Nuclear generators that provide quiet, clean energy for data centers.”*

## Contact form

Uses [FormSubmit](https://formsubmit.co/) to deliver to `tamas@235electric.com` (SoW address). On first submit, FormSubmit may ask you to confirm the recipient email.

## Run locally

```bash
cd website_contract_test
python -m http.server 8000
```

Open `http://localhost:8000` (clean URLs like `/about` still need Caddy or similar; see `Caddyfile.example`).

## Brand colors

Edit `:root` in `css/style.css`: navy `#05223d` (from logo), white accents on dark surfaces.
